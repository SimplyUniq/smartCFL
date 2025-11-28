# smartCFL - Coda Formula Language for Antigravity

A complete integration of Coda Formula Language (CFL) support into Google Antigravity, providing syntax highlighting and AI-powered formula generation for Coda Makers.

## Features

- 🎨 **Syntax Highlighting** - JavaScript-based syntax highlighting for `.coda` files
- 📚 **Comprehensive Documentation** - Complete CFL reference materials for AI agents
- 💡 **Example Formulas** - 3 levels of examples (basic, intermediate, advanced)
- 🤖 **AI Agent Integration** - Antigravity agents can generate CFL from natural language
- ✅ **Validated** - Tested agent capabilities with 8-task validation suite

## Quick Start

### 1. Configure File Association

Enable syntax highlighting for `.coda` files:

1. Open Antigravity Settings (`Cmd + ,` on Mac, `Ctrl + ,` on Windows/Linux)
2. Search for **"File Associations"**
3. Click **"Add Item"**
4. Set: `*.coda` → `javascript`

See [FILE-ASSOCIATION-SETUP.md](FILE-ASSOCIATION-SETUP.md) for detailed instructions.

### 2. Explore Examples

Open the example files to see syntax highlighting in action:

- [`examples/basic-formulas.coda`](examples/basic-formulas.coda) - Filter, Count, basic operations
- [`examples/intermediate-formulas.coda`](examples/intermediate-formulas.coda) - thisRow, User(), conditionals
- [`examples/advanced-formulas.coda`](examples/advanced-formulas.coda) - Chaining, named formulas, optimization

### 3. Test AI Agent

Use the validation prompt to test Antigravity's CFL generation:

```
See EXAMPLE-VALIDATION-PROMPT.md for a quick 5-task test
```

## Repository Structure

```
smartCFL/
├── README.md                           # This file
├── FILE-ASSOCIATION-SETUP.md           # Setup instructions
├── EXAMPLE-VALIDATION-PROMPT.md        # Quick agent test
├── coda-reference/                     # CFL documentation
│   ├── Coda Formula Language Documentation.md
│   ├── Coda Formula Development Guide.md
│   ├── General CFL Integration Guidance.md
│   └── Simple File Association for Code Highlighting.md
├── examples/                           # Example .coda files
│   ├── basic-formulas.coda
│   ├── intermediate-formulas.coda
│   └── advanced-formulas.coda
└── validation/                         # Agent testing
    ├── agent-prompt.md                 # 8-task validation suite
    └── test-results.md                 # Validation results
```

## How It Works

### Syntax Highlighting

CFL shares structural similarities with JavaScript:
- Dot-chaining: `Table.Filter(...).Count()`
- Function calls with parentheses
- String literals and operators

By mapping `.coda` files to JavaScript, we get ~90% accurate syntax highlighting without building a custom extension.

### AI Agent Integration

The `coda-reference/` directory contains comprehensive CFL documentation that Antigravity agents reference when generating formulas. This enables:

- Natural language → CFL formula generation
- Best practices application (chaining syntax, named formulas)
- Contextual understanding (thisRow, User(), table relationships)

## Example Formulas

### Basic Filtering
```coda
// Show all fruits from produce table
Produce.Filter(Fruit or Vegetable = "Fruit").Name
```

### Personalized View
```coda
// My incomplete tasks
Tasks.Filter(Assignee = User() AND Status != "Done")
```

### Conditional Logic
```coda
// Status indicator
SwitchIf(
  thisRow.Priority = "Critical", "🔴 Critical",
  thisRow.Priority = "High", "🟠 High",
  thisRow.Priority = "Medium", "🟡 Medium",
  "🟢 Low"
)
```

### Advanced Chaining
```coda
// Active projects due soon
Projects
  .Filter(Status = "Active")
  .Filter(Owner = User())
  .Filter(Due Date < Today().AddDays(7))
  .Sort(false, Due Date)
  .Name
```

## Validation Results

The AI agent successfully passed all validation tests:

✅ Syntax Correctness - Proper CFL syntax with chaining  
✅ Documentation Reference - Appropriate doc references  
✅ Best Practices - Named formulas, SwitchIf over nested If  
✅ Contextual Understanding - Correct use of thisRow, User(), relationships  
✅ Completeness - All 8 tasks completed with explanations

See [validation/test-results.md](validation/test-results.md) for details.

## CFL Quick Reference

### Essential Functions
- `Filter()` - Filter lists based on criteria
- `Count()` - Count items in a list
- `User()` - Get current user information
- `thisRow` - Reference current row context
- `Contains()` - Check list membership
- `If()` / `SwitchIf()` - Conditional logic

### Operators
- Equality: `=`, `!=`
- Comparison: `<`, `>`, `<=`, `>=`
- Logical: `AND` / `&&`, `OR` / `||`
- Dot operator: `.` (for chaining)

## Resources

- [Official Coda Formula Library](https://coda.io/formulas)
- [Coda Community Forum](https://community.coda.io)
- [Formulas 101 Course](https://coda.io/resources/courses/formulas-101)

## Use Cases

- **Formula Development** - Write and test Coda formulas with syntax highlighting
- **Learning CFL** - Study examples at different complexity levels
- **AI-Assisted Development** - Generate formulas from natural language descriptions
- **Documentation** - Reference comprehensive CFL guides within your IDE

## Requirements

- Google Antigravity (VS Code-based)
- File association configuration (one-time setup)

## Contributing

This workspace demonstrates CFL integration into Antigravity. To extend:

1. Add more example formulas to `examples/`
2. Enhance documentation in `coda-reference/`
3. Create additional validation scenarios
4. Share your CFL patterns and best practices

## License

This project contains documentation and examples for educational purposes. Coda Formula Language is property of Coda.io.

## Acknowledgments

- Built for Google Antigravity
- CFL documentation based on official Coda resources
- Syntax highlighting uses VS Code file association method

---

**Ready to build Coda formulas with AI assistance?** Configure the file association and start exploring the examples!
