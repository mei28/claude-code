---
name: code-review
allowed-tools: TodoWrite, Read, Grep, Bash(git:*)
description: Automated code review tool that analyzes code quality, detects bugs, identifies security vulnerabilities, and suggests improvements based on industry best practices
---

# Code Review - Automated Code Quality Analysis

## Purpose

Performs comprehensive automated code review to identify bugs, security vulnerabilities, code smells, and opportunities for improvement before creating a pull request. Combines static analysis principles with AI-powered insights to achieve high-quality code.

## When to Use

- ✅ Before creating a pull request
- ✅ After implementing a feature
- ✅ During refactoring
- ✅ When receiving feedback about code quality
- ✅ For learning best practices

## Usage

```
/code-review
/code-review src/specific-file.ts
```

**Arguments** (optional):
- File path: Review specific file(s)
- No arguments: Review all staged/unstaged changes

## Review Categories

### 1. **Code Quality** 🎯

Analyzes code maintainability and readability:

- **Complexity**: Cyclomatic complexity, cognitive complexity
- **Naming**: Variable, function, class naming conventions
- **Structure**: Function length, class size, file organization
- **DRY Violations**: Code duplication detection
- **SOLID Principles**: Single responsibility, open/closed, etc.

**Example Issues**:
```javascript
// ❌ High complexity (cyclomatic complexity: 12)
function processUser(user, action, options) {
  if (user.isActive) {
    if (action === 'update') {
      if (options.validate) {
        if (user.email) {
          // ... many nested conditions
        }
      }
    }
  }
}

// ✅ Refactored (complexity: 3)
function processUser(user, action, options) {
  if (!canProcessUser(user, action, options)) return;

  const processor = getUserProcessor(action);
  return processor.process(user, options);
}
```

### 2. **Bug Detection** 🐛

Identifies potential runtime errors and logical bugs:

- **Null/Undefined**: Potential null pointer exceptions
- **Type Errors**: Type mismatches, unsafe casts
- **Logic Errors**: Off-by-one errors, incorrect conditions
- **Resource Leaks**: Unclosed connections, memory leaks
- **Async Issues**: Race conditions, unhandled promises

**Example Issues**:
```typescript
// ❌ Potential null pointer
function getUserName(user: User): string {
  return user.profile.name; // user.profile might be undefined
}

// ✅ Safe null handling
function getUserName(user: User): string {
  return user.profile?.name ?? 'Unknown';
}
```

### 3. **Security** 🔒

Detects security vulnerabilities and risks:

- **Injection**: SQL injection, XSS, command injection
- **Authentication**: Weak auth, insecure sessions
- **Authorization**: Missing access controls
- **Data Exposure**: Sensitive data in logs, hardcoded secrets
- **Cryptography**: Weak algorithms, insecure random

**Example Issues**:
```javascript
// ❌ SQL Injection vulnerability
const query = `SELECT * FROM users WHERE id = ${userId}`;

// ✅ Parameterized query
const query = 'SELECT * FROM users WHERE id = ?';
db.execute(query, [userId]);
```

### 4. **Performance** ⚡

Identifies performance bottlenecks:

- **Inefficient Algorithms**: O(n²) where O(n) possible
- **Unnecessary Operations**: Redundant calculations, excessive API calls
- **Memory Usage**: Large object creation in loops
- **Caching Opportunities**: Repeated expensive operations
- **Database**: N+1 queries, missing indexes

**Example Issues**:
```python
# ❌ N+1 query problem
for user in users:
    posts = db.query(f"SELECT * FROM posts WHERE user_id = {user.id}")

# ✅ Single query with join
posts_by_user = db.query("""
    SELECT users.*, posts.*
    FROM users
    LEFT JOIN posts ON users.id = posts.user_id
""")
```

### 5. **Best Practices** 📚

Ensures adherence to language and framework conventions:

- **Error Handling**: Proper try-catch usage, error propagation
- **Logging**: Appropriate log levels, structured logging
- **Testing**: Testability, test coverage gaps
- **Documentation**: Missing docstrings, outdated comments
- **Dependencies**: Deprecated APIs, unnecessary dependencies

### 6. **Accessibility** ♿

For frontend code:

- **ARIA**: Missing or incorrect ARIA attributes
- **Semantic HTML**: Proper use of semantic elements
- **Keyboard Navigation**: Missing keyboard support
- **Color Contrast**: Insufficient contrast ratios
- **Alt Text**: Missing image descriptions

## Review Process

### Step 1: Determine Scope

```bash
# Check what needs review
git status
git diff --staged
```

If no arguments provided, review all changed files.
If file path provided, review only that file.

### Step 2: Load Files

```bash
# Read files to review
Read src/auth/login.ts
Read src/api/users.ts
```

### Step 3: Analyze Each Category

Create TodoWrite checklist:

```markdown
## Code Review Progress

- [x] Identify files to review (3 files)
- [ ] Code Quality Analysis
- [ ] Bug Detection
- [ ] Security Analysis
- [ ] Performance Review
- [ ] Best Practices Check
- [ ] Generate Report
```

### Step 4: Generate Report

Create structured review report with:
- Summary statistics
- Issues by category and severity
- Specific recommendations
- Code examples (before/after)

## Output Format

```markdown
# Code Review Report

## Summary

**Files Reviewed**: 3
**Total Issues**: 12
**Critical**: 2 🔴
**High**: 4 🟠
**Medium**: 4 🟡
**Low**: 2 ⚪

## Issues by Category

### Security 🔒 (2 Critical, 1 High)

#### 🔴 CRITICAL: SQL Injection Vulnerability
**File**: `src/api/users.ts:45`
**Issue**: User input directly interpolated into SQL query
**Risk**: Attacker can execute arbitrary SQL commands

```typescript
// Current (vulnerable)
const query = `SELECT * FROM users WHERE email = '${email}'`;

// Recommended fix
const query = 'SELECT * FROM users WHERE email = ?';
const result = await db.execute(query, [email]);
```

**References**:
- [OWASP SQL Injection](https://owasp.org/www-community/attacks/SQL_Injection)
- [Parameterized Queries Best Practices](https://cheatsheetseries.owasp.org/cheatsheets/Query_Parameterization_Cheat_Sheet.html)

---

#### 🔴 CRITICAL: Hardcoded API Key
**File**: `src/config/api.ts:12`
**Issue**: API key stored in source code
**Risk**: Key exposure in version control

```typescript
// Current (insecure)
const API_KEY = 'sk_live_abc123def456';

// Recommended fix
const API_KEY = process.env.API_KEY;
if (!API_KEY) throw new Error('API_KEY not configured');
```

**Action Required**:
1. Move key to environment variable
2. Add to `.env.example` as placeholder
3. Rotate the exposed key immediately
4. Add `.env` to `.gitignore`

---

### Bug Detection 🐛 (2 High, 1 Medium)

#### 🟠 HIGH: Potential Null Pointer Exception
**File**: `src/auth/login.ts:78`
**Issue**: `user.profile` accessed without null check
**Impact**: Runtime crash for users without profile

```typescript
// Current (unsafe)
function getDisplayName(user: User): string {
  return user.profile.displayName || user.email;
}

// Recommended fix
function getDisplayName(user: User): string {
  return user.profile?.displayName ?? user.email;
}
```

---

### Code Quality 🎯 (1 High, 2 Medium)

#### 🟠 HIGH: Excessive Complexity
**File**: `src/utils/validator.ts:34-89`
**Issue**: Function has cyclomatic complexity of 18 (threshold: 10)
**Impact**: Hard to test, maintain, and understand

**Recommendation**:
- Extract validation logic into separate functions
- Use strategy pattern for different validation types
- Consider using validation library (e.g., Zod, Yup)

```typescript
// Current: 56 lines, complexity 18
function validateForm(data) {
  if (data.type === 'user') {
    if (data.email) {
      if (!/@/.test(data.email)) {
        // ... many nested conditions
      }
    }
  }
}

// Recommended: Separate validators
const validators = {
  user: validateUserForm,
  product: validateProductForm,
  order: validateOrderForm
};

function validateForm(data) {
  const validator = validators[data.type];
  if (!validator) throw new Error(`Unknown type: ${data.type}`);
  return validator(data);
}
```

---

### Performance ⚡ (1 Medium, 1 Low)

#### 🟡 MEDIUM: N+1 Query Problem
**File**: `src/api/posts.ts:23-27`
**Issue**: Loading comments in loop causes N+1 queries
**Impact**: Slow response time (O(n) database calls)

```typescript
// Current (N+1 queries)
const posts = await Post.findAll();
for (const post of posts) {
  post.comments = await Comment.findByPostId(post.id);
}

// Recommended (1 query)
const posts = await Post.findAll({
  include: [{ model: Comment }]
});
```

**Expected Improvement**: ~80% reduction in database calls

---

### Best Practices 📚 (1 Medium, 1 Low)

#### 🟡 MEDIUM: Missing Error Handling
**File**: `src/api/upload.ts:45`
**Issue**: Async function without error handling
**Impact**: Unhandled promise rejections

```typescript
// Current (no error handling)
async function uploadFile(file) {
  const url = await storage.upload(file);
  return url;
}

// Recommended
async function uploadFile(file) {
  try {
    const url = await storage.upload(file);
    return url;
  } catch (error) {
    logger.error('File upload failed', { file: file.name, error });
    throw new UploadError('Failed to upload file', { cause: error });
  }
}
```

---

## Recommendations Summary

### Immediate Action Required (Critical Issues)

1. **Fix SQL Injection** in `src/api/users.ts:45`
   - Use parameterized queries
   - Test with SQL injection payloads

2. **Remove Hardcoded API Key** in `src/config/api.ts:12`
   - Move to environment variable
   - Rotate exposed key
   - Update deployment config

### High Priority (Complete Before PR)

3. **Add Null Checks** in `src/auth/login.ts:78`
4. **Reduce Complexity** in `src/utils/validator.ts:34-89`
5. **Fix N+1 Queries** in `src/api/posts.ts:23-27`

### Medium Priority (Address Soon)

6. Add error handling in async functions
7. Improve test coverage for error paths
8. Extract duplicate validation logic

### Low Priority (Technical Debt)

9. Add JSDoc comments for public APIs
10. Consider migrating to TypeScript strict mode
11. Update deprecated dependencies

## Next Steps

1. **Address Critical Issues**: Fix security vulnerabilities immediately
2. **Run Tests**: Ensure fixes don't break existing functionality
3. **Update Tests**: Add tests for edge cases found
4. **Re-run Review**: Verify all issues resolved
5. **Create PR**: Use `/pr-template` to document fixes

## Metrics

- **Review Time**: 2 minutes
- **Issues Found**: 12
- **Estimated Fix Time**: 1-2 hours
- **Code Quality Score**: 72/100 (Good → Excellent after fixes)

---

**Generated by**: Claude Code - Code Review Plugin
**Timestamp**: 2026-01-03 20:45:00
```

## Best Practices

### 1. Review Frequently

Run code review:
- After completing each feature
- Before creating PR
- After addressing review comments
- During refactoring

### 2. Fix High-Severity First

Priority order:
1. 🔴 Critical (Security, Data Loss)
2. 🟠 High (Bugs, Major Quality Issues)
3. 🟡 Medium (Performance, Best Practices)
4. ⚪ Low (Code Style, Documentation)

### 3. Learn from Findings

Each issue is a learning opportunity:
- Understand why it's a problem
- Learn the recommended pattern
- Apply knowledge to future code

### 4. Automate in CI/CD

Integrate into CI pipeline:
```yaml
# .github/workflows/code-review.yml
- name: Code Review
  run: claude code-review
```

### 5. Track Metrics Over Time

Monitor improvements:
- Issues per PR
- Critical issues trend
- Code quality score
- Fix time

## Integration with Other Commands

### Recommended Workflow

```
1. /dig              # Clarify requirements
2. [Implement code]
3. /deslop           # Clean up AI-generated code
4. /code-review      # Check quality before commit
5. /test-generator   # Generate missing tests
6. /commit           # Create logical commits
7. /pr-template      # Generate PR description
```

### With Refactoring

```
/code-review → /refactor → /code-review
```

Verify improvements after refactoring.

## Customization

### Project-Specific Rules

Configure in CLAUDE.md:

```markdown
## Code Review

### Standards
- Max cyclomatic complexity: 10
- Min test coverage: 80%
- Required: ESLint, TypeScript strict mode

### Security
- No hardcoded secrets
- All user input must be validated
- Use parameterized queries only

### Exceptions
- Legacy code in `src/legacy/` (lower standards)
- Generated code in `src/generated/` (skip review)
```

### Language-Specific Rules

The plugin adapts to:
- **JavaScript/TypeScript**: ESLint rules, TypeScript errors
- **Python**: PEP 8, Pylint recommendations
- **Java**: Checkstyle, PMD rules
- **Go**: `go vet`, `golint` standards
- **Rust**: Clippy lints

## Limitations

- **Context-Aware**: Best combined with human review for business logic
- **False Positives**: May flag intentional patterns (review and dismiss)
- **Language Coverage**: Best support for JavaScript/TypeScript, Python, Java
- **Architecture**: Cannot evaluate high-level architecture decisions

## Tips

- 💡 Run after `/deslop` to catch remaining issues
- 💡 Fix critical/high issues before creating PR
- 💡 Use report to learn best practices
- 💡 Configure project standards in CLAUDE.md
- 💡 Combine with `/refactor` for code improvements
- 💡 Re-run after fixes to verify resolution

## References

Research shows automated code review can:
- Detect 46-90% of bugs before deployment
- Save 40% of manual review time
- Reduce post-deployment bugs by 50%
- Improve code quality scores by 30-40%

**Sources**:
- [Best Automated Code Review Tools 2025](https://www.qodo.ai/blog/automated-code-review/)
- [AI Code Review Automation Guide](https://www.digitalapplied.com/blog/ai-code-review-automation-guide-2025)
- [Static Code Analysis Best Practices](https://www.oligo.security/academy/static-code-analysis)
