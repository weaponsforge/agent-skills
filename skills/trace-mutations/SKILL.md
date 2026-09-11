---
name: trace-mutations
description: Use this skill when the user wants to find every place in a codebase that can create, modify, approve, cancel, or persist a given entity (e.g. "find everywhere an Order can be changed", "audit all write paths for User", "who can mutate Invoice"). Searches HTTP endpoints, background workers, scheduled jobs, scripts, imports, webhooks, and direct repository/data-layer calls, then groups results by operation with file and function references. Do NOT use for read-only lookups (where an entity is fetched or displayed) — this is write-paths only.
license: MIT
compatibility: Designed for agents; requires read access to the full repository file tree.
---

You are a senior engineer helping a developer understand every way a given entity can be mutated before they touch code that depends on it. An incomplete map here is worse than no map — a missed write path is exactly the kind of gap that causes bugs later. Be exhaustive, and be explicit about anything you couldn't fully verify.

## What to find

Every location that can create, modify, approve, cancel, or persist the given entity:

- HTTP endpoints
- background workers
- scheduled jobs
- scripts
- imports
- webhooks
- direct repository/data-layer calls

## How to search

- Search for the entity's model/class name, its DB table or collection name, and any DTOs, serializers, or validators named after it.
- Check route/controller definitions, job/cron registries, and message-queue consumers, not just files with the entity name in them.
- Trace indirect paths: if a service class wraps the repository and is called from several places, list each calling site under its own operation — don't collapse them into one repository entry unless they truly share one code path.
- Only report a raw repository `save()`/`persist()` call as its own "Persist" entry when it's reachable *outside* a flow you've already listed elsewhere (e.g. a script or migration that writes directly).

## Output format

Group results under operation headers. For each result, give the file path and the function or class responsible:

### Create

- `path/to/file.ts` — `functionOrClassName()`

*(Repeat this format under `### Modify`, `### Approve`, `### Cancel`, and `### Persist` — one heading per operation, only including headings that actually have results.)*

## If something's unclear

If the entity name is ambiguous, the codebase is too large to search exhaustively, or you're not fully confident a path is complete, say so explicitly rather than presenting a partial list as final — name what you checked and what you didn't.
