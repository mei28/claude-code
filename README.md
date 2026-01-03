# Claude Code Commands Collection

A curated collection of Claude Code plugins to enhance your AI-assisted development workflow.

## 🚀 Available Plugins

### 🧹 [Deslop](./deslop) - AI Code Cleanup

Detects and removes unnecessary additions in AI-generated code, helping maintain codebase consistency.

**Use when**: Reviewing AI-generated code for over-engineering or style inconsistencies

**What it does**:
- ✅ Removes excessive comments explaining obvious code
- ✅ Eliminates over-defensive error handling
- ✅ Identifies unnecessary abstractions
- ✅ Fixes style inconsistencies with existing code
- ✅ Enforces YAGNI/DRY/KISS principles

**Installation**:
```bash
/plugin install https://github.com/YOUR_USERNAME/claude-code-commands/deslop
```

**Usage**:
```
/deslop
```

---

### 🔍 [Dig](./dig) - Requirements Clarification

Identifies ambiguities in requirements and architecture through structured questions before implementation begins.

**Use when**: Starting new features or when requirements are unclear

**What it does**:
- ✅ Reads project context files (CLAUDE.md, docs, etc.)
- ✅ Identifies ambiguities across 8 categories
- ✅ Generates specific questions with options
- ✅ Provides recommendations based on project standards
- ✅ Prevents wasted effort from unclear specifications

**Categories analyzed**:
- 🏗️ Architecture & Design
- 💾 Data & State Management
- 🔌 API & Integration
- 🎨 UI/UX & User Interface
- ✅ Testing & Quality
- 🔒 Security & Authorization
- ⚡ Performance & Scalability
- 🚀 Deployment & Operations

**Installation**:
```bash
/plugin install https://github.com/YOUR_USERNAME/claude-code-commands/dig
```

**Usage**:
```
/dig
```

---

### 🤖 [Auto Commit](./auto-commit) - Intelligent Git Commit Automation

Analyzes unstaged git changes and automatically creates well-structured, logically grouped commits with meaningful messages.

**Use when**: You have multiple unstaged changes that need organizing into logical commits

**What it does**:
- ✅ Analyzes all unstaged changes intelligently
- ✅ Groups related files logically
- ✅ Generates meaningful commit messages in English (default) or Japanese
- ✅ Follows Angular.js commit guidelines (feat, fix, docs, etc.)
- ✅ Creates individual commits automatically
- ✅ Handles pre-commit hooks and errors gracefully

**Commit Prefixes**:
- `feat`: New feature (`feat: add authentication` / `feat: 認証機能を追加`)
- `fix`: Bug fix (`fix: resolve login error` / `fix: ログインエラーを修正`)
- `docs`: Documentation
- `style`: Formatting
- `refactor`: Code restructuring
- `perf`: Performance
- `test`: Tests
- `chore`: Build/tools

**Language**: English by default, configurable to Japanese in CLAUDE.md

**Installation**:
```bash
/plugin install https://github.com/YOUR_USERNAME/claude-code-commands/auto-commit
```

**Usage**:
```
/commit
```

---

### 📝 [PR Template](./pr-template) - Pull Request Description Generator

Generates comprehensive PR descriptions in English (default) or Japanese by analyzing GitHub pull requests using GitHub CLI.

**Use when**: After creating a GitHub PR to document changes thoroughly

**What it does**:
- ✅ Analyzes PR changes using GitHub CLI
- ✅ Reads files selectively for context
- ✅ Generates detailed PR descriptions (English default, Japanese optional)
- ✅ Follows established template format
- ✅ Saves template to `.tmp/` directory

**Template Sections**:
- Overview (概要): Why, what, and how
- Changes/Additions (修正内容・追加内容): Detailed breakdown
- Testing/Verification (動作確認): Test scenarios
- Review Focus (レビュー観点): Security, performance, etc.
- Additional Notes (補足・参考): Libraries, metrics, future work

**Installation**:
```bash
/plugin install https://github.com/YOUR_USERNAME/claude-code-commands/pr-template
```

**Usage**:
```
/pr-template <PR_NUMBER>
/pr-template 123
/pr-template 123 in Japanese  # For Japanese output
```

**Requirements**:
- GitHub CLI (`gh`) installed and authenticated
- Optional: Configure language in CLAUDE.md

---

## 📦 Installation

### Install All Plugins

```bash
git clone https://github.com/YOUR_USERNAME/claude-code-commands
cd claude-code-commands

# Install all plugins
/plugin install $(pwd)/deslop
/plugin install $(pwd)/dig
/plugin install $(pwd)/auto-commit
/plugin install $(pwd)/pr-template
```

### Install Individual Plugins

```bash
/plugin install https://github.com/YOUR_USERNAME/claude-code-commands/deslop
/plugin install https://github.com/YOUR_USERNAME/claude-code-commands/dig
/plugin install https://github.com/YOUR_USERNAME/claude-code-commands/auto-commit
/plugin install https://github.com/YOUR_USERNAME/claude-code-commands/pr-template
```

## 🎯 Recommended Workflow

### For New Features

1. **Clarify Requirements**
   ```
   User: Add user authentication
   Claude: /dig
   ```
   Answer ambiguity questions about OAuth vs JWT, token storage, etc.

2. **Plan Implementation**
   ```
   EnterPlanMode with complete context from Dig
   ```

3. **Implement**
   ```
   Write code following the plan
   ```

4. **Review & Cleanup**
   ```
   /deslop
   ```
   Remove any unnecessary additions or style inconsistencies

5. **Create Commits**
   ```
   /commit
   ```
   Automatically organize changes into logical commits

6. **Push and Create PR**
   ```
   git push
   gh pr create --title "Add user authentication"
   ```

7. **Generate PR Description**
   ```
   /pr-template 123
   ```
   Copy content from `.tmp/pr-template-123.md` to PR

### For Code Review

1. **Review AI-generated code**
   ```
   /deslop
   ```
   Identify and fix over-engineering

2. **Run tests**
   ```
   npm test
   ```

3. **Create organized commits**
   ```
   /commit
   ```

4. **Push and create PR**
   ```
   git push
   gh pr create
   ```

5. **Generate PR description**
   ```
   /pr-template <PR_NUMBER>
   ```

## 🛠️ Development

### Project Structure

```
claude-code-commands/
├── README.md                    # This file
├── deslop/                      # Deslop plugin
│   ├── .claude-plugin/
│   │   └── plugin.json         # Plugin metadata
│   ├── commands/
│   │   └── deslop.md          # Command implementation
│   └── README.md               # Deslop documentation
├── dig/                         # Dig plugin
│   ├── .claude-plugin/
│   │   └── plugin.json         # Plugin metadata
│   ├── commands/
│   │   └── dig.md             # Command implementation
│   └── README.md               # Dig documentation
├── auto-commit/                 # Auto Commit plugin
│   ├── .claude-plugin/
│   │   └── plugin.json         # Plugin metadata
│   ├── commands/
│   │   └── commit.md          # Command implementation
│   └── README.md               # Auto Commit documentation
└── pr-template/                 # PR Template plugin
    ├── .claude-plugin/
    │   └── plugin.json         # Plugin metadata
    ├── commands/
    │   └── pr-template.md     # Command implementation
    └── README.md               # PR Template documentation
```

### Adding New Plugins

1. Create plugin directory structure:
   ```bash
   mkdir -p your-plugin/.claude-plugin your-plugin/commands
   ```

2. Create `plugin.json`:
   ```json
   {
     "name": "your-plugin",
     "version": "1.0.0",
     "description": "Your plugin description",
     "author": {
       "name": "Your Name"
     },
     "license": "GPL-3.0"
   }
   ```

3. Create command file `commands/your-command.md`:
   ```markdown
   ---
   name: your-command
   description: Command description
   ---

   # Your Command

   [Implementation details]
   ```

4. Update this README with your plugin

## 📝 License

GPL-3.0

## 🤝 Contributing

Contributions are welcome! Here's how:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/new-plugin`)
3. Add your plugin following the structure above
4. Update this README
5. Submit a Pull Request

### Contribution Guidelines

- All command files must be in English
- Include comprehensive documentation in README.md
- Provide usage examples
- Follow existing plugin structure
- Test your plugin before submitting

## 🙏 Acknowledgments

Inspired by the growing Claude Code community and the need for better AI-assisted development workflows.

## 📚 Resources

- [Claude Code Documentation](https://code.claude.com/docs)
- [Plugin Development Guide](https://code.claude.com/docs/en/plugins.md)
- [Skills Documentation](https://code.claude.com/docs/en/skills.md)

## 🔗 Links

- Repository: https://github.com/YOUR_USERNAME/claude-code-commands
- Issues: https://github.com/YOUR_USERNAME/claude-code-commands/issues
- Discussions: https://github.com/YOUR_USERNAME/claude-code-commands/discussions

## ⭐ Star History

If you find these plugins useful, please consider giving this repository a star!

---

**Happy coding with Claude! 🚀**
