# Example Agent Validation Prompt

This is a simplified example prompt you can use to validate that an Antigravity agent can build Coda Formula Language (CFL) from scratch.

## Quick Validation Prompt

**Copy and paste this prompt to test the agent:**

---

I'm working on a Coda doc for project management. I have a **Tasks** table with these columns:
- Name (text)
- Status (select: Not Started, In Progress, Done, Blocked)
- Priority (select: Low, Medium, High, Critical)
- Assignee (person)
- Due Date (date)
- Project (relation to Projects table)
- Hours Estimated (number)

Please generate Coda Formula Language (CFL) formulas for the following. Reference the CFL documentation in the `coda-reference/` folder and use chaining syntax:

### 1. My Active Tasks
Show all tasks assigned to me that are not done yet, sorted by due date.

### 2. Overdue Count
Count how many tasks are overdue (due date is before today AND status is not "Done").

### 3. Status Indicator
Create a formula that shows:
- 🔴 "Overdue" if due date < today and status != Done
- 🟡 "Due Soon" if due date is within the next 3 days
- 🟢 "On Track" for everything else

### 4. High Priority Summary
Calculate the total estimated hours for all high-priority and critical tasks that aren't done yet.

### 5. Team Workload
For each person in the Assignee column, show their name and count of incomplete tasks.

---

## What to Look For

A successful agent response should:

1. ✅ **Use proper CFL syntax** - Chaining with dot operator, correct function names
2. ✅ **Reference documentation** - Mention files from `coda-reference/` folder
3. ✅ **Apply best practices** - Use Filter, User, thisRow, SwitchIf appropriately
4. ✅ **Explain reasoning** - Describe why specific functions were chosen
5. ✅ **Provide working formulas** - Syntactically correct CFL code

## Expected Formula Patterns

### Task 1 - Should use:
- `User()` for personalization
- `Filter()` with compound conditions
- `Sort()` for ordering

### Task 2 - Should use:
- `Filter()` with date comparison
- `Today()` function
- `Count()` aggregation

### Task 3 - Should use:
- `SwitchIf()` or nested `If()`
- `Today()` and `AddDays()`
- Conditional logic with dates

### Task 4 - Should use:
- `Filter()` with OR conditions for priority
- `Sum()` aggregation
- Proper field references

### Task 5 - Should use:
- `Unique()` to get distinct assignees
- `FormulaMap()` to transform list
- `Filter()` and `Count()` combination

## Testing the Results

1. Copy generated formulas into a `.coda` file
2. Verify syntax highlighting works
3. Check that formulas follow CFL conventions
4. Confirm agent referenced the documentation

---

## Full Validation Suite

For comprehensive testing, use the complete validation prompt at:
[validation/agent-prompt.md](file:///Users/billfrench/Desktop/Manual%20Library/smartCFL/validation/agent-prompt.md)

This includes 8 detailed tasks covering:
- Basic filtering
- Personalized views
- Conditional logic
- Aggregations
- Advanced chaining
- Named formulas
- Button actions
- Complex lookups
