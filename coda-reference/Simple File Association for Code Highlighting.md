Since **Google Antigravity** is built on top of VS Code, you can use the "File Association" trick. This is the fastest "no-code/no-build" way to get 90% of the functionality instantly.

Because the Coda Formula Language shares a very similar structure with JavaScript (dot-chaining objects and functions), you can trick the editor into treating your Coda files as JavaScript.

### **Method 1: The "File Association" Cheat (Instant)**
This forces Antigravity to apply JavaScript syntax highlighting to your `.coda` files.

1.  Open your **Settings** (Cmd/Ctrl + `,`).
2.  Search for **"File Associations"**.
3.  Click **"Add Item"**.
    * **Item:** `*.coda`
    * **Value:** `javascript`
4.  **Result:** Your files will immediately light up.

**Why this works:**
* **Coda:** `Table.Filter(Column = "Value").Count()`
* **JS:** `Table.Filter(Column = "Value").Count()`
* **The Difference:** Coda uses `=` for equality, while JS uses it for assignment. The colors will still appear (variables will look like variables, strings like strings), giving you the visual structure you need without a custom grammar.



---

### **Method 2: The "Agentic" Build (The Antigravity Way)**
Since you are using Antigravity, you can use the Agent to do the "building" for you. This technically builds an extension, but *you* don't have to leave the editor or run terminal commands manually.

**Prompt the Agent in the Manager View:**
> "I need a VS Code extension that adds syntax highlighting for `.coda` files. It should treat `Filter`, `Count`, and `If` as functions, and things inside `[]` as variables. Please scaffold the extension, run the package command, and install the VSIX for me into this workspace."

Antigravity's agent has permission to run terminal commands and file operations. It can generate the `package.json` and `tmLanguage.json` files, run `vsce package`, and then install the resulting file, effectively automating Phase 1 completely.

### **Which should you choose?**
* **Use Method 1 (Association)** if you just want to write a quick formula right now and don't care if the `=` sign is colored slightly wrong.
* **Use Method 2 (Agent)** if you want a dedicated "Coda" icon and perfect highlighting but want the AI to do the heavy lifting.