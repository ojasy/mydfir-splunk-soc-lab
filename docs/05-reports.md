# 05 — Reports (Scheduled Reports)

Reports document trends over time and get delivered on a cadence to teams or
leadership. Full SPL: [`queries/05-reports.spl`](../queries/05-reports.spl).

**Alerts vs. reports, in one line:** an alert tells you *something happened right
now*; a report gives you *a recurring, scheduled summary* to review.

---

## Walkthrough report — Daily SSH Server Outbound Comms

**Goal:** a daily report of the **top 3 destination IPs** that the SSH server
(`178.128.237.149`) is talking to — useful for spotting the server reaching out
somewhere it shouldn't.

Broad search on the IP first (4,018 events), then reduce to the top 3
destinations:

![Broad search](../screenshots/05-reports/01-walkthrough-broad-search-4018.png)
![Top 3 dest IP](../screenshots/05-reports/02-top3-destination-ip.png)

Top destinations: `178.128.225.222` (62.7%), `43.135.172.223` (5.65%),
`104.248.150.105` (5.65%).

**Save as report** → schedule **daily at 0:00**, time range **Yesterday**:

![Save as report](../screenshots/05-reports/03-save-as-report.png)
![Report created](../screenshots/05-reports/04-report-created-dialog.png)
![Schedule daily 0000](../screenshots/05-reports/05-schedule-daily-0000-yesterday.png)

---

## Scenario report — Daily Windows Successful Admin Logins

**Prompt:** *"Create a daily report named `Daily - Windows - Successful
Administrative Logins`… runs every day at 2 AM over 'Yesterday', querying all
Windows logins with administrative privileges. Filter out SYSTEM and computer
accounts. Include time, user & computer, sorted earliest-first."*

This is the **corrected** 4672 query (see the
[Windows dashboard bug write-up](03-windows-dashboard.md#gotcha-why-a-panel-returned-zero-rows))
— grouping by fields that actually exist on the event, and `sort +_time` for
earliest-first:

```spl
index="mydfir-lab1" host="winvm" EventCode=4672 user!=*$ user!=SYSTEM
| stats count by _time user ComputerName
| sort +_time
```

![Admin logins query](../screenshots/05-reports/06-scenario-admin-logins-query.png)

**Save as report** → schedule **daily at 2:00**, time range **Yesterday**:

![Scenario save report](../screenshots/05-reports/07-scenario-save-as-report.png)
![Scenario schedule 0200](../screenshots/05-reports/08-scenario-schedule-0200-yesterday.png)

The scheduled report page confirms the cadence ("runs daily, at 2:00, time range
is yesterday"). It shows no rows yet simply because the first scheduled run
hasn't fired — expected behaviour for a newly scheduled report:

![Scenario report scheduled](../screenshots/05-reports/09-scenario-report-scheduled-confirm.png)
