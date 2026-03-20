---
name: user-layer
description: Use this skill when the user wants a UserLayer report for an App Store or Google Play app, including preview, full analysis, polling, and follow-up questions grounded in real reviews. Trigger it for competitor review analysis, user pain point extraction, segment discovery, and opportunity validation tasks.
---

# UserLayer

UserLayer turns App Store and Google Play reviews into structured research outputs:

- pain points
- user segments
- market opportunities
- follow-up answers grounded in cited reviews

Use the bundled wrappers in `scripts/main.py`. Do not hand-roll raw HTTP requests when this skill is available.

## Use This Skill When

- The user gives you an App Store or Google Play URL and wants review-backed insights.
- The user wants a lighter preview before paying for a full report.
- The user wants to ask follow-up questions about a completed full analysis.

## Prerequisites

- `API_KEY` must be set to a valid UserLayer API key.
- `LAUNCHBASE_API_URL` is optional.
  Default: `https://lb-api.workflowhunt.com`

## Available Wrappers

- `preview(app_url: str, max_reviews: int | None = None)`
- `analyze(app_url: str, max_reviews: int | None = None)`
- `check_status(analysis_id: str)`
- `query(pain_point_id: str, question: str)`

## Operating Rules

- Default review count is `100` latest reviews.
- `preview()` supports up to `500` latest reviews when explicitly requested.
- `analyze()` is asynchronous and returns an `analysis_id`; poll with `check_status()`.
- Use `query()` only after a completed full analysis returns a valid `pain_point_id`.
- Treat `sources` and cited review evidence as the source of truth.
- If `DATA_INDEX_NOT_FOUND` is returned, rerun a full analysis before querying again.
