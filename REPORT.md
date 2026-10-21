# Lowdown Scanner Report: MCP Registry reachability observations

- **Data as of:** 2026-10-21 06:20 UTC (2026-10-21 15:20 KST), the end of the most recent Scanner run
- **Report generated:** 2026-10-21 06:24 UTC
- **Observation period:** 2026-10-06 to 2026-10-21 (UTC)

Lowdown Scanner observes 5,000 MCP Registry entries every day and records MCP initialize and tools/list reachability, HTTP status, latency, and tool-count changes. This report summarizes the most recent run. The 5,000 entries are a fixed sample (cohort `2026-10-19-v2`): all 2,000 entries of the earlier cohort `2026-10-07-v1` plus 3,000 entries added when the sample was extended, selected from the official MCP Registry with a per-host limit (rules in the README) and unchanged since. They are Registry entries, not operators, and they do not represent the whole Registry.

## Scope and limits

- The Scanner sends `initialize` and `tools/list` only. It never calls a tool and does not authenticate. A `401` or `403` is recorded as the HTTP status that was observed; it is not classified as success or failure.
- The Scanner does not follow redirects; a `3xx` status is recorded as the response received from the original URL.
- Each entry is observed once per day from a single network location (GitHub Actions). These counts describe single probes, not availability or uptime.
- `reached_level 2` means the probe completed `initialize` and `tools/list` at that moment. It does not mean a tool executed successfully.
- Cohort entries with no observation row in a run are counted separately and are not recorded as failures.
- This report contains no scores, rankings, labels, or individual server names.

## Latest run

| Measure | Count |
|---|---|
| Cohort entries (fixed sample, `2026-10-19-v2`) | 5,000 |
| Cohort entries with at least one observation row in this run | 4,970 |
| Cohort entries with no observation row in this run | 30 |
| Entries of the earlier cohort `2026-10-07-v1` with at least one observation row (of 2,000) | 1,973 |
| Observation rows in this run (an entry with several remotes has several rows) | 5,022 |
| Rows where the Scanner did not call the URL (blocked by its safety checks) | 3 |
| Probe attempts (observation rows minus rows not called) | 5,019 |

## Reach level of probe attempts

| reached_level | Meaning | Count (of 5,019 probe attempts) |
|---|---|---|
| 2 | initialize and tools/list completed | 3,001 |
| 1 | initialize completed; tools/list did not | 21 |
| 0 | initialize did not complete | 1,997 |

## HTTP status of probe attempts

| HTTP status | Count (of 5,019) |
|---|---|
| 200 | 3,018 |
| 401 | 1,505 |
| no HTTP response | 157 |
| 404 | 142 |
| 503 | 31 |
| 402 | 19 |
| 307 | 18 |
| 500 | 18 |
| 308 | 16 |
| 403 | 13 |
| 502 | 13 |
| 530 | 13 |
| 301 | 11 |
| 400 | 11 |
| 410 | 10 |
| 405 | 8 |
| 429 | 6 |
| 302 | 2 |
| 421 | 2 |
| 521 | 2 |
| 525 | 2 |
| 526 | 2 |

## Error types of probe attempts

| error_type | Count (of 5,019) |
|---|---|
| none | 4,854 |
| dns | 101 |
| timeout | 28 |
| tls | 19 |
| invalid_response | 8 |
| conn_reset | 7 |
| conn_refused | 2 |

## Hosts of probe attempts

A host is the hostname of a remote URL. Several entries can share one host, and one operator can use several hosts, so host counts are not operator counts. Host names are not listed.

| Measure | Value |
|---|---|
| Distinct hosts among probe attempts | 4,361 |
| Distinct hosts with at least one reached_level 2 row | 2,477 |
| Share of probe attempts on the most frequent host | 4.2% |
| Share of probe attempts on the three most frequent hosts | 8.5% |

## Last 7 runs

Totals change when the cohort changes. To compare across the change, use the `2026-10-07-v1` columns, which count only entries of the earlier cohort.

| Run date (UTC) | Cohort | Observation rows | Entries with a row | Rows with reached_level 2 | `2026-10-07-v1` entries with a row | `2026-10-07-v1` rows with reached_level 2 |
|---|---|---|---|---|---|---|
| 2026-10-15 | `2026-10-07-v1` | 1,990 | 1,980 | 1,283 | 1,980 | 1,283 |
| 2026-10-16 | `2026-10-07-v1` | 1,992 | 1,982 | 1,289 | 1,982 | 1,289 |
| 2026-10-17 | `2026-10-07-v1` | 1,988 | 1,978 | 1,289 | 1,978 | 1,289 |
| 2026-10-18 | `2026-10-07-v1` | 1,987 | 1,977 | 1,281 | 1,977 | 1,281 |
| 2026-10-19 | `2026-10-19-v2` | 5,030 | 4,977 | 3,007 | 1,977 | 1,283 |
| 2026-10-20 | `2026-10-19-v2` | 5,022 | 4,970 | 2,961 | 1,973 | 1,268 |
| 2026-10-21 | `2026-10-19-v2` | 5,022 | 4,970 | 3,001 | 1,973 | 1,279 |

## Data

Raw per-observation records are exported weekly as CSV in `scanner_observations/` in this repository. This report is regenerated from the database after each daily run.
