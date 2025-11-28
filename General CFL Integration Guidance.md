Integrating the Coda Formula Language (for Coda.io) into Google Antigravity to create a custom IDE experience involves two distinct layers:

1.  **The Visual Layer (The "IDE"):** Teaching the editor how to highlight and format the code.
2.  **The Intelligence Layer (The "Agent"):** Teaching the Antigravity agents how to understand and write the formulas for you.

Since Antigravity is built on top of VS Code, you can leverage standard VS Code extension methods for the visual layer while using Antigravity's specific agentic capabilities for the intelligence layer.

### **Phase 1: The Visual Layer (Syntax Highlighting)**

You need to create a lightweight VS Code extension to give Antigravity the ability to "read" Coda formulas visually.

**1. Scaffold the Extension**
Open your terminal and use the standard VS Code generator (yeoman) to create a new language support extension:

```bash
npm install -g yo generator-code
yo code
# Select "New Language Support"
# Name it "Coda Formulas"
# Extension: .coda (or .cfl)
```

**2. Define the Grammar (`syntaxes/coda.tmLanguage.json`)**
Coda’s language doesn't have a public grammar file, so you will define a basic one using its "Nouns (Objects) and Verbs (Functions)" structure. Replace the generated grammar content with this structure:

```json
{
  "scopeName": "source.coda",
  "patterns": [
    {
      "comment": "Functions (Verbs)",
      "match": "\\b(Filter|Count|ToText|List|If|Switch|Concatenate|User|Now|Today)\\b",
      "name": "support.function.coda"
    },
    {
      "comment": "Objects/Tables (Nouns) - customized regex for your specific tables",
      "match": "\\b([A-Z][a-zA-Z0-9_]*)\\b",
      "name": "variable.other.object.coda"
    },
    {
      "comment": "Operators",
      "match": "(\\.|\\+|\\-|\\*|\\/|=|!=|>=|<=|&&|\\|\\|)",
      "name": "keyword.operator.coda"
    },
    {
      "comment": "Strings",
      "begin": "\"",
      "end": "\"",
      "name": "string.quoted.double.coda"
    }
  ]
}
```

  * **Tip:** You can expand the `match` list for functions by scraping the Coda formula list.

**3. Install into Antigravity**

1.  Package the extension: `vsce package` (you may need to install `vsce` via npm).
2.  In Antigravity, go to the **Extensions** view.
3.  Click the `...` menu -\> **Install from VSIX...** and select your `.vsix` file.

-----

### **Phase 2: The Intelligence Layer (Agent Context)**

This is where Antigravity shines. You don't "program" the agent; you "onboard" it. You need to give the agent a reference manual so it knows *how* to write the formulas.

**1. Create a Knowledge Base (Context)**
Antigravity agents are excellent at reading files in your workspace to gain context.

1.  Create a folder in your project root called `coda-context/` or `reference/`.
2.  Create markdown files containing the documentation for Coda formulas.
      * **Why Markdown?** LLMs digest it easily.
      * **Content:** Copy/paste definitions from the [Coda Formula Reference](https://coda.io/formulas).
      * **Structure:**
          * `coda_math.md`: `Sum()`, `Average()`, `Round()`...
          * `coda_logic.md`: `If()`, `Switch()`, `IsBlank()`...
          * `coda_tables.md`: Explain how `thisRow` and `[Column Name]` work.

**2. Create a "System Prompt" via an Artifact**
Create a file named `AGENT_INSTRUCTIONS.md` in your root. Antigravity agents often prioritize top-level instruction files.

```markdown
# Coda Formula Maker Identity
You are an expert Coda.io Formula Engineer. 

## Rules
1. Always reference the documentation in the `coda-context/` folder before generating code.
2. Use "Dot Chaining" syntax (e.g., `Table.Filter(...)`) rather than wrapped syntax whenever possible.
3. When referencing columns, always wrap them in `[]` if they contain spaces.
4. If a formula involves a table filter, always check if `CurrentValue` or `thisRow` is more appropriate.
```

-----

### **Phase 3: The Workflow**

Now that you have the **Visuals** (extension) and the **Brains** (context files), here is your development loop:

1.  **Open Antigravity** to your project folder.
2.  **Create a new file** ending in `.coda` (e.g., `revenue_calc.coda`).
3.  **Open the Agent / Chat panel** and verify it sees your `coda-context` folder.
4.  **Prompt:**
    > "Look at `coda_logic.md` and write a formula that filters the 'Sales' table for rows where 'Status' is 'Closed' and the 'Date' is within the last 30 days. Format it using dot-chaining."
5.  **Result:** The agent will generate the code. Because of Phase 1, it will be syntax-highlighted. Because of Phase 2, it will be syntactically correct for Coda.

### **Next Step**

Would you like me to generate the full `package.json` and a more complete list of Coda functions (extracted from their docs) so you can copy-paste the VS Code extension code directly?