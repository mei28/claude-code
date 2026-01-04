# Code Review - Automated Code Quality Analysis Plugin

## Overview

Code Review is a Claude Code plugin that performs comprehensive automated code quality analysis. It detects bugs, identifies security vulnerabilities, suggests performance improvements, and ensures best practices are followed before creating pull requests.

## What It Does

This plugin analyzes your code across six critical dimensions:

- **Code Quality**: Cyclomatic complexity, naming conventions, code structure
- **Bug Detection**: Null pointers, type errors, logic errors, race conditions
- **Security**: SQL injection, XSS, authentication issues, data exposure
- **Performance**: Inefficient algorithms, N+1 queries, memory leaks
- **Best Practices**: Error handling, logging, testing, documentation
- **Accessibility**: ARIA labels, semantic HTML, keyboard navigation

## Installation

### From Marketplace (Recommended)

```bash
# Add marketplace first (one time only)
/plugin marketplace add https://github.com/mei28/claude-code

# Install plugin
/plugin install code-review@mei28/claude-code
```

### From Local Path

```bash
git clone https://github.com/mei28/claude-code
cd claude-code
/plugin install $(pwd)/code-review
```

## Usage

Run code review before creating a pull request:

```
/code-review
```

Review specific files:
```
/code-review src/api/users.ts
```

Focus on specific aspects:
```
/code-review --security
/code-review --performance
```

The plugin will:
1. Analyze recent changes or specified files
2. Detect issues across all categories
3. Prioritize findings by severity (Critical, High, Medium, Low)
4. Provide specific code examples with fixes
5. Generate actionable improvement recommendations

## Example

**Before Review**:
```javascript
app.get('/user', (req, res) => {
  const query = `SELECT * FROM users WHERE email = '${req.query.email}'`;
  db.query(query, (err, result) => {
    res.json(result[0]);
  });
});
```

**Code Review Findings**:

🔴 **CRITICAL - Security Vulnerability**
- **Issue**: SQL Injection in user query
- **Line**: 2
- **Impact**: Attacker can execute arbitrary SQL

**Recommended Fix**:
```javascript
app.get('/user', (req, res) => {
  const query = 'SELECT * FROM users WHERE email = ?';
  db.query(query, [req.query.email], (err, result) => {
    if (err) return res.status(500).json({ error: 'Database error' });
    if (!result || result.length === 0) {
      return res.status(404).json({ error: 'User not found' });
    }
    res.json(result[0]);
  });
});
```

## What Gets Detected

### Code Quality
- ✅ High cyclomatic complexity (>10)
- ✅ Long functions (>50 lines)
- ✅ Deep nesting (>4 levels)
- ✅ Magic numbers
- ✅ Inconsistent naming

### Security
- ✅ SQL injection vulnerabilities
- ✅ XSS vulnerabilities
- ✅ Authentication bypasses
- ✅ Sensitive data exposure
- ✅ CSRF vulnerabilities

### Performance
- ✅ N+1 query problems
- ✅ Inefficient algorithms
- ✅ Memory leaks
- ✅ Synchronous blocking operations
- ✅ Missing pagination

### Best Practices
- ✅ Missing error handling
- ✅ Inadequate logging
- ✅ Missing tests
- ✅ Incomplete documentation
- ✅ Hardcoded configurations

## Requirements

- Claude Code CLI
- Git repository (for analyzing changes)

## License

GPL-3.0

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
