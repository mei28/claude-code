# Deslop - AI Code Cleanup Plugin

## Overview

Deslop is a Claude Code plugin that detects and removes unnecessary additions in AI-generated code, helping maintain codebase consistency and following the YAGNI (You Aren't Gonna Need It) principle.

## What It Does

AI code generators often add:
- Excessive comments explaining obvious code
- Over-defensive error handling for exceptions that can't occur
- Unnecessary abstractions and helper functions
- Code that doesn't match existing project style

Deslop analyzes your existing codebase patterns and identifies these issues in AI-generated code, providing specific recommendations for cleanup.

## Installation

```bash
/plugin install https://github.com/mei28/claude-code/deslop
```

Or manually:
```bash
git clone https://github.com/mei28/claude-code
ln -s $(pwd)/claude-code/deslop ~/.claude/plugins/deslop
```

## Usage

Simply invoke the command when reviewing AI-generated code:

```
/deslop
```

The plugin will:
1. Analyze your existing codebase style
2. Review the AI-generated code
3. Identify inconsistencies and unnecessary additions
4. Provide specific improvement recommendations
5. Offer cleaned-up code versions

## Example

**Before** (AI-generated code):
```python
# Get the user's name
name = user.get_name()  # Call get_name method

# Check if name exists
if name:  # Verify name is not empty
    try:
        # Display the name
        print(name)  # Output to console
    except Exception as e:
        logger.error(f"Error: {e}")
```

**After** (Deslop cleanup):
```python
name = user.get_name()
if name:
    print(name)
```

## What Gets Detected

- ✅ Excessive comments
- ✅ Over-defensive error handling
- ✅ Unnecessary abstractions
- ✅ Style inconsistencies
- ✅ Violations of YAGNI/DRY/KISS principles

## Requirements

- Claude Code CLI
- Existing codebase to compare against

## License

GPL-3.0

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
