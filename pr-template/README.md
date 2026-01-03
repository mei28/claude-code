# PR Template Generator

## Overview

PR Template Generator is a Claude Code plugin that analyzes GitHub pull requests and automatically generates comprehensive, well-structured PR descriptions in English (default) or Japanese using GitHub CLI.

## What It Does

Transforms minimal PR information into comprehensive documentation:
- ✅ Analyzes PR changes using GitHub CLI
- ✅ Reads files selectively for context investigation
- ✅ Generates detailed PR descriptions (English default, Japanese optional)
- ✅ Follows established template format
- ✅ Saves template to `.tmp/` directory
- ✅ Ready to copy to GitHub PR

## Installation

```bash
/plugin install https://github.com/YOUR_USERNAME/claude-code-commands/pr-template
```

Or manually:
```bash
git clone https://github.com/YOUR_USERNAME/claude-code-commands
ln -s $(pwd)/claude-code-commands/pr-template ~/.claude/plugins/pr-template
```

## Usage

```
/pr-template <PR_NUMBER>
```

**Examples**:
```
/pr-template 123
/pr-template 456
```

## Example

**Input**: PR #123 with minimal description

**Command**:
```
/pr-template 123
```

**Generated Template** (English):
```markdown
## Overview

Improved user authentication performance.
API response time reduced from 200ms to 50ms average, enhancing user experience.
Achieved through token validation optimization and cache mechanism introduction.

## Changes/Additions

### New Features
- **Token Cache Mechanism** (`src/auth/tokenCache.ts`)
  - Implement 5-minute token cache using Redis
  - Achieve 90% cache hit rate
  - L45-120: Cache logic implementation

### Performance Improvements
- **Authentication API Optimization** (`src/api/auth.ts`)
  - Optimize database queries (resolve N+1 problem)
  - L78-95: Reduce DB calls through query joining

[... more sections ...]
```

**Saved to**: `.tmp/pr-template-123.md`

## Template Sections

### 1. Overview (概要)
- 1-3 concise lines
- Explains "why", "what", and "how"
- Business value and impact

### 2. Changes/Additions (修正内容・追加内容)
- Categorized breakdown of all modifications
- Specific files with line numbers
- Technical implementation details

### 3. Testing/Verification (動作確認)
- Critical test scenarios
- Functionality verification steps
- Edge cases and error conditions

### 4. Review Focus (レビュー観点) - Optional
- Areas requiring special attention
- Potential risks or concerns
- Security considerations

### 5. Additional Notes (補足・参考)
- New library additions with links
- Reference materials
- Performance metrics
- Future improvements

## Language Configuration

The plugin generates descriptions in **English by default**.

### Switching to Japanese

**Option 1**: Configure in CLAUDE.md
```markdown
## PR Template
Language: Japanese
```

**Option 2**: Request when invoking
```
/pr-template 123 in Japanese
/pr-template 123 日本語で
```

## Features

### Intelligent Analysis

Analyzes:
- File changes and line modifications
- Change patterns (features, fixes, refactoring)
- Technical implementation details
- Business value and impact

### Comprehensive Documentation

Generates:
- Clear, concise overview
- Detailed change breakdown
- Practical testing suggestions
- Relevant supplementary information

### Japanese Output

All content in Japanese:
- Natural, professional Japanese
- Technical terms appropriately used
- Clear, readable formatting

### Markdown Formatting

- Proper section headers
- Code blocks with syntax highlighting
- Tables for structured data
- Lists for easy scanning

## Requirements

### Prerequisites

1. **GitHub CLI** (`gh`)
   ```bash
   # Install gh
   brew install gh  # macOS
   # Or see: https://cli.github.com/

   # Authenticate
   gh auth login
   ```

2. **Repository Access**
   - Read access to the repository
   - PR must exist on GitHub

## Workflow Integration

### Recommended Flow

```
1. Make code changes
2. Run /commit to create logical commits
3. Push to remote and create PR on GitHub
4. Run /pr-template <PR_NUMBER>
5. Review generated template in .tmp/
6. Copy content to GitHub PR description
7. Request code review
```

### With Other Commands

**Before PR**:
```
/deslop          # Clean up code
/commit          # Create commits
git push         # Push to remote
gh pr create     # Create PR
```

**After PR**:
```
/pr-template 123 # Generate description
# Copy .tmp/pr-template-123.md to PR
```

## Best Practices

### 1. Run Immediately After PR Creation

Generate template while context is fresh:
```bash
gh pr create --title "Add authentication"
/pr-template $(gh pr view --json number -q .number)
```

### 2. Review and Edit

Generated template is comprehensive but review for:
- Project-specific details
- Screenshots (add manually for UI changes)
- Links to related issues/PRs
- Team-specific context

### 3. Keep Template Updated

If you push more commits:
```bash
/pr-template 123  # Regenerate with latest changes
```

### 4. Save Custom Sections

For similar PRs, save reusable sections:
```bash
# Save performance metrics template
cat .tmp/pr-template-123.md | grep -A 10 "パフォーマンス結果" > .tmp/perf-template.md
```

## Configuration

### Project-Specific Templates

If your project has custom PR templates:

```bash
# Check existing template
cat .github/PULL_REQUEST_TEMPLATE.md
```

The plugin will adapt to match your project's format.

## Troubleshooting

### "gh: command not found"

Install GitHub CLI:
```bash
brew install gh
# Or visit: https://cli.github.com/
```

### "PR not found"

Verify PR number:
```bash
gh pr list
```

### "Not authenticated"

Login to GitHub:
```bash
gh auth login
```

## Limitations

- Requires GitHub CLI installed and authenticated
- Does not include screenshots (add manually)
- May not capture all business context (review recommended)
- Works best with focused, clear changes
- Language must be configured for non-English output

## Security

- Only accesses public PR information
- Does not modify PR or push changes
- Templates saved locally in `.tmp/`
- Respects GitHub authentication

## License

GPL-3.0

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## Tips

- 💡 Run immediately after creating PR
- 💡 Edit generated template for project-specific details
- 💡 Read files selectively to optimize token usage
- 💡 Add screenshots manually for UI changes
- 💡 Link to related issues in additional notes section
- 💡 Include performance metrics when available
- 💡 Configure language preference in CLAUDE.md for consistency
