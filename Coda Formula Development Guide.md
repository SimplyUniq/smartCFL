# Introduction to Coda’s Formula Syntax Guide

This guide provides a comprehensive overview of the foundational concepts in Coda's Formula Language (CFL), based on the official resource [Introduction to Coda’s Formula Syntax](https://coda.io/resources/guides/intro-to-codas-formula-syntax). It introduces the language's structure, syntax options, and key elements like objects, functions, and chips, helping users build a strong foundation for creating dynamic calculations and automations in Coda docs.

CFL draws inspiration from spreadsheet formulas (e.g., Excel) and programming (e.g., JavaScript), offering flexibility without rigid rules. This document is structured to mirror the original guide for clarity, with preserved examples, code snippets, and explanations. For the full formula library, refer to the [Coda Formula Dictionary](https://coda.io/formulas).

## What's in This Guide

- An understanding of Coda's formula language.
- An introduction to chaining vs. wrapping syntax.
- The basics of formula chips.

## Tools You'll Use
- Formula builder.
- Dot operator (`.`).
- Formula chips.

## The Coda Formula Language Explained

The Coda formula language is similar to spoken or written words—it's a language. This means that although there are rules to improve efficiency and comprehension, there is no one singular way to accomplish anything. Think about all the ways you might greet someone: “Hello,” “hey there,” and “howdy” all look different, but they accomplish the same thing linguistically. You might choose one over the other depending on context: where you are, who you’re speaking to, etc.

When you’re working with the Coda formula language, your way of writing might differ from the way other makers write their formulas—and that’s okay! The other thing to remember is that you don’t need to know every word in the dictionary in order to be a proficient speaker, and the same goes for the Coda formula language. You don’t need to know every formula to be successful, but we do have our [formula dictionary](https://coda.io/formulas) should you ever need it 🧠.

### 1. Breaking Down a Coda Formula

Coda formulas are made up of two major components: **objects** and **functions**. To stay with our language analogy, you can think of objects as nouns and functions as verbs.

#### Objects
If you’ve ever used Excel or Google Sheets, you may be used to using coordinates to pinpoint a cell. In Coda, all **objects** (like tables, rows, and buttons) have names. No coordinates needed! Simply type the name of the object you want to reference. Objects hold the data we want to work with:

- A table is an object.
- A column is an object.
- A row is an object.

**Example**: Instead of `A1`, reference `Produce.Name` to access the Name column in the Produce table.

#### Functions
Back to the sentence metaphor, functions (sometimes called formulas) are the verbs. They *do* stuff. Functions are things that we want to do to or with the given object:

- `Filter()`: Filter the given dataset down based on specific criteria.
- `Count()`: Count the given dataset.
- `toText()`: Convert the given dataset to plain text values.

**Example**:
```
Produce.Filter(Fruit or Vegetable = "Fruit").Name
```
This filters the Produce table for fruits and extracts their names.

### 2. Formula Chips

Your objects will show up as **chips** in your formulas. When you click on a chip, you can learn more about that specific object. When we click on the **Fruit** chip in a formula example, we can see that this is an option in the **Fruit or Vegetable** column in the **Produce** table.

#### Color Coding Tells You the Location
Formula chips of the same color mean that those objects are located in the same table. Take a look at this example. Based on the color of the chips, you can see that Produce and Fruit or Vegetable are part of the same table, and `thisRow.Category` is part of the **Categories** table.

**Visual Tip**: Same-color chips indicate intra-table relationships, making it easy to track data flow.

#### Icons Tell You the Type and Quantity of Data
Take a look at the reference table for icons. These icons will be at the far-right of each chip in your formulas, and they will note what **type** of data you're working with. The icon will also tell you whether you are referencing a **singular** value, a **list** of values, or an array of values. Notice the “stacked” icons for lists:

| Icon Type | Description | Example |
|-----------|-------------|---------|
| 📝 | Single text | `thisRow.Name` |
| 📝 (stacked) | List of text | `Produce.Name` (multiple rows) |
| 🔢 | Single number | `thisRow.Price` |
| 🔢 (stacked) | List of numbers | `Produce.Price` |
| 📅 | Single date | `thisRow.Due Date` |
| 📅 (stacked) | List of dates | `Tasks.Due Date` |
| 👤 | Single person/user | `User().Name` |
| 👤 (stacked) | List of people | `Team.Members` |
| ✅/❌ | Boolean (true/false) | `thisRow.Complete` |
| 🗂️ | Row or page | `thisRow` |

These icons provide quick visual feedback in the formula builder.

### 3. Formula Syntax

The Coda formula language is a little bit Excel, a little bit JavaScript. What we mean by that is that you can choose to use the **wrapping** method or the **chaining** method while writing your formulas.

#### Wrapping
In Excel’s formula language, you use a lot of parentheses. This is called **wrapping**. This syntax is totally valid in the Coda formula language, but as your formulas become longer and more complex, this method can become a bit difficult to read as the number of parentheses increases.

**Example** (Wrapping):
```
Filter(Produce, Fruit or Vegetable = "Fruit")
```

#### Chaining
In Coda, you can also get the same answer this way 👉 This is called **chaining**. The chaining method allows you to write your formulas in a more sentence-structured way, similar to JavaScript syntax.

**Example** (Chaining):
```
Produce.Filter(Fruit or Vegetable = "Fruit")
```

Either way works! It all comes down to personal preference and what feels best to you 👍.

#### Parentheses
Much like in math, things inside of parentheses can be viewed as one statement, or one sentence. Coda is going to look at that one statement and evaluate it as a whole. In lengthy formulas, parentheses will help note where one sentence ends and the next begins. You can click on a parenthesis to see its highlighted pair. This will show you where your sentence begins and ends.

Additionally, just like in math problems, you'll use parentheses to separate multiple `AND` and `OR` functions so that all of your calculations happen in the right order. Coda will calculate anything inside of parentheses first.

**Example** (Math Order):
```
(2*2)/(4+4)  // Evaluates to 1
```

**Example** (Logic Grouping):
```
(Condition1 AND Condition2) OR Condition3
```

In this example, we will multiply 2 times 2 and add 4 plus 4 before doing the division. In the same way, use parentheses to specify how multiple `AND` or `OR` functions should be grouped. By default, the formula applies the logic from left to right in the order that it appears. If you want to specify a specific order, just use parentheses 😉.

#### The Dot Operator
With the help of the **dot operator**, you can use the chaining method to write formulas for better readability. Chaining separates steps in your formula by using a dot operator, which is just a fancy descriptor for a **period:** `"."` At its most basic level, chaining with the **dot operator** looks like this:

**Example**:
```
thisDocument.Modified()
```

In addition to the dot operator, you can use the following operators within your formulas:

| Operator | Symbol(s) | Description |
|----------|-----------|-------------|
| Equal to | `=` | Checks equality. |
| Not equal to | `!=` | Checks inequality. |
| Less than | `<` | Numerical/text comparison. |
| Greater than | `>` | Numerical/text comparison. |
| Less than or equal to | `<=` | Inclusive lower bound. |
| Greater than or equal to | `>=` | Inclusive upper bound. |
| And | `&&` or `AND` (not case-sensitive) | Logical AND. |
| Or | `||` or `OR` (not case-sensitive) | Logical OR. |

**Tip**: Use chaining with the dot operator for readability in complex formulas, especially when combining multiple functions.

## Now What? Next Steps

Now that you’ve learned the basics of the Coda formula language, check out these other resources to keep flexing those formula muscles 💪 🧠:

- [Coda Formula Dictionary](https://coda.io/formulas): Full list of hundreds of formulas.
- [Basics of Coda Formulas](https://help.coda.io/hc/en-us/articles/39555858394637-Basics-of-Coda-formulas): Deeper dive into getting started.
- [Top Five Formulas You Need to Know](https://coda.io/resources/guides/the-top-five-formulas-you-need-to-know): Essential functions like Filter() and User().
- [Writing a Formula in Coda](https://coda.io/resources/guides/writing-a-formula-in-coda): Hands-on with the formula builder.
- [Formulas 101 Course](https://coda.io/resources/courses/formulas-101): Interactive learning path.
- [Coda Community Forum](https://community.coda.io): Share and learn from other makers.

This guide equips Antigravity AI agents with the syntax fundamentals for parsing and generating CFL expressions in automated doc workflows. For advanced topics like performance optimization or integration with Packs, explore the linked resources. Update as CFL evolves via official Coda documentation.