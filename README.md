## agent-skills

Handy collection of agent SKILLS.

### 🟢 [`/good-commit`](./skills/good-commit/SKILL.md)

Drafts a short commit message summarizing the code changes made during the current session. Always trigger when the user asks to "draft a commit", "write a commit message for this session", "commit this", "summarize these changes as a commit", or similar phrasing — even if they don't explicitly say "git commit" or name this skill. Outputs a conventional-commit subject line and a bulleted body itemizing each important update, with the entire message written in lowercase.

Install with:

```sh
npx skills add https://github.com/weaponsforge/agent-skills --skill good-commit
```

### 🔎 [`/inspect-repo`](./skills/inspect-repo/SKILL.md)

Use this skill when the user wants a high-level map of a codebase's architecture — entry points, major modules, databases, external integrations, background/scheduled jobs, auth, config sources, and tests — before diving into implementation details. Produces a structural inventory with file/directory citations for each finding and explicit uncertainty flags, not a line-by-line code review. Only use this skill when the user explicitly types `/inspect-repo`. Do not trigger on descriptive requests like "analyze this repo's architecture," "what does this repo do" questions — wait for the explicit command.

Install with:

```sh
npx skills add https://github.com/weaponsforge/agent-skills --skill inspect-repo
```

### 🔎 [`/inspect-function`](./skills/inspect-function/SKILL.md)

Use this skill when the user wants to understand the purpose and behavior of a specific function in the codebase — its inputs, outputs, side effects, and any dependencies or related functions that are relevant to understanding its role within the codebase. Only use this skill when the user explicitly types `/inspect-function <function_name> [in <file_path>]` where `<file_path>` is the **optional path to the file** containing the function. Do not trigger on descriptive requests like "analyze this function," "what does this function do" questions — wait for the explicit command.

Install with:

```sh
npx skills add https://github.com/weaponsforge/agent-skills --skill inspect-function
```

<br>

## References

- [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/)
- [How to Understand a Legacy Codebase Using AI Before Changing it](https://www.freecodecamp.org/news/understand-a-legacy-codebase-with-ai/)


@weaponsforge<br>
20260906


