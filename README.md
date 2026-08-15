# MyDFIR — Splunk SOC Analyst Lab (Month 1)

Hands-on Splunk Enterprise lab documenting the SOC analyst workflow end to end:
**search → visualise → detect → report**. Built on the MyDFIR Month 1 dataset
(SSH + Windows Security telemetry), this repo walks through building two
investigation dashboards, two scheduled detections, two scheduled reports, and
three manager-driven scenarios — all mapped to MITRE ATT&CK where relevant.

![Splunk](https://img.shields.io/badge/Splunk-Enterprise%2010.4-black)
![SPL](https://img.shields.io/badge/Language-SPL-green)
![MITRE ATT&CK](https://img.shields.io/badge/MITRE%20ATT%26CK-T1078%20%7C%20T1136-red)
![Focus](https://img.shields.io/badge/Focus-SOC%20%7C%20Detection%20Engineering-blue)

---

## What this lab demonstrates

- **Log analysis in SPL** — searching, filtering, field extraction, `stats`,
  `top`, `table`, `iplocation`, and `geom`, plus the case-sensitivity rules that
  trip people up in real investigations.
- **Investigation dashboards** — an SSH Activity dashboard and a Windows Activity
  dashboard that turn raw auth logs into panels an analyst can triage at a glance.
- **Detection engineering** — scheduled alerts with cron/interval triggers,
  thresholds, severities, and app-level sharing, named with a consistent
  `Category - MITRE ID - Activity` convention.
- **Reporting** — scheduled reports for leadership/other teams, with sensible
  cadence and "Yesterday" time ranges.
- **Scenario response** — three tasks framed as requests from a SOC manager
  (add a dashboard panel, build a specific alert, build a specific report).

---

## The story in the data

The dataset is small on purpose, but the events line up into a coherent
intrusion narrative — which is exactly what the dashboards and detections are
built to surface:

| Stage | What the telemetry shows | Where it surfaces |
|-------|--------------------------|-------------------|
| **Initial Access** | Heavy SSH brute force against `root` — **240** failed attempts, top source `178.128.225.222` | SSH dashboard: *Top Failed Account*, *Top Source IP* |
| **Valid Accounts (T1078)** | Successful `root` logins from Canada **and one from Greenland** (`91.90.120.159`) | SSH dashboard: *Successful Logins by User* + heatmap |
| **Privileged activity** | `kporter` repeatedly assigned special/admin privileges (Event **4672**) | Windows dashboard: *Users with Admin Privileges* |
| **Persistence (T1136)** | `kporter` creates a new local account named **`evil`** (Event **4720**) | Windows dashboard: *New User Account Created* + T1136 alert |
| **Defense Evasion** | Windows Firewall exception rules **added** (Event **4946**) | Scenario: *Firewall Exception Added* panel |

> Lab dataset: index `mydfir-lab1`, window `2024-01-07 00:00 → 2024-01-08 00:00`,
> **5,931** total events.

---

## Modules

Each module has its own write-up with the SPL, the reasoning, and annotated
screenshots.

| # | Module | What you'll find |
|---|--------|------------------|
| 00 | [Lab Setup](docs/00-setup.md) | Installing the app, setting the timezone, confirming the index |
| 01 | [Search Fundamentals](docs/01-search-fundamentals.md) | SPL basics, search modes, the case-sensitivity rules, `stats`/`table` |
| 02 | [SSH Activity Dashboard](docs/02-ssh-dashboard.md) | 5 panels incl. geo-IP enrichment and a choropleth heatmap |
| 03 | [Windows Activity Dashboard](docs/03-windows-dashboard.md) | 3 panels for logons, admin privilege, and account creation |
| 04 | [Detections / Alerts](docs/04-alerts.md) | T1078 SSH auth alert + T1136 new-account alert |
| 05 | [Reports](docs/05-reports.md) | Daily outbound-comms report + daily admin-logins report |
| 06 | [Scenario: Firewall Exception Panel](docs/06-scenario-firewall-panel.md) | Event 4946 panel added to the Windows dashboard |

All raw SPL also lives together under [`/queries`](queries) if you just want the
searches.

---

## Skills evidenced

`Splunk Enterprise` · `SPL` · `Log analysis` · `SIEM dashboarding` ·
`Detection engineering` · `Scheduled alerting & reporting` ·
`Windows Security event analysis (4624 / 4672 / 4720 / 4946)` ·
`Linux auth log analysis` · `Geo-IP enrichment` · `MITRE ATT&CK mapping`

A short, honest note on a **real bug I hit and fixed** (a `stats by` clause that
silently returned zero rows on Event 4672) is written up in the
[Windows dashboard module](docs/03-windows-dashboard.md#gotcha-why-a-panel-returned-zero-rows) —
because debugging a broken search *is* the job.

---

## Repo structure

```
mydfir-splunk-soc-lab/
├── README.md
├── SCREENSHOT_GUIDE.md          # exactly which screenshot belongs to which step
├── docs/                        # per-module write-ups
│   ├── 00-setup.md
│   ├── 01-search-fundamentals.md
│   ├── 02-ssh-dashboard.md
│   ├── 03-windows-dashboard.md
│   ├── 04-alerts.md
│   ├── 05-reports.md
│   └── 06-scenario-firewall-panel.md
├── queries/                     # all SPL, one file per module
│   ├── 01-search-fundamentals.spl
│   ├── 02-ssh-activity-dashboard.spl
│   ├── 03-windows-activity-dashboard.spl
│   ├── 04-alerts.spl
│   ├── 05-reports.spl
│   └── 06-scenario-firewall-panel.spl
└── screenshots/                 # organised by module, in step order
    ├── 00-setup/
    ├── 01-search-fundamentals/
    ├── 02-ssh-dashboard/
    ├── 03-windows-dashboard/
    ├── 04-alerts/
    ├── 05-reports/
    └── 06-scenario-firewall-panel/
```

---

## Credits

Dataset and lab structure from the **[MyDFIR](https://www.mydfir.com/)** SOC
analyst program #MyDFIRFORGE (Month 1). All screenshots are my own work carried out in my
home lab.
