# Screenshot Placement Guide

Every screenshot has already been copied into `screenshots/<module>/` under a
clean, ordered name (this is done in the zip). This table is the map: your
**original filename → where it lives now → what it shows**. Use it if you ever
re-export a screenshot and need to know where it belongs.

## 00 — Setup → `screenshots/00-setup/`

| Your file | New name | Shows |
|-----------|----------|-------|
| `01-app-installed.png` | `01-app-install-success.png` | MyDFIR-Splunk app install success |
| `02-timezone-gmt.png` | `02-timezone-set-gmt.png` | Timezone set to GMT |
| `03-indexes-page.png` | `03-index-mydfir-lab1-active.png` | `mydfir-lab1` index active, 5.93K events |

## 01 — Search Fundamentals → `screenshots/01-search-fundamentals/`

| Your file | New name | Shows |
|-----------|----------|-------|
| `04-base-search-time-range.png` | `01-time-range-date-picker.png` | Date range picker |
| `05-smart-mode.png` | `02-search-mode-smart.png` | Smart mode |
| `06-fast-mode.png` | `03-search-mode-fast.png` | Fast mode |
| `07-verbose-mode.png` | `04-search-mode-verbose.png` | Verbose mode |
| `08-case-sensitive-name-Dest_ip-zero.png` | `05-fieldname-case-Dest_ip-0events.png` | `Dest_ip` (wrong case) → 0 events |
| `09-case-sensitive-name-dest_ip-works.png` | `06-fieldname-case-dest_ip-2033events.png` | `dest_ip` → 2,033 events |
| `10-case-sensitive-value-Csv-works.png` | `07-fieldvalue-case-Csv-works.png` | Value `Csv` works |
| `11-case-sensitive-value-csv-works.png` | `08-fieldvalue-case-csv-works.png` | Value `csv` works |
| `12-expanded-event-field-value-pairs.png` | `09-event-field-value-pairs.png` | Expanded event fields |
| `13-ip-multiple-field-names.png` | `10-multiple-ip-field-names.png` | Same IP under multiple fields |
| `14-time-pivot-nearby-events.png` | `11-time-pivot-nearby-events.png` | ±N second nearby-events pivot |
| `15-stats-count-src-dest-112.png` | `12-stats-count-by-src-dest.png` | `stats count by src/dest` (112) |
| `16-table-command-112-rows.png` | `13-table-command-columns.png` | `table` cmd (empty `Src_ip` col) |

## 02 — SSH Dashboard → `screenshots/02-ssh-dashboard/`

| Your file | New name | Shows |
|-----------|----------|-------|
| `17-ssh-failed-search-284.png` | `01-failed-auth-search-284.png` | Failed SSH search (284) |
| `18-ssh-top-user-root-84pct.png` | `02-top-failed-user-root-84pct.png` | `top user` → root 84.5% |
| `19-ssh-single-value-viz.png` | `03-single-value-visualization.png` | Single Value viz picker |
| `20-ssh-save-new-dashboard.png` | `04-save-panel-top-failed-account.png` | Save panel → new SSH Activity dashboard |
| `21-ssh-top-source-ip.png` | `05-save-panel-top-source-ip.png` | Save Top Source IP panel |
| `22-ssh-failed-attempts-by-user.png` | `06-save-panel-failed-attempts-by-user.png` | Save Failed Attempts by User panel |
| `23-ssh-iplocation-greenland-canada.png` | `07-iplocation-successful-logins.png` | `iplocation` → Greenland/Canada logins |
| `24-ssh-successful-logins-save.png` | `08-save-panel-successful-logins.png` | Save Successful Logins panel |
| `25-ssh-geom-heatmap-query.png` | `09-geom-heatmap-query.png` | `geom geo_countries` query |
| `26-ssh-heatmap-categorical-colors.png` | `10-choropleth-categorical-colors.png` | Choropleth, Categorical colours |
| `27-ssh-dashboard-raw-light.png` | `11-dashboard-light-theme.png` | Dashboard, light theme |
| `28-ssh-dashboard-final-dark.png` | `12-dashboard-final-dark.png` | Dashboard, final dark |

## 03 — Windows Dashboard → `screenshots/03-windows-dashboard/`

| Your file | New name | Shows |
|-----------|----------|-------|
| `29-win-993-events-host-filtered.png` | `01-host-winvm-993-events.png` | `host=winvm` (993) |
| `30-win-eventcode-4624-278.png` | `02-eventcode-4624-278.png` | 4624 logons (278) |
| `31-win-exclude-system-accounts-70.png` | `03-exclude-machine-accounts-70.png` | Exclude machine accts (70) |
| `32-win-successful-logins-kporter.png` | `04-successful-logins-by-user.png` | Successful logins → kporter |
| `33-win-eventcode-4672-zero-stats.png` | `05-4672-logontype-returns-0-BUG.png` | **The bug:** 4672 by Logon_Type → 0 rows |
| `34-win-4720-evil-account-stats.png` | `06-4720-new-account-evil.png` | 4720 → account "evil" |
| `35-win-new-account-full-stats.png` | `07-new-account-full-detail.png` | 4720 full detail |
| `36-win-dashboard-final-dark.png` | `08-dashboard-final-dark.png` | Windows dashboard, final |

## 04 — Alerts → `screenshots/04-alerts/`

| Your file | New name | Shows |
|-----------|----------|-------|
| `answer_for_day_29-4.png` | `01-walkthrough-base-query.png` | T1078 base query (iplocation) |
| `answer_for_day_29-5.png` | `02-mitre-attack-t1078.png` | MITRE ATT&CK T1078 page |
| `answer_for_day_29-6.png` | `03-crontab-guru-every-15min.png` | crontab.guru `*/15 * * * *` |
| `answer_for_day_29-7.png` | `04-save-alert-cron-schedule.png` | Save alert, cron schedule |
| `answer_for_day_29-8.png` | `05-save-alert-medium-severity.png` | Save alert, Medium severity |
| `answer_for_day_29-9.png` | `06-alert-permissions-shared.png` | Alert permissions (shared) |
| `answer_for_day_29-10.png` | `07-alert-saved-t1078.png` | T1078 alert saved page |
| `answer_for_day_29-11.png` | `08-triggered-alerts-page.png` | Triggered Alerts page |
| `answer_for_day_29-12.png` | `09-test-relative-time-window.png` | Test: relative time window |
| `answer_for_day_29-13.png` | `10-test-zero-results-live.png` | Test: 0 results on live window |
| `answer_for_day_29-1.png` | `11-scenario-4720-base-query.png` | Scenario 4720 base query |
| `answer_for_day_29-2.png` | `12-scenario-save-alert-t1136.png` | Scenario save alert (T1136) |
| `answer_for_day_29-3.png` | `13-scenario-alert-saved-t1136.png` | Scenario T1136 alert saved |

## 05 — Reports → `screenshots/05-reports/`

| Your file | New name | Shows |
|-----------|----------|-------|
| `answer_for_day_29-14.png` | `01-walkthrough-broad-search-4018.png` | Broad IP search (4,018) |
| `answer_for_day_29-15.png` | `02-top3-destination-ip.png` | `top limit=3 dest_ip` |
| `answer_for_day_29-16.png` | `03-save-as-report.png` | Save As Report dialog |
| `answer_for_day_29-17.png` | `04-report-created-dialog.png` | Report created dialog |
| `answer_for_day_29-18.png` | `05-schedule-daily-0000-yesterday.png` | Schedule daily 0:00, Yesterday |
| `answer_for_day_30-1.png` | `06-scenario-admin-logins-query.png` | Admin logins query (fixed 4672) |
| `answer_for_day_30-2.png` | `07-scenario-save-as-report.png` | Scenario Save As Report |
| `answer_for_day_30-3.png` | `08-scenario-schedule-0200-yesterday.png` | Schedule daily 2:00, Yesterday |
| `answer_for_day_30-4.png` | `09-scenario-report-scheduled-confirm.png` | Scheduled report confirmation |

## 06 — Scenario: Firewall Panel → `screenshots/06-scenario-firewall-panel/`

| Your file | New name | Shows |
|-----------|----------|-------|
| `answer_for_day_28-1.png` | `01-4946-firewall-exception-query.png` | 4946 firewall-rule query (53) |
| `answer_for_day_28-2.png` | `02-save-panel-firewall-exception.png` | Save "Firewall Exception Added" |
| `answer_for_day_28-3.png` | `03-dashboard-with-firewall-panel.png` | Windows dashboard + firewall panel |
