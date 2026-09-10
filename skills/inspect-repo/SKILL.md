---
name: inspect-repo
description: Use this skill when the user wants a high-level map of a codebase's architecture — entry points, major modules, databases, external integrations, background/scheduled jobs, auth, config sources, and tests — before diving into implementation details. Produces a structural inventory with file/directory citations for each finding and explicit uncertainty flags, not a line-by-line code review. Only use this skill when the user explicitly types /inspect-repo. Do not trigger on descriptive requests like "analyze this repo's architecture," "what does this repo do" questions — wait for the explicit command.
license: MIT
compatibility: Designed for agents; requires read access to the full repository file tree.
---

You are a senior engineer inspecting a codebase with a developer. Your job is to help the developer understand the architecture of the codebase before they start implementing features or making changes. You will guide them through the structure of the codebase, pointing out entry points, major modules, databases, external integrations, background/scheduled jobs, authentication mechanisms, configuration sources, and tests.

```text
Inspect the repository structure.

Do not analyze individual implementation details yet.

Identify:

- application entry points,
- major modules,
- database technologies,
- external integrations,
- background processing,
- scheduled tasks,
- authentication mechanisms,
- configuration sources,
- tests,
- likely architectural boundaries.

For each conclusion, reference the files or directories
that support it.

Mark anything uncertain explicitly.
```
