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
/plugin install https://github.com/mei28/claude-code/deslop
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
/plugin install https://github.com/mei28/claude-code/dig
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
/plugin install https://github.com/mei28/claude-code/auto-commit
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
/plugin install https://github.com/mei28/claude-code/pr-template
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

### 🔍 [Code Review](./code-review) - Automated Code Quality Analysis

Performs comprehensive automated code quality analysis, detecting bugs, security vulnerabilities, and suggesting improvements.

**Use when**: Before creating a pull request to ensure high code quality

**What it does**:
- ✅ Analyzes code across 6 dimensions (quality, bugs, security, performance, best practices, accessibility)
- ✅ Detects security vulnerabilities (SQL injection, XSS, authentication issues)
- ✅ Identifies performance problems (N+1 queries, inefficient algorithms, memory leaks)
- ✅ Checks best practices (error handling, logging, testing)
- ✅ Prioritizes findings by severity (Critical, High, Medium, Low)
- ✅ Provides code examples with fixes

**Categories**:
- 💎 Code Quality: Complexity, naming, structure
- 🐛 Bug Detection: Null pointers, type errors, race conditions
- 🔒 Security: Injection attacks, data exposure
- ⚡ Performance: Inefficient code, blocking operations
- ✅ Best Practices: Error handling, documentation
- ♿ Accessibility: ARIA, semantic HTML

**Installation**:
```bash
/plugin install https://github.com/mei28/claude-code/code-review
```

**Usage**:
```
/code-review
/code-review src/api/users.ts
/code-review --security
```

---

### 🧪 [Test Generator](./test-generator) - Automated Unit Test Creation

Automatically generates comprehensive unit tests for functions, classes, and modules with meaningful test cases.

**Use when**: After implementing features, for legacy code, or before refactoring

**What it does**:
- ✅ Generates normal cases, edge cases, error conditions, boundary values
- ✅ Creates mocks for dependencies
- ✅ Supports multiple frameworks (Jest, pytest, JUnit, Go testing, etc.)
- ✅ Reduces manual test writing by up to 97%
- ✅ Generates data-driven tests
- ✅ Improves test coverage by 30-50%

**Supported Frameworks**:
- **JavaScript/TypeScript**: Jest, Vitest, Mocha, Jasmine
- **Python**: pytest, unittest, nose2
- **Java**: JUnit 5, TestNG, Mockito
- **Go**: testing, testify
- **Ruby**: RSpec, Minitest
- **Rust**: Built-in test framework

**Installation**:
```bash
/plugin install https://github.com/mei28/claude-code/test-generator
```

**Usage**:
```
/test-generator
/test-generator src/utils/calculator.ts
/test-generator --coverage
```

---

### ♻️ [Refactor](./refactor) - Code Quality Improvement

Suggests and applies code refactoring improvements including complexity reduction and code smell removal.

**Use when**: Before adding features, after code review feedback, or for technical debt reduction

**What it does**:
- ✅ Identifies refactoring opportunities with before/after examples
- ✅ Reduces cyclomatic complexity
- ✅ Extracts methods from long functions
- ✅ Removes code duplication (DRY principle)
- ✅ Replaces magic numbers with constants
- ✅ Simplifies parameter lists
- ✅ Applies safe automatic refactorings

**Refactoring Patterns**:
- 🔻 Complexity Reduction
- 🔨 Extract Method
- 🔄 Remove Duplication
- 🎭 Replace Conditional with Polymorphism
- 📦 Introduce Parameter Object
- 🔢 Replace Magic Numbers

**Installation**:
```bash
/plugin install https://github.com/mei28/claude-code/refactor
```

**Usage**:
```
/refactor
/refactor src/services/orderService.ts
/refactor --suggest
/refactor --apply
```

---

### 📚 [Doc-Gen](./doc-gen) - API Documentation Generator

Generates comprehensive API documentation from code including OpenAPI/Swagger specs and API reference guides.

**Use when**: After implementing API endpoints, before releasing public APIs, or documenting legacy APIs

**What it does**:
- ✅ Generates OpenAPI/Swagger 3.0 specifications
- ✅ Adds JSDoc/TSDoc/Javadoc comments to code
- ✅ Creates Markdown API reference guides
- ✅ Generates request/response examples
- ✅ Supports REST APIs, GraphQL, and function libraries
- ✅ Creates Swagger UI and Redoc integration

**Supported Types**:
- **REST APIs**: Express, Fastify, NestJS, FastAPI, Spring Boot
- **GraphQL**: Apollo, GraphQL schemas
- **Comments**: JSDoc, TSDoc, Javadoc, Python docstrings, GoDoc, Rustdoc

**Installation**:
```bash
/plugin install https://github.com/mei28/claude-code/doc-gen
```

**Usage**:
```
/doc-gen
/doc-gen src/api/users.ts
/doc-gen --openapi
/doc-gen --jsdoc
```

---

### 📋 [Changelog](./changelog) - Automated Release Notes

Generates CHANGELOG.md from git commit history following Keep a Changelog format with semantic versioning.

**Use when**: Before creating releases, when preparing release notes, or after merging features

**What it does**:
- ✅ Follows Keep a Changelog format
- ✅ Categorizes commits (Added, Changed, Fixed, Deprecated, Removed, Security)
- ✅ Suggests semantic version bumps
- ✅ Detects breaking changes prominently
- ✅ Filters out non-user-facing changes
- ✅ Adds commit links for traceability

**Commit Categorization**:
- `feat:` → Added (minor version bump)
- `fix:` → Fixed (patch version bump)
- `BREAKING CHANGE:` → Changed with warning (major version bump)
- `security:` → Security
- `deprecate:` → Deprecated
- `remove:` → Removed

**Installation**:
```bash
/plugin install https://github.com/mei28/claude-code/changelog
```

**Usage**:
```
/changelog
/changelog --version 2.1.0
/changelog --since v2.0.0
/changelog --preview
```

---

## 📦 Installation

### Method 1: Install from Marketplace (Recommended)

First, add the marketplace:

```bash
/plugin marketplace add https://github.com/mei28/claude-code
```

Then install individual plugins:

```bash
# Development Workflow
/plugin install deslop@mei28/claude-code
/plugin install dig@mei28/claude-code
/plugin install auto-commit@mei28/claude-code
/plugin install pr-template@mei28/claude-code

# Code Quality & Testing
/plugin install code-review@mei28/claude-code
/plugin install test-generator@mei28/claude-code
/plugin install refactor@mei28/claude-code

# Documentation & Release
/plugin install doc-gen@mei28/claude-code
/plugin install changelog@mei28/claude-code
```

Or install all at once:

```bash
/plugin marketplace add https://github.com/mei28/claude-code
/plugin install deslop@mei28/claude-code
/plugin install dig@mei28/claude-code
/plugin install auto-commit@mei28/claude-code
/plugin install pr-template@mei28/claude-code
/plugin install code-review@mei28/claude-code
/plugin install test-generator@mei28/claude-code
/plugin install refactor@mei28/claude-code
/plugin install doc-gen@mei28/claude-code
/plugin install changelog@mei28/claude-code
```

### Method 2: Install from Local Path

Clone the repository and install locally:

```bash
git clone https://github.com/mei28/claude-code
cd claude-code

# Install all plugins
/plugin install $(pwd)/deslop
/plugin install $(pwd)/dig
/plugin install $(pwd)/auto-commit
/plugin install $(pwd)/pr-template
/plugin install $(pwd)/code-review
/plugin install $(pwd)/test-generator
/plugin install $(pwd)/refactor
/plugin install $(pwd)/doc-gen
/plugin install $(pwd)/changelog
```

## 🎯 Recommended Workflow

### For New Features (Complete Workflow)

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

4. **Generate Tests**
   ```
   /test-generator
   ```
   Auto-generate comprehensive unit tests for new code

5. **Review Code Quality**
   ```
   /code-review
   ```
   Check for bugs, security issues, and performance problems

6. **Refactor if Needed**
   ```
   /refactor --suggest
   ```
   Get suggestions for complexity reduction and code improvements

7. **Review & Cleanup**
   ```
   /deslop
   ```
   Remove any unnecessary additions or style inconsistencies

8. **Generate Documentation**
   ```
   /doc-gen
   ```
   Create API documentation and code comments

9. **Create Commits**
   ```
   /commit
   ```
   Automatically organize changes into logical commits

10. **Push and Create PR**
    ```
    git push
    gh pr create --title "Add user authentication"
    ```

11. **Generate PR Description**
    ```
    /pr-template 123
    ```
    Copy content from `.tmp/pr-template-123.md` to PR

### For Code Quality Improvement

1. **Review existing code**
   ```
   /code-review src/services/
   ```
   Identify issues across quality, security, performance

2. **Generate tests for coverage**
   ```
   /test-generator --coverage
   ```
   Add tests for uncovered code paths

3. **Refactor complex code**
   ```
   /refactor src/services/orderService.ts
   ```
   Reduce complexity and improve maintainability

4. **Run tests**
   ```
   npm test
   ```

5. **Commit improvements**
   ```
   /commit
   ```

### For Release Preparation

1. **Review code quality**
   ```
   /code-review
   ```
   Final check before release

2. **Ensure test coverage**
   ```
   /test-generator --coverage
   npm test -- --coverage
   ```

3. **Generate/update documentation**
   ```
   /doc-gen --openapi
   ```
   Update API docs and specs

4. **Generate changelog**
   ```
   /changelog --version 2.1.0
   ```
   Create release notes from commits

5. **Commit changelog**
   ```
   /commit
   ```

6. **Create release**
   ```
   git tag -a v2.1.0 -m "Release v2.1.0"
   git push origin v2.1.0
   gh release create v2.1.0 --notes-file CHANGELOG.md
   ```

### Quick Workflows by Task

**Bug Fix**:
```
1. /test-generator    # Add regression test
2. [Fix the bug]
3. /code-review       # Verify fix
4. /commit            # Commit fix + test
```

**Refactoring**:
```
1. /test-generator    # Safety net
2. /refactor --suggest # Get suggestions
3. [Apply refactorings]
4. npm test           # Verify
5. /commit            # Commit
```

**API Development**:
```
1. [Implement endpoint]
2. /doc-gen --openapi # Generate docs
3. /test-generator    # Generate tests
4. /code-review       # Check quality
5. /commit            # Commit all
```

## 🛠️ Development

### Project Structure

```
claude-code/
├── README.md                    # This file
│
├── deslop/                      # AI Code Cleanup
│   ├── .claude-plugin/
│   │   └── plugin.json
│   ├── commands/
│   │   └── deslop.md
│   └── README.md
│
├── dig/                         # Requirements Clarification
│   ├── .claude-plugin/
│   │   └── plugin.json
│   ├── commands/
│   │   └── dig.md
│   └── README.md
│
├── auto-commit/                 # Git Commit Automation
│   ├── .claude-plugin/
│   │   └── plugin.json
│   ├── commands/
│   │   └── commit.md
│   └── README.md
│
├── pr-template/                 # PR Description Generator
│   ├── .claude-plugin/
│   │   └── plugin.json
│   ├── commands/
│   │   └── pr-template.md
│   └── README.md
│
├── code-review/                 # Code Quality Analysis
│   ├── .claude-plugin/
│   │   └── plugin.json
│   ├── commands/
│   │   └── code-review.md
│   └── README.md
│
├── test-generator/              # Unit Test Creation
│   ├── .claude-plugin/
│   │   └── plugin.json
│   ├── commands/
│   │   └── test-generator.md
│   └── README.md
│
├── refactor/                    # Code Refactoring
│   ├── .claude-plugin/
│   │   └── plugin.json
│   ├── commands/
│   │   └── refactor.md
│   └── README.md
│
├── doc-gen/                     # API Documentation
│   ├── .claude-plugin/
│   │   └── plugin.json
│   ├── commands/
│   │   └── doc-gen.md
│   └── README.md
│
└── changelog/                   # Release Notes
    ├── .claude-plugin/
    │   └── plugin.json
    ├── commands/
    │   └── changelog.md
    └── README.md
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

- Repository: https://github.com/mei28/claude-code
- Issues: https://github.com/mei28/claude-code/issues
- Discussions: https://github.com/mei28/claude-code/discussions

## ⭐ Star History

If you find these plugins useful, please consider giving this repository a star!

---

**Happy coding with Claude! 🚀**
