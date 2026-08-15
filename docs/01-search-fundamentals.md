# 01 — Search Fundamentals

Getting fluent in SPL and learning to think like a SOC analyst inside Splunk.
Full SPL for this module: [`queries/01-search-fundamentals.spl`](../queries/01-search-fundamentals.spl).

## Time range

Every search is bounded to the dataset window using a **Date Range** of
`07/01/2024 00:00:00` → `08/01/2024 00:00:00`. Getting the time picker right is
the difference between "no results" and the full 5,931-event picture.

![Time range picker](../screenshots/01-search-fundamentals/01-time-range-date-picker.png)

## Search modes

Splunk offers three search modes, and knowing when to use each matters for speed
vs. detail:

| Mode | What it does | Use when |
|------|--------------|----------|
| **Smart** | Balances field discovery and speed (default) | General searching |
| **Fast** | Minimal field extraction, fastest | You know exactly what you need |
| **Verbose** | Extracts every field it can | Deep-diving a small result set |

![Smart mode](../screenshots/01-search-fundamentals/02-search-mode-smart.png)
![Fast mode](../screenshots/01-search-fundamentals/03-search-mode-fast.png)
![Verbose mode](../screenshots/01-search-fundamentals/04-search-mode-verbose.png)

## The case-sensitivity rule (the one that bites everyone)

**Field _names_ are case-sensitive. Field _values_ are case-insensitive.**

Searching `Dest_ip="178.128.237.149"` (capital D) returns **0 events** — there is
no field called `Dest_ip`:

![Field name wrong case](../screenshots/01-search-fundamentals/05-fieldname-case-Dest_ip-0events.png)

Fix the field name to lowercase `dest_ip` and the same search returns **2,033
events**:

![Field name correct case](../screenshots/01-search-fundamentals/06-fieldname-case-dest_ip-2033events.png)

But the *value* doesn't care about case — `sourcetype=Csv` and `sourcetype=csv`
return the same events:

![Value Csv](../screenshots/01-search-fundamentals/07-fieldvalue-case-Csv-works.png)
![Value csv](../screenshots/01-search-fundamentals/08-fieldvalue-case-csv-works.png)

## Reading events and pivoting

Expanding an event shows its field/value pairs — the raw material for building
searches:

![Field value pairs](../screenshots/01-search-fundamentals/09-event-field-value-pairs.png)

The same logical thing (an IP) can appear under multiple field names
(`src_ip`, `dest_ip`, etc.), so it pays to check what's actually populated:

![Multiple IP fields](../screenshots/01-search-fundamentals/10-multiple-ip-field-names.png)

Splunk can also pivot to **nearby events** (±N seconds/minutes) around a chosen
event — invaluable for reconstructing what happened right before and after
something suspicious:

![Time pivot](../screenshots/01-search-fundamentals/11-time-pivot-nearby-events.png)

## Transforming commands

`stats` aggregates — here, counting connections between a specific source and
destination (112 events for that pair):

![stats count](../screenshots/01-search-fundamentals/12-stats-count-by-src-dest.png)

`table` shapes results into named columns. Note the `Src_ip` column comes back
**empty** — a live demonstration of the case rule above (the real field is
`src_ip`):

![table command](../screenshots/01-search-fundamentals/13-table-command-columns.png)
