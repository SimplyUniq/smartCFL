# File Association Configuration Instructions

To enable syntax highlighting for `.coda` files in Antigravity, you need to configure a file association manually through the settings interface.

## Steps to Configure

1. **Open Settings**
   - Mac: Press `Cmd + ,`
   - Windows/Linux: Press `Ctrl + ,`
   - Or: Click the gear icon in the bottom left → Settings

2. **Search for File Associations**
   - In the search bar at the top, type: `file associations`
   - Look for the setting: **Files: Associations**

3. **Add New Association**
   - Click **"Add Item"** button
   - In the **Item** field, enter: `*.coda`
   - In the **Value** field, enter: `javascript`
   - Press Enter or click OK

4. **Verify Configuration**
   - Open any `.coda` file from the `examples/` folder
   - You should see syntax highlighting applied
   - Functions, strings, and operators should be color-coded

## What This Does

This configuration tells Antigravity to treat all files with the `.coda` extension as JavaScript files for syntax highlighting purposes. Since CFL shares similar syntax patterns with JavaScript (dot-chaining, function calls, operators), this provides immediate visual structure without requiring a custom language extension.

## Expected Results

Once configured, opening files like `examples/basic-formulas.coda` should display:
- **Functions** highlighted (e.g., `Filter`, `Count`, `User`)
- **Strings** in a distinct color
- **Operators** (`.`, `=`, `&&`, `||`) highlighted
- **Comments** (`//` and `/* */`) in a muted color
- **Numbers** in a distinct color

## Limitations

This approach provides ~90% accuracy. Some CFL-specific syntax may not be perfectly highlighted:
- CFL uses `=` for equality (JS uses it for assignment)
- CFL column names with spaces in `[]` may not be perfectly recognized
- Some CFL-specific functions won't be recognized as keywords

These limitations are minor and don't impact the overall readability and usefulness of the syntax highlighting.

## Alternative: Custom Extension

If you need 100% accurate syntax highlighting, you would need to build a custom VS Code extension with a CFL-specific grammar. The file association method is recommended for quick setup and immediate productivity.

## Troubleshooting

**Highlighting not appearing?**
- Verify the file extension is exactly `.coda`
- Check that the association was saved correctly in settings
- Try closing and reopening the file
- Restart Antigravity if needed

**Wrong colors or highlighting?**
- Ensure the value is set to `javascript` (lowercase)
- Check your color theme supports JavaScript syntax
- Try a different color theme if needed
