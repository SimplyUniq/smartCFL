# Coda Formula Language (CFL) Documentation

This document provides a comprehensive overview of the Coda Formula Language (CFL), compiled from official Coda resources including guides, help articles, and introductory materials. CFL is a powerful, flexible language that blends elements of spreadsheet formulas (like Excel) and programming syntax (like JavaScript). It enables dynamic calculations, data manipulation, automation, and interactivity in Coda docs.

CFL is designed for makers—users building collaborative documents, tables, buttons, and automations—allowing you to reference named objects (tables, columns, rows) without coordinates. Formulas can be added to canvas elements, table columns, buttons, filters, and more.

For the complete, up-to-date formula library (hundreds of functions), refer to the official [Coda Formula Library](https://coda.io/formulas). This document focuses on foundational concepts, syntax, tools, and essential functions, with examples.

## 1. Introduction to CFL

The Coda Formula Language is akin to a spoken language: it has rules for efficiency and comprehension, but no single "correct" way to express ideas. You don't need to master every formula to be proficient—just like you don't need the entire dictionary to converse fluently.

### Key Concepts
- **Objects (Nouns)**: Data holders like tables, columns, rows, documents, or users. Everything in Coda has a name, making references intuitive (e.g., `Produce.Name` instead of `A1`).
- **Functions (Verbs)**: Actions performed on objects, such as filtering, counting, or converting data.
- **Chips**: Visual representations of objects in formulas. They show color-coded locations (same table = same color), icons for data types, and quantity (single vs. list/array).

### Data Types and Icons
Formula chips use icons to indicate types and quantity:
- **Text**: 📝 (single) or stacked for lists.
- **Number**: 🔢 (single) or stacked.
- **Date**: 📅 (single) or stacked.
- **Person/User**: 👤 (single) or stacked.
- **Boolean**: ✅/❌ (true/false).
- **List/Array**: Stacked icons indicate multiple values.
- **Row/Page**: 🗂️ or similar for structured data.

### Where Formulas Live
- **Canvas**: Type `=` to start.
- **Table Columns**: Right-click column header > **Calculate** > *f* icon for formula editor.
- **Buttons/Automations/Controls**: Access via settings.
- **Filters/Conditional Formatting**: Use the *f* icon.

## 2. Formula Syntax

CFL supports two styles: **wrapping** (Excel-like, parenthesis-heavy) and **chaining** (JavaScript-like, readable sentences). Both yield the same result—choose based on preference.

### Wrapping (Parenthesis-Style)
Nest functions inside parentheses:
```
Modified(thisDocument)
```
As formulas grow complex, parentheses multiply, reducing readability.

### Chaining (Dot Operator)
Use `.` to chain actions like a sentence:
```
thisDocument.Modified()
```
Example:
```
Produce.Filter(Fruit or Vegetable = "Fruit").Name
```
This filters the `Produce` table for fruits and extracts names.

### Parentheses for Grouping
- Treat contents as a single unit (evaluated first).
- Use for order in math/logic: `(2*2)/(4+4) = 0.5`.
- Group `AND`/`OR` conditions: `(Condition1 AND Condition2) OR Condition3`.
- Click a parenthesis to highlight its pair.

### Operators
- **Equality**: `=`, `!=` (not equal).
- **Comparison**: `<`, `>`, `<=`, `>=`.
- **Logical**: `&&` or `AND` (not case-sensitive), `||` or `OR`.
- **Dot (.)**: Chains methods/properties.

### Comments
Add notes for clarity:
- Single-line: `// This is a comment.`
- Multi-line: `/* This spans multiple lines. */`

### Auto-Formatting
In the expanded formula builder, click **Auto-format** to indent and structure long formulas.

## 3. The Formula Builder

The formula builder is your primary interface for writing CFL. It's intelligent, with auto-complete and error detection.

### Opening the Builder
- **Canvas**: Type `=`, then formula. Press `Esc` to cancel.
- **Table Column**: Column header > **Calculate** > *f* icon. Choose "Custom formula" for full control.
- **Other**: *f* icons in buttons, filters, etc.

### Features
- **Auto-Suggestions**: As you type, suggestions appear for objects/functions (e.g., typing "Prod" suggests `Produce` table).
- **Formula Details**: Hover/select a function for inputs, outputs, and examples.
- **Error Handling**: Red squiggles highlight issues; tooltips explain (e.g., missing argument). See [Troubleshooting Formulas](https://help.coda.io/hc/en-us/articles/39555735651341-Troubleshoot-your-formulas) for tips.
- **Expand Modal**: Click expand icon for more space; includes auto-format.
- **Named Formulas**: Click **Add Name** to reuse formulas doc-wide (like variables). Reference as `MyNamedFormula`.

### Best Practices
- Break complex formulas into named sub-formulas.
- Use chaining for readability.
- Test incrementally to avoid errors.
- Optimize for performance: Avoid redundant calculations in large tables.

## 4. Essential Functions

While CFL has hundreds of functions, start with these five most-used. They cover filtering, personalization, row context, searching, and logic. Full details in the [Formula Library](https://coda.io/formulas).

### 1. Filter()
Filters a list (e.g., table/column) based on criteria. Output: Filtered list.

**Structure**:
```
[Table].Filter([Criteria]).[Action]
```
- **Inputs**: List to filter, condition (e.g., `Column = Value`).
- **Outputs**: Filtered list; chain with `.Count()`, `.FormulaMap()`, etc.

**Example** (List fruits from `Produce` table):
```
Produce.Filter(Fruit or Vegetable = "Fruit").Name
```
**Use Cases**: Dynamic views (e.g., "My Tasks"), aggregations.

### 2. User()
Returns the current user's info (name, email, avatar).

**Structure**:
```
User().Property
```
- **Properties**: `.Name`, `.Email`, `.Photo`.

**Example** (Greeting):
```
Concatenate("Welcome, ", User().Name, "!")
```
**Use Cases**: Personalized views, auto-assignment (e.g., `Filter(Tasks, Assignee = User())`).

### 3. thisRow
References the current row's context in table formulas. Treats rows as units (not cells).

**Structure**:
```
thisRow.Property
```
- **Properties**: Column names (e.g., `thisRow.Name`).

**Example** (Pull project due date):
```
thisRow.Project.Due Date
```
**Use Cases**: Row-specific calculations, lookups (e.g., `thisRow.Category.Count()`).

### 4. Contains()
Checks if a list includes a value. Returns `true`/`false`.

**Structure**:
```
List(...).Contains(Value)
```
**Example**:
```
List("Dog", "Giraffe").Contains("Dog")  // true
```
**Use Cases**: With `Filter()` for multi-selects (e.g., `Filter(Tasks, Status.Contains("In Progress"))`).

### 5. If() and SwitchIf()
Handle conditional logic.

**If() Structure**:
```
If(Condition, True Value, False Value)
```
**Example** (Compare counts):
```
If(Produce.Filter(Fruit or Vegetable = "Vegetable").Count() > Produce.Filter(Fruit or Vegetable = "Fruit").Count(), "More veggies! 🥦", "More fruits! 🍎")
```

**SwitchIf() Structure** (Multi-condition with fallback):
```
SwitchIf(Condition1, Value1, Condition2, Value2, ..., Fallback)
```
**Example** (Time-based greeting):
```
SwitchIf(Today() > Date(2030, 1, 20), "Future!", Year(Today()) = 2025, "Present!", "Past!")
```
**Use Cases**: Dynamic text, routing logic. Prefer `SwitchIf()` over nested `If()` for multiples.

## 5. Common Patterns and Examples

### Basic Calculations
- Count rows: `Produce.Count()`.
- Sum: `Produce.Sum(Price)`.
- Concatenate: `Concatenate("Item: ", thisRow.Name)`.

### Date Handling
- Today: `Today()`.
- Workdays: `NetWorkingDays(Start, End)` (custom holidays configurable).

### Text Manipulation
- To text: `thisRow.Name.ToText()`.
- Compose: Use in text columns for dynamic content (e.g., `=If(thisRow.Status = "Done", "✅", "⏳")`).

### Lists and Arrays
- Create list: `List("A", "B", "C")`.
- Map over list: `[List].FormulaMap(Transform)`.

### Advanced: Named Formulas
Define once, reuse everywhere:
1. Canvas formula: `Total Fruits = Produce.Filter(Fruit or Vegetable = "Fruit").Count()`.
2. Reference: `Total Fruits` in other formulas.

## 6. Performance and Troubleshooting

### Optimization
- Use `thisTable` for current table references.
- Cache repeats with named formulas.
- Avoid volatile functions (e.g., `Now()`) in tables.
- Monitor "Calculating" status; simplify heavy filters.

### Common Errors
- **Mismatched Types**: Ensure inputs match (e.g., text vs. number).
- **Missing Args**: Check function details.
- **Circular References**: Formulas referencing each other cyclically.
- **Tip**: Break into parts, test each.

### Debugging
- Use `ToText()` to inspect values.
- Expanded builder shows line-by-line evaluation.

## 7. Further Resources
- [Official Formula Library](https://coda.io/formulas): Searchable list of all functions by category (e.g., Aggregation, Date, Text, Math).
- [Basics Guide](https://help.coda.io/hc/en-us/articles/39555858394637-Basics-of-Coda-formulas).
- [Syntax Intro](https://coda.io/resources/guides/intro-to-codas-formula-syntax).
- [Formula Builder Guide](https://coda.io/resources/guides/writing-a-formula-in-coda).
- [Top Formulas Guide](https://coda.io/resources/guides/the-top-five-formulas-you-need-to-know).
- [Troubleshooting](https://help.coda.io/hc/en-us/articles/39555735651341-Troubleshoot-your-formulas).
- [Formulas 101 Course](https://coda.io/resources/courses/formulas-101).
- Community: [Coda Community Forum](https://community.coda.io) for advanced tips.

This documentation equips an Antigravity AI agent with CFL fundamentals for doc automation, data analysis, and dynamic content generation. For agent-specific integrations, extend with Packs or API calls. Update periodically via the official library, as CFL evolves.