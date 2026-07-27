---
name: Handle a Gamesight GDPR/CCPA request
description: Honor a data-subject right-to-forget or opt-out request using Gamesight's GDPR-scoped API.
api: openapi/gamesight-reporting-openapi.json
operations: [reportingusersremove, do_not_track, get_do_not_track]
---

# Handle a GDPR / CCPA data request

## Auth
Use a **GDPR**-scoped API key in the `Authorization` header.

## Steps
1. To erase a user's data (right-to-forget), call `DELETE /reporting/users/remove` (operation `reportingusersremove`) on the Reporting API (`https://api.marketing.gamesight.io`).
2. To set a game-wide opt-out / do-not-track state, call `PUT /games/{game_id}/do_not_track` (operation `do_not_track`) on the Measurement API (`https://api.ingest.marketing.gamesight.io`).
3. To verify current do-not-track state, call `GET /games/{game_id}/do_not_track` (operation `get_do_not_track`).

## Notes
GDPR-scoped keys support Data Access, Right-to-Forget, and Opt-Out operations only. See `authentication/gamesight-authentication.yml` and `conformance/gamesight-conformance.yml` (GDPR/CCPA).
