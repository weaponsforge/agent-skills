---
name: good-commit
description: Drafts a short commit message summarizing the code changes made during the current session. Always trigger when the user asks to "draft a commit", "write a commit message for this session", "commit this", "summarize these changes as a commit", or similar phrasing — even if they don't explicitly say "git commit" or name this skill. Outputs a conventional-commit subject line and a bulleted body itemizing each important update, with the entire message written in lowercase.
license: MIT
compatibility: Designed for agents, but can be used in any context where a commit message is needed.
---

# Good Commit

Session commit drafter that turns the code changes made during the current session into a single git-style commit message the user can paste straight into `git commit -m`.

## Gathering what actually changed

A commit message is only useful if it's accurate, so ground it in the real changes rather than a plausible-sounding guess:

- If the user has already written a commit message, check it for accuracy and completeness.
- If there's a chat session or history of edits, review it to see what the user actually changed and why.
- If there's an accessible git repository, run `git status` and `git diff` (or `git diff --staged` if things are staged) to see exactly what changed. This is the most reliable source — prefer it over relying on memory of the conversation.
- If there's no repo to inspect, reconstruct the change set from the session itself: files created or edited via tools, code blocks the user asked to change, and what each change was for.
- If the picture is still incomplete (e.g. changes happened outside this session, or the diff is too large to summarize confidently), ask the user briefly what to include rather than inventing specifics.

## Message format

Follow the [Conventional Commits](./references/conventional-commits.md) format, with a subject line and a bulleted body:

```
<prefix>: <one-line summary of the overall change, imperative mood>

- <short bullet for one important update>
- <short bullet for another important update>
- <...>
```

- The subject line always starts with a conventional commit `<prefix>:` (lowercase, one space after the colon).
- Each bullet covers one distinct, important update — not every micro-edit. Roll minor related tweaks (formatting, unused-import cleanup, typo fixes) into a single bullet rather than listing each one separately.
- Keep bullets short and lead with a verb: added, fixed, refactored, removed, wired up, etc.
- Write the whole message — subject and every bullet — in lowercase, including proper nouns and acronyms (e.g. "wire up openai api", not "Wire up OpenAI API").
- Order bullets by importance, most significant change first.
- Only skip the bulleted body if there is genuinely just one change to report; otherwise always itemize.

## Example

Session changes: added a login form component, wired it to the auth API, fixed a bug where the submit button stayed disabled after a failed request, and removed some unused imports.

Output:

```
feat: add login form and connect to auth api

- add login form component with email/password fields
- wire form submission to the auth api
- fix submit button staying disabled after a failed login attempt
- remove unused imports
```

## Delivering the result

Present the message in a single fenced code block so it can be copied directly. Don't add commentary or an explanation of the changes unless the user asks for one.