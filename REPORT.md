# Lowdown Scanner Report: MCP Registry reachability observations

- **Data as of:** 2026-11-10 02:01 UTC (2026-11-10 11:01 KST), the end of the most recent Scanner run
- **Report generated:** 2026-11-10 02:24 UTC
- **Observation period:** 2026-10-06 to 2026-11-10 (UTC)

Lowdown Scanner observes 10,000 MCP Registry entries every day and records MCP initialize and tools/list reachability, HTTP status, latency, and tool-count changes. This report summarizes the most recent run. The 10,000 entries are a fixed sample (cohort `2026-10-29-v3`): all 2,000 entries of the earlier cohort `2026-10-07-v1` plus 8,000 entries added when the sample was extended, selected from the official MCP Registry with a per-host limit (rules in the README) and unchanged since. They are Registry entries, not operators, and they do not represent the whole Registry.

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
| Cohort entries (fixed sample, `2026-10-29-v3`) | 10,000 |
| Cohort entries with at least one observation row in this run | 9,914 |
| Cohort entries with no observation row in this run | 86 |
| Entries of the earlier cohort `2026-10-07-v1` with at least one observation row (of 2,000) | 1,963 |
| Observation rows in this run (an entry with several remotes has several rows) | 10,049 |
| Rows where the Scanner did not call the URL (blocked by its safety checks) | 4 |
| Probe attempts (observation rows minus rows not called) | 10,045 |

## Reach level of probe attempts

| reached_level | Meaning | Count (of 10,045 probe attempts) |
|---|---|---|
| 2 | initialize and tools/list completed | 5,581 |
| 1 | initialize completed; tools/list did not | 44 |
| 0 | initialize did not complete | 4,420 |

## HTTP status of probe attempts

| HTTP status | Count (of 10,045) |
|---|---|
| 200 | 5,610 |
| 401 | 3,187 |
| no HTTP response | 360 |
| 404 | 278 |
| 302 | 167 |
| 503 | 67 |
| 502 | 60 |
| 402 | 48 |
| 500 | 33 |
| 301 | 31 |
| 400 | 31 |
| 308 | 25 |
| 530 | 25 |
| 307 | 23 |
| 403 | 23 |
| 405 | 23 |
| 429 | 21 |
| 410 | 14 |
| 526 | 5 |
| 421 | 4 |
| 525 | 3 |
| 521 | 2 |
| 201 | 1 |
| 451 | 1 |
| 501 | 1 |
| 522 | 1 |
| 523 | 1 |

## Error types of probe attempts

| error_type | Count (of 10,045) |
|---|---|
| none | 9,670 |
| dns | 197 |
| timeout | 88 |
| tls | 51 |
| conn_reset | 18 |
| invalid_response | 14 |
| conn_refused | 6 |
| network_error | 1 |

## Hosts of probe attempts

A host is the hostname of a remote URL. Several entries can share one host, and one operator can use several hosts, so host counts are not operator counts. Host names are not listed.

| Measure | Value |
|---|---|
| Distinct hosts among probe attempts | 9,195 |
| Distinct hosts with at least one reached_level 2 row | 4,978 |
| Share of probe attempts on the most frequent host | 2.1% |
| Share of probe attempts on the three most frequent hosts | 4.2% |

## Last 7 runs

Totals change when the cohort changes. To compare across the change, use the `2026-10-07-v1` columns, which count only entries of the earlier cohort.

| Run date (UTC) | Cohort | Observation rows | Entries with a row | Rows with reached_level 2 | `2026-10-07-v1` entries with a row | `2026-10-07-v1` rows with reached_level 2 |
|---|---|---|---|---|---|---|
| 2026-11-04 | `2026-10-29-v3` | 10,060 | 9,928 | 5,518 | 1,965 | 1,228 |
| 2026-11-05 | `2026-10-29-v3` | 10,058 | 9,926 | 5,573 | 1,965 | 1,234 |
| 2026-11-06 | `2026-10-29-v3` | 10,058 | 9,925 | 5,556 | 1,965 | 1,226 |
| 2026-11-07 | `2026-10-29-v3` | 10,052 | 9,919 | 5,559 | 1,964 | 1,231 |
| 2026-11-08 | `2026-10-29-v3` | 10,049 | 9,916 | 5,566 | 1,963 | 1,233 |
| 2026-11-09 | `2026-10-29-v3` | 10,049 | 9,916 | 5,568 | 1,963 | 1,232 |
| 2026-11-10 | `2026-10-29-v3` | 10,049 | 9,914 | 5,581 | 1,963 | 1,227 |

## Data

Raw per-observation records are exported weekly as CSV in `scanner_observations/` in this repository. This report is regenerated from the database after each daily run.
