---
name: update-dependencies
description: Safely updates an npm project's dependencies and devDependencies to their latest patch/minor versions, runs npm audit and audit fix, verifies lint, format, type check, build and tests, and writes the results to logs/audit-report.md. Use whenever the user asks to update, upgrade, bump or refresh Node.js/npm packages, check for outdated or vulnerable dependencies, or do routine dependency maintenance, even if they don't list the steps. Also use when they ask for major version upgrades.
license: MIT
compatibility: Requires a shell with Node.js and npm, network access to the npm registry, and write access to the repository.
---

# Update npm dependencies

Update the project's dependencies without introducing breaking changes, then leave a report that a human can act on. You are a careful maintainer: update what is safe, verify everything, and report problems rather than fixing them.

## Before you start

Confirm the project uses npm: the repository root must contain both `package.json` and `package-lock.json`. If either is missing (or a `yarn.lock`, `pnpm-lock.yaml` or `bun.lockb` is present instead), stop and tell the user this skill only supports npm. Running npm in a project managed by another package manager creates a conflicting lockfile.

Things to know while running the commands:

- `npm outdated` exits with code 1 when anything is outdated, and `npm audit` exits non-zero when it finds vulnerabilities. That is expected output, not a failure. Capture the output and continue.
- Get the timestamp in UTC with `date -u`.
- The project name is the `name` field in `package.json`.

## Workflow

Copy this checklist and tick items off as you go:

```
- [ ] 1. npm install
- [ ] 2. npm outdated (before) → report
- [ ] 3. npm audit (before) → report
- [ ] 4. Update patch/minor versions in package.json, npm install
- [ ] 5. npm outdated (after) → report
- [ ] 6. npm audit (after update) → report
- [ ] 7. npm audit fix (only if vulnerabilities remain) → report
- [ ] 8–12. Lint, format, type check, build, test
- [ ] 13–15. Results, errors, and action items → report
- [ ] 16. Final message to the user
```

All report sections go in `logs/audit-report.md` at the repository root, using the templates in [Report template](#report-template). Create the folder and file if they don't exist. If the file already exists, append the new run below the existing content; never overwrite earlier runs.

### 1. Install

Run `npm install` so the installed tree matches the lockfile before anything is compared.

### 2. Record outdated packages

Run `npm outdated` and write the **Outdated dependencies** section.

Classify each package by comparing **Current** to **Latest**:

- **Major**: the major version differs (e.g. `4.2.0 → 5.0.0`). For `0.x` versions, a minor change counts as major (e.g. `0.3.1 → 0.4.0`), because semver treats it as potentially breaking.
- **Patch/minor**: everything else.

Add ` ⚠️` after the name of every package with a major update.

### 3. Record vulnerabilities before updating

Run `npm audit` and append the **npm audit** section with the full output and the one-line summary (e.g. `6 vulnerabilities (3 moderate, 3 high)`, or `found 0 vulnerabilities`).

### 4. Apply patch and minor updates

For each patch/minor package from step 2, set its version in `package.json` to the **Latest** version, keeping the existing range prefix (`^`, `~`, or none). Leave major updates untouched: they can contain breaking API changes that need a human decision. Then run `npm install`.

### 5. Record the result

Run `npm outdated` again and append the **After Update** section. List every package from step 2: the new version for those you updated, `_(skipped)_` for major updates (with ` ⚠️`).

### 6. Re-audit

Run `npm audit` and append another **npm audit** section, titled `(after update)`.

### 7. Fix remaining vulnerabilities

If step 6 still reports vulnerabilities, run `npm audit fix` **without** `--force` (`--force` installs breaking major versions), then run `npm audit` and append the **npm audit (after npm audit fix)** section. If step 6 found none, skip this step.

### 8–12. Verify the project

Look at the `scripts` in `package.json` and the installed devDependencies, then run whichever of these the project has, in this order:

| Step | Check | Typical tools / scripts |
| --- | --- | --- |
| 8 | Linting | ESLint, Biome (`lint`) |
| 9 | Formatting | Prettier, Biome (`format`, or `format:check`) |
| 10 | Type checking | TypeScript, Flow (`typecheck`, `tsc --noEmit`) |
| 11 | Build | Vite, Webpack, Rollup, Parcel, tsc (`build`) |
| 12 | Tests | Jest, Vitest, Mocha (`test`) |

Prefer the project's own npm scripts over invoking tools directly. Mark a check as `N/A` when the project has no tool for it. **Do not fix failures**: record them. The point of this report is to show the human what the update broke.

### 13. Record results

Append the **Lint, format, tests results** table. Each result is `✅ Passed`, `❌ Failed`, `⚠️ Passed with warnings`, or `N/A`.

### 14. Record errors

If anything in steps 1–12 produced errors, append the **Check errors encountered** and/or **Audit / install errors encountered** sections. Omit each section entirely when it has nothing to report.

### 15. Record action items

Append **Still needs action**: skipped major updates, vulnerabilities `npm audit fix` couldn't resolve, failing checks, and deprecation warnings worth following up.

### 16. Tell the user

Summarize briefly: how many packages were updated, how many were skipped as major, the vulnerability count before and after, and which checks failed. Remind them to verify the application still works as expected and to review the changelogs of updated packages for breaking changes.

## Major version updates

Only do this when the user explicitly asks for major updates.

1. Update the requested packages (or all of them, if asked) to their latest major versions in `package.json`, then run `npm install`.
2. Run steps 5–16 again.
3. Append the **After Major Version Updates** section, listing every direct dependency that was updated or removed (patch, minor and major), followed by its audit output, errors and warnings.
4. **Do not fix failing tests or broken builds.** Report them, and remind the user that they need to fix the errors and warnings and check each package's migration guide.

## Report template

Replace `<placeholders>`. Each section is appended in the step that produces it.

````md
## Outdated dependencies - <project-name>

**Date**: <Month> <day>, <year> <hh:mm AM/PM> UTC
**Timestamp**: <ISO 8601 UTC timestamp>

**`npm outdated`**

| Package | Current | Wanted | Latest |
| --- | --- | --- | --- |
| <package-name> | <current> | <wanted> | <latest> |
| <package-name> ⚠️ | <current> | <wanted> | <latest> |

**`npm audit`**

<details>
<summary>Click to view audit report</summary>

```sh
<full-audit-report>
```

</details>

```text
<short-summary>
```

## After Update

**`npm outdated`**

| Package | Old | New |
| --- | --- | --- |
| <package-name> | <old-version> | <new-version> |
| <package-name> ⚠️ | <old-version> | _(skipped)_ |

**`npm audit`** (after update)

<!-- same <details> + summary block as above -->

**`npm audit`** (after `npm audit fix`)

<!-- same <details> + summary block as above -->

## Lint, format, tests results

| Check | Result |
| --- | --- |
| Linting | <result> |
| Formatting | <result> |
| Type Checking | <result> |
| Build | <result> |
| Tests | <result> |

### Check errors encountered

- **Linting**: <summary>
- **Formatting**: <summary>
- **Type Checking**: <summary>
- **Build**: <summary>
- **Tests**: <summary>

### Audit / install errors encountered

- <error>: <description>

### Still needs action

<One-sentence summary.>

- <action-item>

## After Major Version Updates

### Updated / removed direct dependencies

| Package | Old | New |
| --- | --- | --- |
| <package-name> | <old-version> | <new-version or _(removed)_> |

<!-- then the audit, results, errors and action-item sections as above -->
````
