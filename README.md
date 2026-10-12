# lowdown-data

Lowdown is a time-series record of the gap between what the official MCP Registry declares and what is actually observed. It records what changed and when. It does not score, grade, or rank servers.

This repository holds the public output of the Lowdown Scanner: a daily summary report and the raw observation records.

## Contents

| Path | What it is | Updated |
|---|---|---|
| [`REPORT.md`](REPORT.md) | Summary of the most recent Scanner run and the last few runs | Regenerated from the database after Scanner runs |
| `scanner_observations/YYYY-MM.csv` | Raw observation records, one file per month (UTC) | Weekly; the last two months are re-exported each time |
| `LICENSE` | CC BY 4.0 | |

## What the Scanner observes

- **Population:** a fixed sample of 2,000 entries (cohort `2026-10-07-v1`) selected once from the official MCP Registry and unchanged since. These are Registry entries, not operators, and they do not represent the whole Registry. Only entries with a `streamable-http` remote are in scope; stdio-only servers are not observed.
- **Requests:** `initialize` and `tools/list` only. The Scanner never calls a tool and does not authenticate.
- **Frequency and location:** once per day, from a single network location (GitHub Actions).
- **Redirects** are not followed. `401` and `403` are recorded as the status observed, not as success or failure.
- **Retries:** probes that fail in a way that may be temporary (timeout, connection refused or reset, HTTP 408, 429, 5xx) are tried once more a few minutes after the run, one request per host at a time. The retry result is added to the same row under `metadata.retry`. The first-attempt columns are never changed. Rows recorded before retries were introduced have no `retry` key.
- **Registry fallback:** on a day when the Registry list cannot be fetched, the Scanner observes the same cohort using the remote URLs from the previous run. Those rows carry `metadata.registry_fallback: true` with `registry_snapshot_run` and `registry_snapshot_at`, and that day's Registry changes are not reflected.

These are single probes. They describe reachability at one moment, not availability or uptime.

## CSV columns

| Column | Meaning |
|---|---|
| `id` | Row id (ascending) |
| `scan_run_id` | One id per Scanner run |
| `node_id` | Id of the observing Scanner node |
| `target_id` | `mcp:` + Registry server name |
| `target_type` | Always `mcp_server` |
| `observed_at` | Time of the first attempt (UTC) |
| `transport` | Remote transport type (`streamable-http`) |
| `http_status` | HTTP status of the last response received; empty if no HTTP response |
| `reached_level` | `0` initialize did not complete, `1` initialize completed and tools/list did not, `2` both completed |
| `latency_ms` | Latency of the initialize request |
| `error_type` | Set only when no HTTP response was received (`timeout`, `dns`, `tls`, `conn_refused`, `conn_reset`, `network_error`), the URL was not called (`blocked_url`), or a 2xx response was not valid JSON-RPC (`invalid_response`) |
| `source` | Always `scanner` |
| `metadata` | JSON with additional facts, listed below |

Common `metadata` keys: `remote_url`, `remote_index`, `registry_version`, `scanner_version`, `cohort_version`, `registry_fallback`, `init_status`, `list_status`, `list_latency_ms`, `list_error_type`, `protocol_version`, `server_version`, `session_id_issued`, `tool_count`, `tools_has_more`, `schema_hash` (tool names and input/output schemas), `desc_hash` (tool names, titles and descriptions), `rpc_error_code`, `www_authenticate`, `www_authenticate_resource_metadata`, and `retry` (`retried_at`, `reached_level`, `http_status`, `error_type`, `latency_ms`, `per_host_concurrency`). Tool descriptions themselves are not stored, only their hash.

## License and citation

The data and `REPORT.md` are licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). You may share and adapt them for any purpose, including commercial use, with attribution.

Suggested attribution:

> Lowdown Scanner data (PetShopBros/lowdown-data), CC BY 4.0, https://github.com/PetShopBros/lowdown-data

## Source

The Scanner code is in [PetShopBros/lowdown-proxy](https://github.com/PetShopBros/lowdown-proxy) (`scanner/`).
