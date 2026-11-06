# Lowdown Scanner Report: MCP Registry reachability observations

- **Data as of:** 2026-11-06 01:40 UTC (2026-11-06 10:40 KST), the end of the most recent Scanner run
- **Report generated:** 2026-11-06 01:51 UTC
- **Observation period:** 2026-10-06 to 2026-11-06 (UTC)

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
| Cohort entries with at least one observation row in this run | 9,925 |
| Cohort entries with no observation row in this run | 75 |
| Entries of the earlier cohort `2026-10-07-v1` with at least one observation row (of 2,000) | 1,965 |
| Observation rows in this run (an entry with several remotes has several rows) | 10,058 |
| Rows where the Scanner did not call the URL (blocked by its safety checks) | 4 |
| Probe attempts (observation rows minus rows not called) | 10,054 |

## Reach level of probe attempts

| reached_level | Meaning | Count (of 10,054 probe attempts) |
|---|---|---|
| 2 | initialize and tools/list completed | 5,556 |
| 1 | initialize completed; tools/list did not | 53 |
| 0 | initialize did not complete | 4,445 |

## HTTP status of probe attempts

| HTTP status | Count (of 10,054) |
|---|---|
| 200 | 5,593 |
| 401 | 3,201 |
| no HTTP response | 373 |
| 404 | 296 |
| 302 | 167 |
| 502 | 61 |
| 503 | 57 |
| 402 | 42 |
| 500 | 34 |
| 301 | 29 |
| 400 | 29 |
| 308 | 25 |
| 403 | 25 |
| 429 | 24 |
| 307 | 23 |
| 530 | 23 |
| 405 | 22 |
| 410 | 11 |
| 526 | 5 |
| 421 | 4 |
| 521 | 2 |
| 522 | 2 |
| 525 | 2 |
| 201 | 1 |
| 451 | 1 |
| 501 | 1 |
| 523 | 1 |

## Error types of probe attempts

| error_type | Count (of 10,054) |
|---|---|
| none | 9,658 |
| dns | 194 |
| timeout | 105 |
| tls | 52 |
| conn_reset | 23 |
| invalid_response | 14 |
| conn_refused | 7 |
| network_error | 1 |

## Hosts of probe attempts

A host is the hostname of a remote URL. Several entries can share one host, and one operator can use several hosts, so host counts are not operator counts. Host names are not listed.

| Measure | Value |
|---|---|
| Distinct hosts among probe attempts | 9,204 |
| Distinct hosts with at least one reached_level 2 row | 4,971 |
| Share of probe attempts on the most frequent host | 2.1% |
| Share of probe attempts on the three most frequent hosts | 4.2% |

## Last 7 runs

Totals change when the cohort changes. To compare across the change, use the `2026-10-07-v1` columns, which count only entries of the earlier cohort.

| Run date (UTC) | Cohort | Observation rows | Entries with a row | Rows with reached_level 2 | `2026-10-07-v1` entries with a row | `2026-10-07-v1` rows with reached_level 2 |
|---|---|---|---|---|---|---|
| 2026-10-31 | `2026-10-29-v3` | 10,075 | 9,944 | 5,550 | 1,965 | 1,235 |
| 2026-11-01 | `2026-10-29-v3` | 10,069 | 9,938 | 5,637 | 1,964 | 1,240 |
| 2026-11-02 | `2026-10-29-v3` | 10,064 | 9,933 | 5,570 | 1,962 | 1,229 |
| 2026-11-03 | `2026-10-29-v3` | 10,063 | 9,932 | 5,584 | 1,965 | 1,232 |
| 2026-11-04 | `2026-10-29-v3` | 10,060 | 9,928 | 5,518 | 1,965 | 1,228 |
| 2026-11-05 | `2026-10-29-v3` | 10,058 | 9,926 | 5,573 | 1,965 | 1,234 |
| 2026-11-06 | `2026-10-29-v3` | 10,058 | 9,925 | 5,556 | 1,965 | 1,226 |

## Data

Raw per-observation records are exported weekly as CSV in `scanner_observations/` in this repository. This report is regenerated from the database after each daily run.
