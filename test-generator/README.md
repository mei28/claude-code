# Test Generator - Automated Unit Test Creation Plugin

## Overview

Test Generator is a Claude Code plugin that automatically generates comprehensive unit tests for your functions, classes, and modules. It reduces manual test writing by up to 97% while improving test coverage with meaningful test cases including edge cases and error conditions.

## What It Does

Analyzing your code structure, this plugin generates:

- **Normal Cases**: Tests for expected, typical usage
- **Edge Cases**: Tests for unusual but valid inputs
- **Error Conditions**: Tests for invalid inputs and error handling
- **Boundary Values**: Tests for limits and boundaries
- **Integration Points**: Tests for interactions with dependencies (with mocks)

Supports multiple testing frameworks:
- **JavaScript/TypeScript**: Jest, Vitest, Mocha, Jasmine
- **Python**: pytest, unittest, nose2
- **Java**: JUnit 5, TestNG, Mockito
- **Go**: testing, testify
- **Ruby**: RSpec, Minitest
- **Rust**: Built-in test framework

## Installation

```bash
/plugin install https://github.com/mei28/claude-code/test-generator
```

Or manually:
```bash
git clone https://github.com/mei28/claude-code
ln -s $(pwd)/claude-code/test-generator ~/.claude/plugins/test-generator
```

## Usage

Generate tests for recent changes:
```
/test-generator
```

Generate tests for specific files:
```
/test-generator src/utils/calculator.ts
```

Check current coverage gaps:
```
/test-generator --coverage
```

The plugin will:
1. Detect your testing framework
2. Analyze target code structure
3. Check existing tests for gaps
4. Generate comprehensive test file
5. Run tests to verify they work

## Example

**Source Code**:
```typescript
// src/utils/calculator.ts
export function divide(a: number, b: number): number {
  if (b === 0) {
    throw new Error('Division by zero');
  }
  return a / b;
}
```

**Generated Tests**:
```typescript
// tests/utils/calculator.test.ts
import { divide } from '../../src/utils/calculator';

describe('divide', () => {
  describe('Normal Cases', () => {
    test('should divide positive integers', () => {
      expect(divide(10, 2)).toBe(5);
    });

    test('should divide negative numbers', () => {
      expect(divide(-10, 2)).toBe(-5);
      expect(divide(10, -2)).toBe(-5);
      expect(divide(-10, -2)).toBe(5);
    });

    test('should handle decimal results', () => {
      expect(divide(10, 3)).toBeCloseTo(3.333, 3);
    });
  });

  describe('Edge Cases', () => {
    test('should handle division resulting in zero', () => {
      expect(divide(0, 5)).toBe(0);
    });

    test('should handle very small numbers', () => {
      expect(divide(0.0001, 0.0002)).toBeCloseTo(0.5, 4);
    });

    test('should handle very large numbers', () => {
      expect(divide(1e10, 1e5)).toBe(1e5);
    });
  });

  describe('Error Conditions', () => {
    test('should throw error on division by zero', () => {
      expect(() => divide(10, 0)).toThrow('Division by zero');
    });

    test('should throw error on division by zero with negative dividend', () => {
      expect(() => divide(-10, 0)).toThrow('Division by zero');
    });
  });

  describe('Boundary Values', () => {
    test('should handle division by 1', () => {
      expect(divide(10, 1)).toBe(10);
    });

    test('should handle division by -1', () => {
      expect(divide(10, -1)).toBe(-10);
    });
  });
});
```

**Report**:
```
Test Cases Generated: 10
Coverage Areas:
  ✅ Normal cases (3 tests)
  ✅ Edge cases (3 tests)
  ✅ Error conditions (2 tests)
  ✅ Boundary values (2 tests)

Estimated Coverage: 100%
```

## What Gets Generated

### Test Categories
- ✅ Normal usage scenarios
- ✅ Edge cases and unusual inputs
- ✅ Error conditions and exceptions
- ✅ Boundary values (min/max)
- ✅ Null/undefined handling
- ✅ Integration with mocked dependencies

### Test Structure
- ✅ Proper imports and setup
- ✅ describe/test blocks (or equivalent)
- ✅ Mock setup (beforeEach/afterEach)
- ✅ Assertions with appropriate matchers
- ✅ Cleanup hooks

### Advanced Features
- ✅ Data-driven tests (parametrized)
- ✅ Async/await handling
- ✅ Snapshot testing (for complex objects)
- ✅ Mock setup for dependencies

## Requirements

- Claude Code CLI
- Testing framework installed (Jest, pytest, etc.)
- Source code to test

## License

GPL-3.0

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
