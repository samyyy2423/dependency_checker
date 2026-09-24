# 📦 Dependency Checker

A lightweight TypeScript CLI that keeps a project's npm dependencies up to date and secure. It lists
outdated packages, runs `npm audit`, can apply fixes, and writes JSON and Markdown reports. Works on a
single project or a monorepo (`packages/*/`).

## Installation

```bash
npm install --save-dev ts-node typescript @types/node
```

## Usage

```bash
ts-node dependency-checker.ts                  # 🔍 check outdated packages and vulnerabilities
ts-node dependency-checker.ts --fix            # 🛠️ npm audit fix (safe fixes only)
ts-node dependency-checker.ts --fix --force    # 💥 npm audit fix --force (may install breaking changes)
```

## Output

- ✅ Console summary per project
- 📄 `dependency-report.json`: machine-readable
- 📝 `dependency-report.md`: human-readable, ready for a PR comment or Slack

Example Markdown entry:

```markdown
### api-service
- Path: packages/api
- Outdated: 2
- Vulnerabilities: Critical=0, High=1, Moderate=3, Low=5
- AutoFix: ✅ Applied
```

## Precautions

- Review changes after an auto-fix with `git diff`.
- `--force` can install breaking major versions; test thoroughly afterwards.
- Monorepo discovery only looks at `packages/*/`; extend the script for other layouts.
- This is a helper, not a replacement for Dependabot, Renovate or Snyk.

## Suggested use

- Run it before every release.
- Add it to CI and fail the build on critical or high vulnerabilities.
- Share the Markdown report with the team.
