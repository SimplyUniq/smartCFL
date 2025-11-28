# Antigravity Agent CFL Generation Validation Prompt

This prompt is designed to validate that an Antigravity agent can successfully understand and generate Coda Formula Language (CFL) code from natural language requirements.

## Validation Scenario

You are working on a Coda doc that tracks a product inventory and sales pipeline. The doc contains the following tables:

### Tables Structure

**Products Table**
- Name (text)
- Category (select: Electronics, Clothing, Food, Home)
- Price (number)
- Stock Quantity (number)
- Supplier (text)
- Last Restocked (date)

**Sales Table**
- Product (relation to Products)
- Quantity Sold (number)
- Sale Date (date)
- Salesperson (person)
- Total Amount (number - calculated)
- Status (select: Pending, Completed, Cancelled)

**Categories Table**
- Name (text)
- Description (text)
- Target Margin (number - percentage)

## Validation Tasks

Please generate CFL formulas for the following requirements. For each task, explain your approach and reference the appropriate CFL documentation from the `coda-reference/` folder.

### Task 1: Basic Filtering
Create a formula that displays all products in the "Electronics" category that have a stock quantity less than 10.

**Expected Output Format:** List of product names

### Task 2: Personalized View
Create a formula for a salesperson's dashboard that shows only their completed sales from the last 30 days, sorted by sale date (most recent first).

**Expected Output Format:** Filtered and sorted list

### Task 3: Conditional Logic
Create a formula that assigns a status indicator to each product based on stock levels:
- "🔴 Critical" if stock < 5
- "🟡 Low" if stock >= 5 and < 20
- "🟢 Good" if stock >= 20

**Expected Output Format:** Text with emoji

### Task 4: Aggregation with Filtering
Create a formula that calculates the total revenue from completed sales in the "Electronics" category for the current month.

**Expected Output Format:** Single number

### Task 5: Advanced Chaining
Create a formula that:
1. Filters products by a specific category
2. Checks which products have been sold in the last 7 days
3. Returns the names of products that need restocking (stock < 10)
4. Sorts them by stock quantity (lowest first)

**Expected Output Format:** Sorted list of product names

### Task 6: Named Formula Pattern
Create a reusable named formula called "LowStockProducts" that can be referenced throughout the doc to identify products needing attention.

**Expected Output Format:** Formula definition and example usage

### Task 7: Button Action
Create a button formula that, when clicked, adds a new row to the Sales table with:
- Product: (user selects)
- Quantity Sold: 1
- Sale Date: Today's date
- Salesperson: Current user
- Status: "Pending"

**Expected Output Format:** Button action formula

### Task 8: Complex Lookup
For each sale in the Sales table, create a formula that looks up the product's category and calculates whether the sale price achieved the target margin for that category.

**Expected Output Format:** Boolean or text result

## Validation Criteria

A successful validation should demonstrate:

1. **Syntax Correctness**: Formulas use proper CFL syntax (chaining with dot operator, correct function names, proper operators)

2. **Documentation Reference**: Agent explicitly references the CFL documentation files when explaining formula construction

3. **Best Practices**: 
   - Uses chaining syntax for readability
   - Applies appropriate functions (Filter, User, thisRow, Contains, If/SwitchIf)
   - Considers performance (avoids redundant filters)

4. **Contextual Understanding**:
   - Understands table relationships
   - Correctly uses thisRow context
   - Applies User() for personalization
   - Uses proper date functions

5. **Completeness**: Provides working formulas for all 8 tasks with explanations

## How to Use This Prompt

1. Open Antigravity with the smartCFL workspace
2. Ensure the `coda-reference/` folder is accessible
3. Present this validation prompt to the agent
4. Review the generated formulas against the validation criteria
5. Test syntax highlighting by copying formulas into `.coda` files

## Expected Agent Behavior

The agent should:
- Reference files in `coda-reference/` for syntax rules and function definitions
- Generate syntactically correct CFL code
- Explain the reasoning behind formula construction
- Suggest alternatives when multiple approaches exist
- Highlight any assumptions made about the data structure
