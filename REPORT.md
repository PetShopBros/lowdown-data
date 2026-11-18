# Lowdown Scanner Report: MCP Registry reachability observations

- **Data as of:** 2026-11-18 01:54 UTC (2026-11-18 10:54 KST), the end of the most recent Scanner run
- **Report generated:** 2026-11-18 02:08 UTC
- **Observation period:** 2026-10-06 to 2026-11-18 (UTC)

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
| Cohort entries with at least one observation row in this run | 9,894 |
| Cohort entries with no observation row in this run | 106 |
| Entries of the earlier cohort `2026-10-07-v1` with at least one observation row (of 2,000) | 1,961 |
| Observation rows in this run (an entry with several remotes has several rows) | 10,030 |
| Rows where the Scanner did not call the URL (blocked by its safety checks) | 4 |
| Probe attempts (observation rows minus rows not called) | 10,026 |

## Reach level of probe attempts

| reached_level | Meaning | Count (of 10,026 probe attempts) |
|---|---|---|
| 2 | initialize and tools/list completed | 5,314 |
| 1 | initialize completed; tools/list did not | 45 |
| 0 | initialize did not complete | 4,667 |

## HTTP status of probe attempts

| HTTP status | Count (of 10,026) |
|---|---|
| 200 | 5,345 |
| 401 | 3,146 |
| 404 | 516 |
| no HTTP response | 383 |
| 302 | 167 |
| 503 | 85 |
| 502 | 61 |
| 402 | 54 |
| 301 | 31 |
| 400 | 29 |
| 403 | 27 |
| 405 | 27 |
| 530 | 26 |
| 500 | 25 |
| 429 | 23 |
| 308 | 22 |
| 307 | 21 |
| 410 | 17 |
| 421 | 4 |
| 526 | 4 |
| 521 | 3 |
| 525 | 3 |
| 202 | 2 |
| 201 | 1 |
| 451 | 1 |
| 501 | 1 |
| 504 | 1 |
| 523 | 1 |

## Error types of probe attempts

| error_type | Count (of 10,026) |
|---|---|
| none | 9,624 |
| dns | 219 |
| timeout | 91 |
| tls | 55 |
| conn_reset | 15 |
| invalid_response | 15 |
| conn_refused | 5 |
| network_error | 2 |

## Hosts of probe attempts

A host is the hostname of a remote URL. Several entries can share one host, and one operator can use several hosts, so host counts are not operator counts. Host names are not listed.

| Measure | Value |
|---|---|
| Distinct hosts among probe attempts | 9,176 |
| Distinct hosts with at least one reached_level 2 row | 4,921 |
| Share of probe attempts on the most frequent host | 2.1% |
| Share of probe attempts on the three most frequent hosts | 4.2% |

## Last 7 runs

Totals change when the cohort changes. To compare across the change, use the `2026-10-07-v1` columns, which count only entries of the earlier cohort.

| Run date (UTC) | Cohort | Observation rows | Entries with a row | Rows with reached_level 2 | `2026-10-07-v1` entries with a row | `2026-10-07-v1` rows with reached_level 2 |
|---|---|---|---|---|---|---|
| 2026-11-12 | `2026-10-29-v3` | 10,045 | 9,910 | 5,569 | 1,962 | 1,226 |
| 2026-11-13 | `2026-10-29-v3` | 10,044 | 9,908 | 5,563 | 1,962 | 1,230 |
| 2026-11-14 | `2026-10-29-v3` | 10,045 | 9,906 | 5,567 | 1,962 | 1,231 |
| 2026-11-15 | `2026-10-29-v3` | 10,044 | 9,904 | 5,566 | 1,962 | 1,231 |
| 2026-11-16 | `2026-10-29-v3` | 10,035 | 9,901 | 5,544 | 1,962 | 1,228 |
| 2026-11-17 | `2026-10-29-v3` | 10,029 | 9,894 | 5,535 | 1,961 | 1,225 |
| 2026-11-18 | `2026-10-29-v3` | 10,030 | 9,894 | 5,314 | 1,961 | 1,011 |

## Data

Raw per-observation records are exported weekly as CSV in `scanner_observations/` in this repository. This report is regenerated from the database after each daily run.
