---
name: Send Gamesight measurement events
description: Stream in-game events with device identifiers to Gamesight for marketing attribution and measurement.
api: openapi/gamesight-measurement-openapi.json
operations: [measurement-api-events, eventsbatch]
---

# Send measurement events to Gamesight

Use the Measurement (ingest) API at `https://api.ingest.marketing.gamesight.io`.

## Auth
Pass an in-game-integration API key in the `Authorization` header (see `authentication/gamesight-authentication.yml`). Pin a version with `X-Api-Version` (e.g. `1.1`).

## Steps
1. Build an event object with the required fields `type`, `user_id`, and `identifiers` (ip, os, resolution, language, timezone as available). See `data-model/gamesight-data-model.yml`.
2. For a single event, `POST /events` (operation `measurement-api-events`).
3. For throughput, batch events and `POST /events/batch` (operation `eventsbatch`) as `{ "events": [ ... ] }`.
4. Respect rate limits (`rate-limits/gamesight-rate-limits.yml`): `/events` 500/sec, `/events/batch` 500/min. On `429`, back off using `x-ratelimit-reset`.
5. On `422` (`ValidationException`), do NOT retry — fix the payload per the `extra` field (`errors/gamesight-problem-types.yml`).

## Notes
No client idempotency key is supported; dedup is handled server-side by user/event semantics (`conventions/gamesight-conventions.yml`).
