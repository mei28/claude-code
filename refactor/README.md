# Refactor - Code Quality Improvement Plugin

## Overview

Refactor is a Claude Code plugin that suggests and applies code refactoring improvements. It analyzes code quality metrics, identifies complexity issues, detects code smells, and provides actionable recommendations to reduce technical debt and enhance maintainability.

## What It Does

This plugin identifies and helps fix common code quality issues:

- **Complexity Reduction**: Reduces high cyclomatic complexity
- **Extract Method**: Breaks down long functions into smaller units
- **Remove Duplication**: Eliminates redundant code (DRY principle)
- **Polymorphism**: Replaces conditional logic with polymorphic patterns
- **Parameter Objects**: Simplifies long parameter lists
- **Magic Numbers**: Replaces hardcoded values with named constants

## Installation

```bash
/plugin install https://github.com/mei28/claude-code-commands/refactor
```

Or manually:
```bash
git clone https://github.com/mei28/claude-code-commands
ln -s $(pwd)/claude-code-commands/refactor ~/.claude/plugins/refactor
```

## Usage

Analyze recent changes:
```
/refactor
```

Refactor specific files:
```
/refactor src/services/orderService.ts
```

Get suggestions without changes:
```
/refactor --suggest
```

Apply automatic refactorings:
```
/refactor --apply
```

The plugin will:
1. Read and analyze code metrics
2. Identify refactoring opportunities
3. Prioritize by impact and effort
4. Show before/after examples
5. Optionally apply safe refactorings

## Example

**Before** - High Complexity (15):
```typescript
function calculatePrice(item, user, promotion) {
  let price = item.basePrice;

  if (user.isPremium) {
    if (user.loyaltyYears > 5) {
      price *= 0.85;
    } else if (user.loyaltyYears > 2) {
      price *= 0.9;
    } else {
      price *= 0.95;
    }
  }

  if (promotion) {
    if (promotion.type === 'percentage') {
      price *= (1 - promotion.value / 100);
    } else if (promotion.type === 'fixed') {
      price -= promotion.value;
    } else if (promotion.type === 'bogo') {
      if (item.quantity > 1) {
        price = price * 0.5 * item.quantity;
      }
    }
  }

  if (item.category === 'electronics') {
    if (item.warranty) {
      price += 49.99;
    }
  }

  return price;
}
```

**After** - Reduced Complexity (4):
```typescript
function calculatePrice(item, user, promotion) {
  let price = item.basePrice;
  price = applyUserDiscount(price, user);
  price = applyPromotion(price, promotion, item);
  price = addWarranty(price, item);
  return price;
}

function applyUserDiscount(price, user) {
  if (!user.isPremium) return price;

  const discounts = {
    5: 0.85,
    2: 0.9,
    0: 0.95
  };

  const discount = Object.entries(discounts)
    .find(([years]) => user.loyaltyYears >= Number(years))?.[1] ?? 1;

  return price * discount;
}

function applyPromotion(price, promotion, item) {
  if (!promotion) return price;

  const strategies = {
    percentage: (p, promo) => p * (1 - promo.value / 100),
    fixed: (p, promo) => p - promo.value,
    bogo: (p, promo, itm) => itm.quantity > 1 ? p * 0.5 * itm.quantity : p
  };

  return strategies[promotion.type]?.(price, promotion, item) ?? price;
}

function addWarranty(price, item) {
  return item.category === 'electronics' && item.warranty
    ? price + 49.99
    : price;
}
```

**Improvements**:
- ✅ Complexity: 15 → 4 (-73%)
- ✅ Easier to test (4 small functions)
- ✅ Easier to extend (add new discount tiers)
- ✅ Single responsibility per function

## What Gets Detected

### Code Quality Issues
- ✅ High cyclomatic complexity (>10)
- ✅ Long functions (>50 lines)
- ✅ Deep nesting (>4 levels)
- ✅ Code duplication
- ✅ Long parameter lists (>5)
- ✅ Magic numbers
- ✅ Inconsistent naming

### Refactoring Patterns
- ✅ Extract Method
- ✅ Extract Constant
- ✅ Introduce Parameter Object
- ✅ Replace Conditional with Polymorphism
- ✅ Remove Dead Code
- ✅ Simplify Conditionals
- ✅ Reduce Nesting

### Metrics Tracked
- Cyclomatic complexity
- Function length
- Code duplication percentage
- Nesting depth
- Maintainability index

## Requirements

- Claude Code CLI
- Source code to analyze
- Tests recommended (for safe refactoring)

## License

GPL-3.0

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
