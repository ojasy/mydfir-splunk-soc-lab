# 04 — Detections (Scheduled Alerts)

Moving from "looking at data" to "being told when something happens." Full SPL:
[`queries/04-alerts.spl`](../queries/04-alerts.spl).

**Naming convention** used throughout: `Category - MITRE ATT&CK ID - Activity`,
e.g. `Network- T1078- Successful SSH Authentication`. Consistent names make an
alerts backlog searchable and self-documenting.

---

## Walkthrough alert — Successful SSH Authentication (T1078)

**Goal:** fire whenever someone successfully authenticates to the SSH server, so
an analyst can OSINT the source IP and pivot ±5 minutes for indicators.

Base search enriches the successful login with `iplocation`:

![Base query](../screenshots/04-alerts/01-walkthrough-base-query.png)

The MITRE technique (**T1078 – Valid Accounts**) and the cron schedule were
looked up while building it — `*/15 * * * *` = every 15 minutes, confirmed on
crontab.guru:

![MITRE T1078](../screenshots/04-alerts/02-mitre-attack-t1078.png)
![crontab every 15 min](../screenshots/04-alerts/03-crontab-guru-every-15min.png)

**Alert config:**

| Setting | Value |
|---------|-------|
| Permissions | Shared in App |
| Alert type | Scheduled → Run on Cron Schedule `*/15 * * * *` |
| Trigger | Number of Results **is greater than 0** |
| Action | Add to Triggered Alerts, **Severity: Medium** |

![Save alert cron](../screenshots/04-alerts/04-save-alert-cron-schedule.png)
![Save alert severity](../screenshots/04-alerts/05-save-alert-medium-severity.png)

Permissions set to Everyone (read) / power+admin (write) so the whole app can
see it:

![Alert permissions](../screenshots/04-alerts/06-alert-permissions-shared.png)
![Alert saved](../screenshots/04-alerts/07-alert-saved-t1078.png)

**Verifying it works.** The Triggered Alerts page is where fired alerts land.
Testing the search against a live "Last 15 minutes" window correctly returns 0
results (the lab data is from Jan 2024) — proving the search and trigger logic
behave, without a false positive:

![Triggered alerts page](../screenshots/04-alerts/08-triggered-alerts-page.png)
![Test time window](../screenshots/04-alerts/09-test-relative-time-window.png)
![Test zero results](../screenshots/04-alerts/10-test-zero-results-live.png)

---

## Scenario alert — New User Account Created (T1136)

**Prompt:** *"Create a MEDIUM severity alert that fires if a new user account is
created. Run it every hour and send it to the Triggered Alerts page. Follow the
`Endpoint - <MITRE ID> - <Activity>` naming convention."*

Base search is the Event 4720 detection from the Windows dashboard:

![Scenario base query](../screenshots/04-alerts/11-scenario-4720-base-query.png)

**Alert config:**

| Setting | Value |
|---------|-------|
| Title | `Endpoint-T1136- New User Account Created` |
| Description | *Detects a newly created user account. Review both activities performed by the newly created user and source user for potential compromise.* |
| Permissions | Shared in App |
| Alert type | Scheduled → Run every hour, at 0 minutes past the hour |
| Trigger | Number of Results **is greater than 0** |
| Action | Add to Triggered Alerts, **Severity: Medium** |

![Scenario save alert](../screenshots/04-alerts/12-scenario-save-alert-t1136.png)
![Scenario alert saved](../screenshots/04-alerts/13-scenario-alert-saved-t1136.png)

## Day 27 accountability prompt

> *What alert and report did you create in Splunk today, and who would benefit
> from reading it in a real SOC?*

Created the T1078 SSH-auth alert and the T1136 new-account alert. In a real SOC
the SSH-auth alert would feed the tier-1 triage queue (fast OSINT + pivot on the
source IP), while the new-account alert is high-signal for tier-2 / IR — account
creation outside a change window is a classic persistence indicator worth an
immediate look.
