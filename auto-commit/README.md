# Auto Commit - Intelligent Git Commit Automation

## Overview

Auto Commit is a Claude Code plugin that analyzes unstaged git changes and automatically creates well-structured, logically grouped commits with meaningful messages in English (default) or Japanese, following Angular.js commit conventions.

## What It Does

Transforms messy, unorganized changes into clean, atomic commits:
- ✅ Analyzes all unstaged changes intelligently
- ✅ Groups related files logically
- ✅ Generates meaningful commit messages in English (default) or Japanese
- ✅ Follows Angular.js commit guidelines
- ✅ Creates individual commits automatically
- ✅ Verifies each commit succeeds

## Installation

### From Marketplace (Recommended)

```bash
# Add marketplace first (one time only)
/plugin marketplace add https://github.com/mei28/claude-code

# Install plugin
/plugin install auto-commit@mei28/claude-code
```

### From Local Path

```bash
git clone https://github.com/mei28/claude-code
cd claude-code
/plugin install $(pwd)/auto-commit
```

## Usage

Simply invoke when you have unstaged changes:

```
/commit
```

## Example

**Before** (messy unstaged changes):
```
M  src/auth/login.ts
A  src/auth/login.test.ts
M  src/components/LoginForm.tsx
M  docs/AUTH.md
M  package.json
```

**After** (organized commits in English):
```
✅ feat: implement login functionality
   - src/auth/login.ts
   - src/components/LoginForm.tsx

✅ test: add login functionality tests
   - src/auth/login.test.ts

✅ docs: update authentication documentation
   - docs/AUTH.md

✅ chore: update dependencies
   - package.json
```

## Commit Message Prefixes

Follows Angular.js conventions:

| Prefix | Usage | Example (English) | Example (Japanese) |
|--------|-------|-------------------|---------------------|
| `feat` | New feature | `feat: add user authentication` | `feat: ユーザー認証機能を追加` |
| `fix` | Bug fix | `fix: resolve login exception` | `fix: ログイン時の例外処理を修正` |
| `docs` | Documentation | `docs: update API documentation` | `docs: APIドキュメントを更新` |
| `style` | Code formatting | `style: unify indentation` | `style: インデントを統一` |
| `refactor` | Code restructuring | `refactor: extract auth logic` | `refactor: 認証ロジックを分離` |
| `perf` | Performance | `perf: optimize database queries` | `perf: データベースクエリを最適化` |
| `test` | Tests | `test: add registration tests` | `test: ユーザー登録のテストを追加` |
| `chore` | Build/tools | `chore: update package.json` | `chore: package.jsonを更新` |

## Features

### Intelligent Grouping

Groups files based on:
- **Functionality**: Related features together
- **Change Type**: New features, bug fixes, refactoring
- **Dependency**: Files that depend on each other
- **Scope**: Similar module or component

### Meaningful Messages

Generates messages that explain:
- **Why**: The reason for the change
- **What**: The business value
- **How**: The technical approach (when relevant)

**Example (English)**:
```
feat: add user profile retrieval feature

Implement API-based user data fetching with caching.
Introduce 5-minute in-memory cache for performance improvement.
```

**Example (Japanese)**:
```
feat: ユーザープロフィール取得機能を追加

APIからユーザーデータを取得し、キャッシュする機能を実装。
パフォーマンス改善のため、5分間のメモリキャッシュを導入。
```

### Error Handling

Handles common scenarios:
- ✅ Pre-commit hook failures (with suggestions)
- ✅ Merge conflicts (reports to user)
- ✅ Empty changes (friendly message)
- ✅ Sensitive files (warns before committing)

### Task Tracking

Uses TodoWrite to show progress:
```
## Auto-Commit Progress

- [x] Analyze changes (5 files modified)
- [x] Group files into commits
- [x] Commit 1/3: feat: add dark mode feature
- [ ] Commit 2/3: test: add dark mode tests
- [ ] Commit 3/3: docs: update documentation
```

## Best Practices

### When to Use

✅ **Good Use Cases**:
- Multiple unrelated changes accumulated
- After implementing a feature (before PR)
- Cleaning up experimental commits
- Organizing work before code review

❌ **Not Recommended**:
- Single file with clear purpose (just commit manually)
- Mid-development (commit logically as you code)
- Breaking changes (commit carefully with manual messages)

### Workflow Integration

**Recommended Flow**:
```
1. Code your changes
2. Run /deslop to clean up AI-generated code
3. Run /commit to create logical commits
4. Push to remote
5. Create PR
6. Run /pr-template <PR_NUMBER> for PR description
```

## Requirements

- Git repository with unstaged changes
- Claude Code CLI
- Write access to repository

## Configuration

### Project-Specific Conventions

The plugin respects project-specific commit conventions in `CLAUDE.md`:

**English (Default)**:
```markdown
# CLAUDE.md

## Git Workflow

### Commit Convention
- Language: English  # Use English for commit messages (default)
- Prefix: Use Angular.js guidelines
- Include issue numbers: `feat: add feature (#123)`
```

**Japanese (Optional)**:
```markdown
# CLAUDE.md

## Git Workflow

### Commit Convention
- Language: Japanese  # Use Japanese for commit messages
- Include issue numbers: `feat: 機能追加 (#123)`
- Add emoji prefixes: ✨ feat, 🐛 fix, 📝 docs
```

The plugin will automatically adapt to these rules.

## Limitations

- Does not handle merge conflicts (reports to user for manual resolution)
- Does not rewrite history or force push
- Respects pre-commit hooks (fails if hooks reject)
- Requires manual intervention for complex scenarios

## Security

- Never commits sensitive files (.env, credentials, etc.)
- Warns if sensitive patterns detected
- Respects `.gitignore` patterns
- Does not override git config

## License

GPL-3.0

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## Tips

- 💡 Run `/deslop` before `/commit` to ensure code quality
- 💡 Check `git log` after commits to verify messages
- 💡 Use `git commit --amend` to fix the last commit if needed
- 💡 Read project's CLAUDE.md for commit conventions
