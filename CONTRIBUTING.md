# Contributing to Then.Run

💡 Thanks for taking the time to contribute!  
All contributions - whether they're bug reports, documentation fixes, new features, or design tweaks - are welcome and appreciated.

> **Note**  
> This guide applies to _all_ repositories under the **Then.Run** organization unless a specific repo ships its own `CONTRIBUTING.md` with additional rules.

---

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [How to Get Started](#how-to-get-started)
  - [Prerequisites](#prerequisites)
  - [Fork & Clone](#fork--clone)
  - [Set Up Your Development Environment](#set-up-your-development-environment)
- [Branching & Commit Guidelines](#branching--commit-guidelines)
- [Issue Reporting](#issue-reporting)
- [Pull Request Workflow](#pull-request-workflow)
- [Style & Formatting](#style--formatting)
- [Testing](#testing)
- [Documentation](#documentation)
- [License & CLA](#license--cla)
- [Getting Help / Community](#getting-help--community)
- [Thank You!](#thank-you)

---

## Code of Conduct

All contributors are expected to follow our [Code of Conduct](CODE_OF_CONDUCT.md).  
Please read it before interacting with the community.

---

## How to Get Started

### Prerequisites

| Tool                                                 | Minimum Version | Why?                      |
| ---------------------------------------------------- | --------------- | ------------------------- |
| **Git**                                              | 2.30+           | Version control           |
| **Node.js** (if the repo uses JavaScript/TypeScript) | 24.x            | Runtime & package manager |
| **Docker**                                           | 20.10+          | Containerised workflows   |
| **Other language runtimes**                          | —               | Add as needed per repo    |

> 👉 **Tip** - We recommend using a version manager (`nvm`, `pyenv`, etc.) to keep the required versions isolated.

### Fork & Clone

1. **Fork** the repository on GitHub (click the "Fork" button at the top‑right).
2. Clone your fork locally:

   ```bash
   git clone https://github.com/<YOUR_USERNAME>/<repo-name>.git
   cd <repo-name>
   ```

3. Add the upstream remote to keep your fork in sync:

   ```bash
   git remote add upstream https://github.com/Then-Run/<repo-name>.git
   ```

### Set Up Your Development Environment

#### Node / JavaScript / TypeScript repos

```bash
# Install dependencies
npm ci   # or `yarn install` / `pnpm i` if the repo prefers another package manager
# Run the build (if applicable)
npm run build
# Run lint / format checks
npm run lint
npm run format:check
```

#### Python repos

```bash
python -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

#### Docker‑based projects

```bash
docker compose up --build
```

> **If your repository uses a different stack**, replace the commands above with the appropriate ones and update this section accordingly.

---

## Branching & Commit Guidelines

| Type              | Branch name example    | Description                               |
| ----------------- | ---------------------- | ----------------------------------------- |
| **Feature**       | `feat/add-graphql-api` | New functionality                         |
| **Bug fix**       | `fix/login-button`     | Correcting a defect                       |
| **Documentation** | `docs/update-readme`   | Docs only                                 |
| **Refactor**      | `refactor/auth-module` | Code restructuring (no functional change) |
| **Chore**         | `chore/upgrade-deps`   | Tooling, CI, or dependency updates        |

### Commit Message Format (Conventional Commits)

```
<type>(<scope>): <subject>

<body (optional)>

<footer (optional)>
```

_Examples_

```
feat(auth): add JWT refresh token flow

The new endpoint allows clients to obtain a fresh access token
without re‑authenticating.

Closes #42
```

```bash
# Quick helper (optional)
npx commitizen init cz-conventional-changelog --save-dev --save-exact
```

---

## Issue Reporting

Before opening a new issue, please:

1. **Search** existing issues (open & closed) - your problem may already be addressed.
2. Check the **Roadmap** (see the repo's README) to see if the feature is planned.

### Bug Report Template

```markdown
**Title:** Short, descriptive title (e.g., "Crash when uploading a .csv file")

**Environment**

- OS: (e.g., macOS 13.5, Windows 11)
- Node.js version: (if applicable)
- Browser: (if relevant)
- Other relevant tools/versions:

**Steps to Reproduce**

1. ...
2. ...
3. ...

**Expected behavior**
A clear description of what you expected to happen.

**Actual behavior**
What actually happened (include error messages, screenshots, logs).

**Additional context**
Anything else that might help us diagnose the problem.
```

### Feature Request Template

```markdown
**Title:** Short, descriptive title (e.g., "Add support for SVG avatars")

**Motivation**
Why is this useful? Who benefits?

**Proposed solution**
Outline the intended implementation (high‑level is fine).

**Alternatives considered**
Any other approaches you thought about.

**Additional context**
Links to related issues, designs, or references.
```

---

## Pull Request Workflow

1. **Create a branch** from `main` (or the target base branch) following the naming conventions above.
2. **Make your changes** - keep them focused on a single purpose.
3. **Run the test suite** locally (see the **Testing** section).
4. **Commit** using the conventional‑commit format.
5. **Push** the branch to your fork:

   ```bash
   git push origin <branch-name>
   ```

6. **Open a Pull Request** on GitHub:

   - Target: `Then-Run/<repo-name>:main`
   - Title: Use the same subject line as your commit (or a concise summary).
   - Description:
     - Briefly explain the problem being solved.
     - Reference any related issues (e.g., `Closes #123`).
     - Mention any manual testing steps you performed.

7. **CI will run automatically** (lint, tests, build).
   - If the CI fails, fix the issues locally and push new commits - the PR will update automatically.
8. **Review** - A maintainer will review your PR, possibly requesting changes.
   - Once approved, the PR will be merged with a **squash‑merge** (preserving a clean commit history).

### Keeping Your Fork Up‑to‑Date

```bash
git fetch upstream
git checkout main
git merge upstream/main   # or `git rebase upstream/main`
git push origin main
```

---

## Style & Formatting

| Language / Tool             | Style Guide                                               | Linter / Formatter    |
| --------------------------- | --------------------------------------------------------- | --------------------- |
| **JavaScript / TypeScript** | Airbnb + TypeScript                                       | `eslint` + `prettier` |
| **Python**                  | PEP 8                                                     | `flake8` + `black`    |
| **CSS / SCSS**              | Standard CSS conventions                                  | `stylelint`           |
| **Markdown**                | Write clear, concise prose; use proper heading hierarchy. | `markdownlint`        |

_All repos ship a pre‑commit hook that runs the appropriate linters/formatters. Install it with:_

```bash
# Node repos
npm run prepare   # runs `husky install`

# Python repos
pre-commit install
```

If you're unsure about a style rule, just follow the existing codebase - consistency matters more than perfection.

---

## Testing

- **Run the full test suite** before submitting a PR.

  ```bash
  # Node / JS
  npm test

  # Python
  pytest
  ```

- **Write tests** for any new functionality or bug fix.

  - Aim for **unit tests** that cover edge cases.
  - Add **integration tests** if the change touches multiple components.
  - Follow the repo's existing testing conventions (e.g., Jest, Mocha, PyTest).

- **Coverage**: Keep the overall coverage above the repository's threshold (usually ≥ 80%).
  CI will fail if the coverage drops below the required level.

---

## Documentation

- **Update docs** (README, inline JSDoc/Python docstrings, API reference, etc.) whenever you modify public behavior.
- If the repo uses a static site generator (e.g., Docusaurus, MkDocs), run the build locally to verify the docs render correctly:

  ```bash
  # Example for Docusaurus
  npm run docs:build
  ```

- For UI changes, include **screenshots** or **GIFs** in the PR description.

---

## License & CLA

- The project is licensed under the **MIT License** (see `LICENSE`).
- By submitting a pull request, you agree to license your contribution under the same terms.
- If the organization adopts a Contributor License Agreement (CLA) in the future, you'll be prompted to sign it via the **CLA Assistant** bot.

---

## Getting Help / Community

- **GitHub Discussions** - ideal for brainstorming, design discussions, or "how‑to" questions.
- **Discord / Slack** - we'll announce the invite link when the community channels are live.
- **Email** - `hello@then.run` for direct queries or to report abuse.

If you're stuck, feel free to ping a maintainer or open a "question" issue - we'll get back to you as soon as possible.

---

## Thank You!

Your contributions make Then.Run better for everyone.
We appreciate the time, effort, and thought you put into improving the project. 🎉

Happy coding! 🚀

---
