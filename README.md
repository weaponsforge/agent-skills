## agent-skills

Handy collection of agent SKILLS.

### 🟢 [`/good-commit`](./skills/good-commit/SKILL.md)

Only invoke this skill when the user explicitly types `/good-commit`. Do not trigger on descriptive requests like "draft a commit", "write a commit message for this session", "commit this", or "summarize these changes as a commit," or similar phrasing — those should be handled directly, not routed to this skill. When invoked, drafts a short commit message summarizing the code changes made during the current session. Outputs a conventional-commit subject line and a bulleted body itemizing each important update, with the entire message written in lowercase.

Install with:

```sh
npx skills add https://github.com/weaponsforge/agent-skills --skill good-commit
```

### 🔎 [`/inspect-repo`](./skills/inspect-repo/SKILL.md)

Provides a high-level map of a codebase's architecture — entry points, major modules, databases, external integrations, background/scheduled jobs, auth, config sources, and tests — before diving into implementation details. Produces a structural inventory with file/directory citations for each finding and explicit uncertainty flags, not a line-by-line code review.

Install with:

```sh
npx skills add https://github.com/weaponsforge/agent-skills --skill inspect-repo
```

### 🔎 [`/inspect-function`](./skills/inspect-function/SKILL.md)

Use this skill when the user wants to understand the purpose and behavior of a specific function in the codebase — its inputs, outputs, side effects, and any dependencies or related functions that are relevant to understanding its role within the codebase, or when the user explicitly types `/inspect-function <function_name> [in <file_path>]` where `<file_path>` is the **optional path to the file** containing the function.

Install with:

```sh
npx skills add https://github.com/weaponsforge/agent-skills --skill inspect-function
```

### 🔎 [`/inspect-modules`](./skills/inspect-modules/SKILL.md)

Helps a user understand the dependencies between modules in a codebase. The skill will provide a high-level overview of how different modules interact with each other, including any direct or indirect dependencies.

Install with:

```sh
npx skills add https://github.com/weaponsforge/agent-skills --skill inspect-modules
```

### 🔎 [`/trace-mutations`](./skills/trace-mutations/SKILL.md)

Finds every place in the codebase that creates, modifies, approves, cancels, or persists a given entity — HTTP endpoints, background workers, scheduled jobs, scripts, imports, webhooks, and direct repository calls. Groups results by operation, with file path and function/class for each. Use when asked to map, audit, or trace all write-paths / mutation points for an entity (e.g. "find everywhere Order can be changed").

Install with:

```sh
npx skills add https://github.com/weaponsforge/agent-skills --skill trace-mutations
```

<br>

## References

- [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/)
- [How to Understand a Legacy Codebase Using AI Before Changing it](https://www.freecodecamp.org/news/understand-a-legacy-codebase-with-ai/)

@weaponsforge<br>
20260906


