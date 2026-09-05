## agent-skills

Handy collection of agent SKILLS.

#### `/good-commit`

Drafts a short commit message summarizing the code changes made during the current session. Always trigger when the user asks to "draft a commit", "write a commit message for this session", "commit this", "summarize these changes as a commit", or similar phrasing — even if they don't explicitly say "git commit" or name this skill. Outputs a conventional-commit subject line and a bulleted body itemizing each important update, with the entire message written in lowercase.

Install with:

```sh
npx skills add https://github.com/weaponsforge/agent-skills --skill good-commit
```

@weaponsforge<br>
20260906


