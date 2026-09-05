## Conventional Commits

### Structure

A commit message should be structured as follows:

```sh
<type>[optional scope]: <description>

[optional body]

[optional footer]
```

### Structural Elements

The commit contains the following structural elements, to communicate intent:

| Commit Type | Description |
| --- | --- |
| `fix:` | A commit of the type fix patches a bug in your codebase |
| `feat:` | A commit of the type feat introduces a new feature to the codebase |
| `BREAKING CHANGE:` | A commit that has the text BREAKING CHANGE: at the beginning of its optional body or footer section introduces a breaking API change. A breaking change can be part of either a `fix:` or `feat:` type commit. |

A scope may be provided to a commit’s type, to provide additional contextual information and is contained within parenthesis, e.g., `feat(parser): adds ability to parse arrays`.

### Other Commit Types

Commit types other than `fix:` and `feat:` are allowed, for example the Angular convention recommends `docs:`, `style:`, `refactor:`, `perf:`, `test:`, `chore:`

| Commit Type | Description |
| --- | --- |
| `chore:` | Maintenance tasks that don't modify src or test files |
| `docs:` | For code or repository documentation-only changes |
| `refactor:` | For massive structural or functional changes |
| `perf:` | For performance and optimizations |
| `test:` | Adding or correcting tests  |
| `build:` | Changes to build system or external dependencies |
| `ci:` | Changes to CI configuration files and scripts |
| `style:` | Code style changes (formatting, whitespace, etc.) |
| `ops:` | Infrastructure, deployment, backup, recovery operations |
| `revert:` | Reverts a previous commit |


### Specification

The key words “MUST”, “MUST NOT”, “REQUIRED”, “SHALL”, “SHALL NOT”, “SHOULD”, “SHOULD NOT”, “RECOMMENDED”, “MAY”, and “OPTIONAL” in this document are to be interpreted as described in RFC 2119.

1. commits MUST be prefixed with a type, which consists of a noun, `feat`, `fix`, etc., followed by a colon and a space.

2. the type `feat` MUST be used when a commit adds a new feature to your application or library.

3. the type `fix` MUST be used when a commit represents a bug fix for your application.

4. an optional scope MAY be provided after a type. A scope is a phrase describing a section of the codebase enclosed in parenthesis, e.g., `fix(parser):`

5. A description MUST immediately follow the type/scope prefix. The description is a short description of the pull request, e.g., _fix: array parsing issue when multiple spaces were contained in string._

6. A longer commit body MAY be provided after the short description. The body MUST begin one blank line after the description.

7. A footer MAY be provided one blank line after the body. The footer SHOULD contain additional meta-information about the pull-request (such as the issues it fixes, e.g., `fixes #13, #5`).

8. Breaking changes MUST be indicated at the very beginning of the footer or body section of a commit. A breaking change MUST consist of the uppercase text `BREAKING CHANGE`, followed by a colon and a space.

9. A description MUST be provided after the `BREAKING CHANGE:`, describing what has changed about the API, e.g., BREAKING
CHANGE: environment variables now take precedence over config files.

10. types other than `feat` and `fix` MAY be used in your commit messages.

Source: https://www.conventionalcommits.org/en/v1.0.0-beta/#summary