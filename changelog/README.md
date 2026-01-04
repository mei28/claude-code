# Changelog - Automated Release Notes Generator Plugin

## Overview

Changelog is a Claude Code plugin that automatically generates and maintains CHANGELOG.md from git commit history. It follows [Keep a Changelog](https://keepachangelog.com/) format with semantic versioning, categorizing commits into Added, Changed, Fixed, Deprecated, Removed, and Security sections for user-friendly release notes.

## What It Does

This plugin transforms raw git history into structured release notes:

- **Automatic Categorization**: Groups commits by type (Added, Changed, Fixed, etc.)
- **Semantic Versioning**: Suggests version bumps based on change types
- **Keep a Changelog Format**: Follows industry-standard changelog structure
- **Breaking Change Detection**: Highlights breaking changes prominently
- **Commit Filtering**: Excludes non-user-facing changes (docs, tests, chores)
- **Links Generation**: Adds links to commits, issues, and PRs

## Installation

### From Marketplace (Recommended)

```bash
# Add marketplace first (one time only)
/plugin marketplace add https://github.com/mei28/claude-code

# Install plugin
/plugin install changelog@mei28/claude-code
```

### From Local Path

```bash
git clone https://github.com/mei28/claude-code
cd claude-code
/plugin install $(pwd)/changelog
```

## Usage

Generate changelog from last tag to HEAD:
```
/changelog
```

Generate changelog for specific version:
```
/changelog --version 2.1.0
```

Generate from specific tag:
```
/changelog --since v2.0.0
```

Preview without writing:
```
/changelog --preview
```

The plugin will:
1. Detect current version from git tags
2. Get commit history since last release
3. Categorize commits by type
4. Suggest appropriate version bump
5. Generate formatted changelog entry
6. Update CHANGELOG.md

## Example

**Raw Git History**:
```bash
$ git log --oneline v2.0.0..HEAD

a1b2c3d feat: add OAuth 2.0 authentication
e4f5g6h fix: memory leak in WebSocket connection
i7j8k9l feat: implement dark mode
m0n1o2p refactor: improve database query performance
q3r4s5t fix: timezone handling in date picker
u6v7w8x feat: email notification system
```

**Generated Changelog**:
```markdown
## [2.1.0] - 2024-01-15

### Added
- OAuth 2.0 authentication ([a1b2c3d](https://github.com/user/repo/commit/a1b2c3d))
- Dark mode support ([i7j8k9l](https://github.com/user/repo/commit/i7j8k9l))
- Email notification system ([u6v7w8x](https://github.com/user/repo/commit/u6v7w8x))

### Changed
- Improved database query performance ([m0n1o2p](https://github.com/user/repo/commit/m0n1o2p))

### Fixed
- Memory leak in WebSocket connection ([e4f5g6h](https://github.com/user/repo/commit/e4f5g6h))
- Timezone handling in date picker ([q3r4s5t](https://github.com/user/repo/commit/q3r4s5t))

[2.1.0]: https://github.com/user/repo/compare/v2.0.0...v2.1.0
```

## Commit Categorization

Uses Angular.js commit conventions:

| Commit Prefix | Category | Version Bump |
|---------------|----------|--------------|
| `feat:` | **Added** | Minor (x.Y.0) |
| `fix:` | **Fixed** | Patch (x.y.Z) |
| `perf:` | **Changed** | Patch (x.y.Z) |
| `refactor:` | **Changed** | - |
| `security:` | **Security** | Patch (x.y.Z) |
| `deprecate:` | **Deprecated** | Minor (x.Y.0) |
| `remove:` | **Removed** | Major (X.0.0) |
| `BREAKING CHANGE:` | **Changed** (marked) | Major (X.0.0) |
| `docs:`, `test:`, `chore:` | _(filtered out)_ | - |

## Semantic Versioning

**Version Bumping Strategy**:

```
Breaking Changes → Major (2.1.0 → 3.0.0)
New Features     → Minor (2.1.0 → 2.2.0)
Bug Fixes        → Patch (2.1.0 → 2.1.1)
```

**Example Analysis**:
```
Current Version: 2.1.0
Commits:
  - 1 breaking change (feat!)
  - 3 features (feat:)
  - 2 bug fixes (fix:)

Suggested Version: 3.0.0 (major bump due to breaking change)
```

## What Gets Generated

### Changelog Structure
- ✅ [Unreleased] section for ongoing changes
- ✅ Versioned sections with release dates
- ✅ Categorized changes (Added, Changed, Fixed, etc.)
- ✅ Commit links for traceability
- ✅ Version comparison links
- ✅ Breaking change warnings

### Version Detection
- ✅ Git tags (v2.1.0, 2.1.0)
- ✅ package.json version
- ✅ Cargo.toml version (Rust)
- ✅ pyproject.toml version (Python)
- ✅ pom.xml version (Java)

### Filtering
- ✅ Excludes documentation changes
- ✅ Excludes test additions
- ✅ Excludes build/tooling changes
- ✅ Focuses on user-facing changes

## Requirements

- Claude Code CLI
- Git repository with commit history
- Optional: Conventional commit messages for best results

## License

GPL-3.0

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
