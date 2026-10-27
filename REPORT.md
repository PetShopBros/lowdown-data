# Lowdown Scanner Report: MCP Registry reachability observations

- **Data as of:** 2026-10-27 01:31 UTC (2026-10-27 10:31 KST), the end of the most recent Scanner run
- **Report generated:** 2026-10-27 01:36 UTC
- **Observation period:** 2026-10-06 to 2026-10-27 (UTC)

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
| Cohort entries with at least one observation row in this run | 4,955 |
| Cohort entries with no observation row in this run | 45 |
| Entries of the earlier cohort `2026-10-07-v1` with at least one observation row (of 2,000) | 1,968 |
| Observation rows in this run (an entry with several remotes has several rows) | 5,013 |
| Rows where the Scanner did not call the URL (blocked by its safety checks) | 3 |
| Probe attempts (observation rows minus rows not called) | 5,010 |

## Reach level of probe attempts

| reached_level | Meaning | Count (of 5,010 probe attempts) |
|---|---|---|
| 2 | initialize and tools/list completed | 2,965 |
| 1 | initialize completed; tools/list did not | 20 |
| 0 | initialize did not complete | 2,025 |

## HTTP status of probe attempts

| HTTP status | Count (of 5,010) |
|---|---|
| 200 | 2,984 |
| 401 | 1,499 |
| no HTTP response | 170 |
| 404 | 146 |
| 503 | 33 |
| 402 | 21 |
| 500 | 21 |
| 502 | 19 |
| 307 | 18 |
| 308 | 17 |
| 530 | 15 |
| 301 | 13 |
| 403 | 11 |
| 400 | 10 |
| 410 | 10 |
| 405 | 8 |
| 429 | 5 |
| 526 | 3 |
| 302 | 2 |
| 421 | 2 |
| 525 | 2 |
| 521 | 1 |

## Error types of probe attempts

| error_type | Count (of 5,010) |
|---|---|
| none | 4,831 |
| dns | 105 |
| timeout | 33 |
| tls | 23 |
| conn_reset | 8 |
| invalid_response | 8 |
| conn_refused | 2 |

## Hosts of probe attempts

A host is the hostname of a remote URL. Several entries can share one host, and one operator can use several hosts, so host counts are not operator counts. Host names are not listed.

| Measure | Value |
|---|---|
| Distinct hosts among probe attempts | 4,348 |
| Distinct hosts with at least one reached_level 2 row | 2,443 |
| Share of probe attempts on the most frequent host | 4.2% |
| Share of probe attempts on the three most frequent hosts | 8.5% |

## Last 7 runs

Totals change when the cohort changes. To compare across the change, use the `2026-10-07-v1` columns, which count only entries of the earlier cohort.

| Run date (UTC) | Cohort | Observation rows | Entries with a row | Rows with reached_level 2 | `2026-10-07-v1` entries with a row | `2026-10-07-v1` rows with reached_level 2 |
|---|---|---|---|---|---|---|
| 2026-10-21 | `2026-10-19-v2` | 5,022 | 4,970 | 3,001 | 1,973 | 1,279 |
| 2026-10-22 | `2026-10-19-v2` | 5,022 | 4,969 | 2,974 | 1,972 | 1,271 |
| 2026-10-23 | `2026-10-19-v2` | 5,022 | 4,969 | 2,947 | 1,972 | 1,263 |
| 2026-10-24 | `2026-10-19-v2` | 5,015 | 4,961 | 2,970 | 1,969 | 1,271 |
| 2026-10-25 | `2026-10-19-v2` | 5,017 | 4,959 | 2,976 | 1,968 | 1,274 |
| 2026-10-26 | `2026-10-19-v2` | 5,015 | 4,957 | 2,962 | 1,968 | 1,267 |
| 2026-10-27 | `2026-10-19-v2` | 5,013 | 4,955 | 2,965 | 1,968 | 1,269 |

## Data

Raw per-observation records are exported weekly as CSV in `scanner_observations/` in this repository. This report is regenerated from the database after each daily run.
