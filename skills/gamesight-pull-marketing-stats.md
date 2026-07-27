---
name: Pull Gamesight marketing analytics
description: Programmatically pull campaign stats, goals, games, and trackers from the Gamesight Reporting API into a data warehouse.
api: openapi/gamesight-reporting-openapi.json
operations: [games, trackers, goal_types, stats-v3, reportinggoals]
---

# Pull marketing analytics from Gamesight

Use the Reporting API at `https://api.marketing.gamesight.io`.

## Auth
Pass a Reporting or Aggregate Reporting scoped API key in the `Authorization` header (distinct from the ingest key). Set `X-Api-Version: 2.0`.

## Steps
1. Discover accessible games with `GET /games` (operation `games`).
2. List trackers with `GET /trackers` (operation `trackers`); pass `limit` to page and `with_names=true` to include names.
3. List goal types with `GET /goal_types` (operation `goal_types`).
4. Query metrics with `POST /stats` (operation `stats-v3`) for campaign/goal analytics.
5. Pull goal-level reporting with `POST /reporting/goals` (operation `reportinggoals`).

## Notes
Aggregate Reporting keys cannot access game analytics or user-level data. Errors return a JSON envelope (`errors/gamesight-problem-types.yml`). Conventions: `conventions/gamesight-conventions.yml`.
