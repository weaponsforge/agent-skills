## agent-skills

Handy collection of agent SKILLS.

### 🟢 [`/good-commit`](./skills/good-commit/SKILL.md)

Drafts a short commit message summarizing the code changes made during the current session. Always trigger when the user asks to "draft a commit", "write a commit message for this session", "commit this", "summarize these changes as a commit", or similar phrasing — even if they don't explicitly say "git commit" or name this skill. Outputs a conventional-commit subject line and a bulleted body itemizing each important update, with the entire message written in lowercase.

Install with:

```sh
npx skills add https://github.com/weaponsforge/agent-skills --skill good-commit
```

### 🟢 [`/inspect-repo`](./skills/inspect-repo/SKILL.md)

Use this skill when the user wants a high-level map of a codebase's architecture — entry points, major modules, databases, external integrations, background/scheduled jobs, auth, config sources, and tests — before diving into implementation details. Produces a structural inventory with file/directory citations for each finding and explicit uncertainty flags, not a line-by-line code review. Only use this skill when the user explicitly types /inspect-repo. Do not trigger on descriptive requests like "analyze this repo's architecture," "what does this repo do" questions — wait for the explicit command.

Install with:

```sh
npx skills add https://github.com/weaponsforge/agent-skills --skill inspect-repo
```


@weaponsforge<br>
20260906


