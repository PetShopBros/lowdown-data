# Lowdown Scanner Report: MCP Registry reachability observations

- **Data as of:** 2026-10-18 06:09 UTC (2026-10-18 15:09 KST), the end of the most recent Scanner run
- **Report generated:** 2026-10-18 06:10 UTC
- **Observation period:** 2026-10-06 to 2026-10-18 (UTC)

Lowdown Scanner observes 2,000 MCP Registry entries every day and records MCP initialize and tools/list reachability, HTTP status, latency, and tool-count changes. This report summarizes the most recent run. The 2,000 entries are a fixed sample (cohort `2026-10-07-v1`) selected once from the official MCP Registry and unchanged since; they are Registry entries, not operators, and they do not represent the whole Registry.

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
| Cohort entries (fixed sample, `2026-10-07-v1`) | 2,000 |
| Cohort entries with at least one observation row in this run | 1,977 |
| Cohort entries with no observation row in this run | 23 |
| Observation rows in this run (an entry with several remotes has several rows) | 1,987 |
| Rows where the Scanner did not call the URL (blocked by its safety checks) | 2 |
| Probe attempts (observation rows minus rows not called) | 1,985 |

## Reach level of probe attempts

| reached_level | Meaning | Count (of 1,985 probe attempts) |
|---|---|---|
| 2 | initialize and tools/list completed | 1,281 |
| 1 | initialize completed; tools/list did not | 10 |
| 0 | initialize did not complete | 694 |

## HTTP status of probe attempts

| HTTP status | Count (of 1,985) |
|---|---|
| 200 | 1,289 |
| 401 | 505 |
| 404 | 64 |
| no HTTP response | 47 |
| 503 | 11 |
| 402 | 9 |
| 308 | 7 |
| 307 | 6 |
| 405 | 6 |
| 500 | 6 |
| 502 | 6 |
| 530 | 6 |
| 410 | 5 |
| 301 | 4 |
| 400 | 4 |
| 403 | 4 |
| 429 | 2 |
| 302 | 1 |
| 421 | 1 |
| 521 | 1 |
| 526 | 1 |

## Error types of probe attempts

| error_type | Count (of 1,985) |
|---|---|
| none | 1,934 |
| dns | 27 |
| timeout | 11 |
| tls | 10 |
| invalid_response | 2 |
| conn_refused | 1 |

## Last 7 runs

| Run date (UTC) | Observation rows | Entries with a row | Rows with reached_level 2 |
|---|---|---|---|
| 2026-10-12 | 1,996 | 1,986 | 1,205 |
| 2026-10-13 | 1,996 | 1,986 | 1,293 |
| 2026-10-14 | 1,990 | 1,980 | 1,283 |
| 2026-10-15 | 1,990 | 1,980 | 1,283 |
| 2026-10-16 | 1,992 | 1,982 | 1,289 |
| 2026-10-17 | 1,988 | 1,978 | 1,289 |
| 2026-10-18 | 1,987 | 1,977 | 1,281 |

## Data

Raw per-observation records are exported weekly as CSV in `scanner_observations/` in this repository. This report is regenerated from the database after each daily run.
