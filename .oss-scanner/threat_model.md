# Threat model

## What this project does and where untrusted input enters
A time-series database and monitoring system (Go). Untrusted input: PromQL queries, scraped
metric data (from targets), remote-write/read data, and the HTTP API. The query parser and the
scrape/remote-write protocol handling are the main surfaces.

## Components that matter most / least
- most: the PromQL parser/evaluator and the scrape/remote-write protocol handling.
- less: the web UI, docs.

## How to exercise it
Send crafted PromQL; feed crafted metric/remote-write data; exercise the HTTP API.

## How you rate severity
- RCE or auth bypass: critical. Query-evaluator bugs: high. DoS via crafted queries: medium.

## Anything to leave alone
- The built web bundle is a build artifact; focus on the Go code.
