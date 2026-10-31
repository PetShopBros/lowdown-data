# Lowdown Scanner Report: MCP Registry reachability observations

- **Data as of:** 2026-10-31 01:40 UTC (2026-10-31 10:40 KST), the end of the most recent Scanner run
- **Report generated:** 2026-10-31 01:57 UTC
- **Observation period:** 2026-10-06 to 2026-10-31 (UTC)

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
| Cohort entries with at least one observation row in this run | 9,944 |
| Cohort entries with no observation row in this run | 56 |
| Entries of the earlier cohort `2026-10-07-v1` with at least one observation row (of 2,000) | 1,965 |
| Observation rows in this run (an entry with several remotes has several rows) | 10,075 |
| Rows where the Scanner did not call the URL (blocked by its safety checks) | 3 |
| Probe attempts (observation rows minus rows not called) | 10,072 |

## Reach level of probe attempts

| reached_level | Meaning | Count (of 10,072 probe attempts) |
|---|---|---|
| 2 | initialize and tools/list completed | 5,550 |
| 1 | initialize completed; tools/list did not | 49 |
| 0 | initialize did not complete | 4,473 |

## HTTP status of probe attempts

| HTTP status | Count (of 10,072) |
|---|---|
| 200 | 5,583 |
| 401 | 3,178 |
| no HTTP response | 435 |
| 404 | 274 |
| 302 | 167 |
| 503 | 72 |
| 502 | 57 |
| 402 | 44 |
| 500 | 41 |
| 400 | 28 |
| 530 | 26 |
| 301 | 25 |
| 308 | 25 |
| 403 | 22 |
| 307 | 21 |
| 429 | 21 |
| 405 | 20 |
| 410 | 14 |
| 526 | 5 |
| 421 | 4 |
| 454 | 2 |
| 523 | 2 |
| 525 | 2 |
| 201 | 1 |
| 451 | 1 |
| 501 | 1 |
| 521 | 1 |

## Error types of probe attempts

| error_type | Count (of 10,072) |
|---|---|
| none | 9,619 |
| timeout | 188 |
| dns | 183 |
| tls | 44 |
| conn_reset | 18 |
| invalid_response | 15 |
| conn_refused | 4 |
| network_error | 1 |

## Hosts of probe attempts

A host is the hostname of a remote URL. Several entries can share one host, and one operator can use several hosts, so host counts are not operator counts. Host names are not listed.

| Measure | Value |
|---|---|
| Distinct hosts among probe attempts | 9,226 |
| Distinct hosts with at least one reached_level 2 row | 4,960 |
| Share of probe attempts on the most frequent host | 2.1% |
| Share of probe attempts on the three most frequent hosts | 4.2% |

## Last 7 runs

Totals change when the cohort changes. To compare across the change, use the `2026-10-07-v1` columns, which count only entries of the earlier cohort.

| Run date (UTC) | Cohort | Observation rows | Entries with a row | Rows with reached_level 2 | `2026-10-07-v1` entries with a row | `2026-10-07-v1` rows with reached_level 2 |
|---|---|---|---|---|---|---|
| 2026-10-25 | `2026-10-19-v2` | 5,017 | 4,959 | 2,976 | 1,968 | 1,274 |
| 2026-10-26 | `2026-10-19-v2` | 5,015 | 4,957 | 2,962 | 1,968 | 1,267 |
| 2026-10-27 | `2026-10-19-v2` | 5,013 | 4,955 | 2,965 | 1,968 | 1,269 |
| 2026-10-28 | `2026-10-19-v2` | 5,011 | 4,953 | 2,894 | 1,967 | 1,255 |
| 2026-10-29 | `2026-10-29-v3` | 10,081 | 9,951 | 5,655 | 1,966 | 1,250 |
| 2026-10-30 | `2026-10-29-v3` | 10,080 | 9,949 | 5,634 | 1,966 | 1,244 |
| 2026-10-31 | `2026-10-29-v3` | 10,075 | 9,944 | 5,550 | 1,965 | 1,235 |

## Data

Raw per-observation records are exported weekly as CSV in `scanner_observations/` in this repository. This report is regenerated from the database after each daily run.
