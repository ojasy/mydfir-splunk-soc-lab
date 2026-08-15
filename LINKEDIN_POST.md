# LinkedIn Post — Splunk SOC Detection Lab

Framed as hands-on technical work (building dashboards + detections), not as a
course completion. Uses the **MyDFIR LinkedIn Visibility Toolkit** structure.

**Before posting:**
- Replace the `[bracketed]` bits with your own words.
- Attach 2–3 of the strongest screenshots (suggested: final SSH dashboard
  `02-ssh-dashboard/12`, final Windows dashboard `03-windows-dashboard/08`, and
  the T1136 alert `04-alerts/13`).
- Keep the hashtags. @MYDFIR sits at the bottom as a dataset credit.
- Optionally add your referral link from your Skool dashboard.

---

## Primary — leads with the work

> I've been deep in Splunk lately, building out a SOC detection lab on a real
> intrusion dataset — and it's been some of the most useful hands-on work I've
> done.
>
> The goal: take raw SSH and Windows Security logs and run the full analyst loop
> — **search → visualise → detect → report.** What I built:
>
> 🔎 **Two investigation dashboards**
> • SSH Activity — surfaced a brute-force campaign against root (240 failed
>   attempts), the top source IP, and a geo-IP heatmap that flagged a successful
>   root login from an unexpected country.
> • Windows Activity — successful logons, admin-privilege assignment (Event
>   4672), and account creation (Event 4720) — which caught an account literally
>   named "evil" being spun up.
>
> 🚨 **Two scheduled detections**, mapped to MITRE ATT&CK:
> • T1078 – Successful SSH Authentication (every 15 min)
> • T1136 – New User Account Created (hourly, medium severity)
>
> 📊 **Two scheduled reports** for daily review, plus three "your SOC manager
> just emailed you" scenarios — including adding a Windows Firewall exception
> panel (Event 4946) to an existing dashboard.
>
> The most valuable part wasn't a clean win — it was a bug. A stats table kept
> returning zero rows even with events in the search. I was grouping by a field
> (Logon_Type) that doesn't exist on Event 4672. Tracking that down and fixing it
> is the actual job, so I documented it too.
>
> Put together, the panels trace a full intrusion chain: SSH brute force →
> valid-account login from an odd geo → privilege escalation → a new persistence
> account → firewall holes. Exactly what a SOC exists to catch.
>
> Full write-up, all the SPL, and annotated screenshots here: [GitHub link]
>
> [One honest line about where you're at — e.g. "Always sharpening the blue-team
> skillset. If your team is hiring SOC analysts in the [GTA / your area], I'd
> love to connect."]
>
> Dataset via @MYDFIR.
>
> #SOC #Splunk #CyberSecurity #BlueTeam #DetectionEngineering #SIEM #MITREATTACK #MYDFIR

---

## Alternative — shorter / punchier

> Spent the last few weeks deep in Splunk, building a SOC detection lab on a real
> intrusion dataset. 🔍
>
> From raw SSH + Windows Security logs, I built:
> → 2 investigation dashboards (SSH + Windows)
> → 2 MITRE-mapped detections (T1078, T1136)
> → 2 scheduled reports + 3 SOC-manager scenarios
>
> The dashboards trace a full intrusion: SSH brute force → valid-account login
> from an odd geo → an account named "evil" created → firewall holes punched.
> Exactly the chain a SOC exists to catch.
>
> Best lesson came from a broken search returning 0 rows — I was grouping on a
> field that doesn't exist on that event. Fixed it, documented it, because that's
> the real work.
>
> All the SPL + screenshots 👇 [GitHub link]
>
> [Your call-to-action line here.]
>
> Dataset via @MYDFIR.
>
> #Splunk #SOC #BlueTeam #CyberSecurity #DetectionEngineering #MYDFIR
