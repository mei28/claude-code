# Dig - Requirements Clarification Plugin

## Overview

Dig is a Claude Code plugin that systematically identifies ambiguities in requirements and architecture through structured questions across multiple categories (Architecture, Data, API, UI/UX, Testing, Security, Performance, Deployment). This prevents wasted effort from unclear specifications.

## What It Does

Before you start implementing a feature, Dig:
1. ✅ Reads your project context files (CLAUDE.md, architecture docs, etc.)
2. ✅ Analyzes the feature request for ambiguities
3. ✅ Identifies unclear points across 8 categories
4. ✅ Generates specific, actionable questions with options
5. ✅ Provides recommendations based on existing project patterns

## Installation

```bash
/plugin install https://github.com/mei28/claude-code-commands/dig
```

Or manually:
```bash
git clone https://github.com/mei28/claude-code-commands
ln -s $(pwd)/claude-code-commands/dig ~/.claude/plugins/dig
```

## Usage

Simply invoke the command when starting a new feature:

```
/dig
```

Or use it before planning:

```
User: Add user authentication to the app
You: Let me run /dig to clarify the requirements first
```

## Example Output

**Request**: "Add dark mode toggle"

**Dig finds**:
- 🎨 **UI/UX**: Where should the toggle be placed? (navbar vs settings)
- 💾 **Data**: Should preference sync across devices? (localStorage vs database)
- 🏗️ **Architecture**: How to integrate with existing theme system?
- ⚡ **Performance**: Should switching be animated?
- 🔒 **Security**: Any considerations for theme persistence?

Each question includes:
- **Context**: Why this matters
- **Options**: 2-4 concrete approaches
- **Impact**: How it affects implementation
- **Recommendation**: Suggested approach based on your project standards

## Categories Analyzed

1. 🏗️ **Architecture & Design** - Patterns, structure, organization
2. 💾 **Data & State Management** - State, persistence, caching
3. 🔌 **API & Integration** - Endpoints, protocols, external services
4. 🎨 **UI/UX & User Interface** - Components, flows, accessibility
5. ✅ **Testing & Quality** - Coverage, frameworks, strategies
6. 🔒 **Security & Authorization** - Access control, encryption, audit
7. ⚡ **Performance & Scalability** - Load, optimization, caching
8. 🚀 **Deployment & Operations** - Migrations, monitoring, rollback

## Why Use Dig?

### Without Dig
```
User: Add authentication
Claude: [Starts implementing with assumptions]
Claude: [Realizes later] Wait, should this use OAuth or JWT?
Claude: [Has to refactor]
```

### With Dig
```
User: Add authentication
Claude: /dig
[Identifies 8 ambiguities: OAuth vs JWT, where to store tokens,
 session duration, password requirements, etc.]
User: [Answers questions]
Claude: [Implements correctly the first time]
```

## Best Practices

1. **Use before complex features**: Any feature with multiple implementation approaches
2. **Read your CLAUDE.md**: Dig leverages your project standards
3. **Answer high-impact questions first**: Dig prioritizes what matters most
4. **Share with team**: Dig output great for stakeholder alignment

## Integration with Planning

Perfect workflow:
```
1. User requests feature
2. Run /dig to identify ambiguities
3. User answers questions
4. Use EnterPlanMode with complete context
5. Implement with confidence
```

## Requirements

- Claude Code CLI
- Project documentation (CLAUDE.md, README.md, etc.) - optional but recommended

## License

GPL-3.0

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## Tips

- 💡 For simple one-line changes, skip Dig - use your judgment
- 💡 For new features or refactoring, always run Dig first
- 💡 Dig output can be shared in PRs to document design decisions
- 💡 Update CLAUDE.md with standards to get better recommendations
