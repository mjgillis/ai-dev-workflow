# Claude Product Development Workflows for Cursor

**Cursor-optimized version of Claude Product Development Workflows**

---

## What's Different in Cursor?

This is the same comprehensive workflow system, adapted for Cursor IDE:

- ✅ Uses `.cursorrules` file (Cursor's configuration format)
- ✅ Includes `@filename` reference syntax
- ✅ Optimized for Cursor Composer (Cmd+I) and Chat (Cmd+L)
- ✅ Same workflows, same templates, Cursor-specific instructions

---

## Quick Start for Cursor

### Installation

**Option 1: Copy .cursorrules to Project Root (Recommended)**

```bash
# In your project directory
cp /path/to/ai-dev-workflow/.cursor/.cursorrules .cursorrules

# Copy workflows for reference
cp -r /path/to/ai-dev-workflow/.cursor/workflows .cursor/workflows
cp -r /path/to/ai-dev-workflow/.cursor/reference .cursor/reference
```

**Option 2: Copy Entire .cursor Folder**

```bash
# Copy the whole .cursor folder to your project
cp -r /path/to/ai-dev-workflow/.cursor /path/to/your-project/

# Then copy .cursorrules to root
cp .cursor/.cursorrules .cursorrules
```

### That's It!

Cursor AI will automatically load `.cursorrules` when you:
- Open Cursor Chat (Cmd+L)
- Use Cursor Composer (Cmd+I)
- Ask questions or request code changes

---

## Workflow Commands for Cursor

Simply tell Cursor which workflow to use:

### Using Cursor Chat (Cmd+L)

```bash
# 1. Create PRD
"Create a PRD for [feature] using the prd-creation-workflow"

# 2. Create TDD
"Create a TDD for [feature] using the tdd-creation-workflow"

# 3. Break down into tickets
"Break down this PRD and TDD using the task-breakdown-workflow"

# 4. Implement a ticket
"Implement ticket [TICKET-ID] using the linear-ticket-workflow"
```

### Using Cursor Composer (Cmd+I)

For multi-file implementations:

```bash
# Reference workflow in Composer
"Following the linear-ticket-workflow, implement PROJ-42 across these files"

# Reference specific TDD sections
"Implement the API endpoint defined in TDD v2.1 Section 4.1"
```

### Referencing Files with @

Cursor can reference files with `@` syntax:

```bash
"Based on @.cursor/workflows/tdd-creation-workflow.md, design the architecture"

"Follow @.cursor/workflows/linear-ticket-workflow.md to implement this ticket"

"Show me @.cursor/reference/quick-reference.md"
```

---

## Complete Example in Cursor

```
You (Cmd+L): "I want to build an API usage dashboard using the prd-creation-workflow"

Cursor AI: [Guides you through PRD creation with questions]

You: "Now create a TDD using the tdd-creation-workflow"

Cursor AI: [Helps design technical architecture]

You: "Break this down using the task-breakdown-workflow"

Cursor AI: [Creates sprint plan with Linear tickets]

You (Cmd+I): "Implement ticket PROJ-1 using the linear-ticket-workflow"

Cursor AI: [Implements across multiple files with TDD approach]
```

---

## File Structure

```
your-project/
├── .cursorrules                 # Cursor configuration (auto-loaded)
├── .cursor/
│   ├── workflows/              # Detailed workflows (reference with @)
│   │   ├── prd-creation-workflow.md
│   │   ├── tdd-creation-workflow.md
│   │   ├── task-breakdown-workflow.md
│   │   └── linear-ticket-workflow.md
│   └── reference/              # Templates and quick reference
│       ├── quick-reference.md
│       ├── prd-template.md
│       ├── tdd-template.md
│       ├── task-breakdown-template.md
│       └── adr-template.md
└── src/
```

---

## Command Reference

Quick reference for Cursor workflow commands:

| When You Want To... | Say This in Cursor (Cmd+L or Cmd+I) |
|---------------------|--------------------------------------|
| Define requirements | `"Create a PRD for [feature] using the prd-creation-workflow"` |
| Design implementation | `"Create a TDD for [feature] using the tdd-creation-workflow"` |
| Break into tickets | `"Break down this PRD and TDD using the task-breakdown-workflow"` |
| Implement a ticket | `"Implement ticket [TICKET-ID] using the linear-ticket-workflow"` |
| See quick reference | `"Show me @.cursor/reference/quick-reference.md"` |

**Pattern:** Just say **"using the [workflow-name]"** and Cursor will load and follow it.

---

## Cursor-Specific Features

### 1. Multi-File Editing with Composer (Cmd+I)

```
"Using the linear-ticket-workflow, implement PROJ-42:
- Update API endpoint in api/routes.py
- Add tests in tests/test_api.py
- Update docs in README.md"
```

Cursor Composer will edit all files simultaneously following the workflow.

### 2. Inline References with @

```
"Based on @.cursor/workflows/tdd-creation-workflow.md Section 4.1,
implement the GET /api/v1/usage endpoint"
```

### 3. Chat History Context

Cursor Chat maintains conversation history, so you can:

```
You: "Create a PRD using the prd-creation-workflow"
[Cursor creates PRD]

You: "Now create a TDD using the tdd-creation-workflow"
[Cursor can reference the PRD from chat history]
```

---

## Workflows Overview

Same workflows as Claude Code version:

1. **[prd-creation-workflow.md](workflows/prd-creation-workflow.md)** - Define WHAT & WHY
2. **[tdd-creation-workflow.md](workflows/tdd-creation-workflow.md)** - Design HOW
3. **[task-breakdown-workflow.md](workflows/task-breakdown-workflow.md)** - Create TICKETS
4. **[linear-ticket-workflow.md](workflows/linear-ticket-workflow.md)** - Build FEATURE
5. **[product-development-workflow.md](workflows/product-development-workflow.md)** - Overview

### Reference Templates

1. **[prd-template.md](reference/prd-template.md)** - PRD template
2. **[tdd-template.md](reference/tdd-template.md)** - Technical design template
3. **[task-breakdown-template.md](reference/task-breakdown-template.md)** - Task breakdown template
4. **[adr-template.md](reference/adr-template.md)** - Architecture decision record template
5. **[quick-reference.md](reference/quick-reference.md)** - One-page cheat sheet (for quick lookups, onboarding, or printing - not a replacement for detailed workflows)

---

## Differences from Claude Code Version

| Feature | Claude Code (.claude/) | Cursor (.cursor/) |
|---------|------------------------|-------------------|
| Config file | `.claude/instructions.md` | `.cursorrules` (in project root) |
| File location | `.claude/` directory | `.cursor/` directory + root `.cursorrules` |
| File reference | Automatic with "using the workflow" | Use `@.cursor/workflows/filename.md` |
| Multi-file editing | Edit tool (sequential) | Composer (simultaneous) |
| Command invocation | Natural language in chat | Cmd+L (chat) or Cmd+I (composer) |

---

## Tips for Using with Cursor

### 1. Start Chat Sessions with Workflow Context

```
Cmd+L → "I'm implementing PROJ-42. Let's follow the linear-ticket-workflow"
```

### 2. Reference Workflows Mid-Implementation

```
Cmd+I → "Following @.cursor/workflows/linear-ticket-workflow.md Phase 3,
write the failing tests first"
```

### 3. Use Composer for Full Ticket Implementation

```
Cmd+I → "Implement ticket PROJ-42 using the linear-ticket-workflow.
Update all necessary files with TDD approach."
```

Select all relevant files in the sidebar, then Cursor will edit them together.

### 4. Combine with Cursor's Tab Autocomplete

As you code, Cursor's autocomplete will respect the workflow principles (TDD, naming conventions, etc.) defined in `.cursorrules`.

---

## Getting Started

### First Time Setup

1. **Copy .cursorrules to your project:**
   ```bash
   cp /path/to/ai-dev-workflow/.cursor/.cursorrules /path/to/your-project/.cursorrules
   ```

2. **Copy workflows for reference:**
   ```bash
   cp -r /path/to/ai-dev-workflow/.cursor /path/to/your-project/.cursor
   ```

3. **Open Cursor in your project**

4. **Start with Cursor Chat (Cmd+L):**
   ```
   "I want to build [feature] using the prd-creation-workflow"
   ```

### Your First Feature in Cursor

```bash
# Step 1: Define requirements (Cmd+L)
"Create a PRD for [simple feature] using the prd-creation-workflow"

# Step 2: Design solution (Cmd+L)
"Create a TDD for this feature using the tdd-creation-workflow"

# Step 3: Create tickets (Cmd+L)
"Break this down using the task-breakdown-workflow"

# Step 4: Implement (Cmd+I on multiple files)
"Implement ticket [TICKET-ID] using the linear-ticket-workflow"
```

---

## Benefits of Cursor Version

✅ **Same rigorous workflows** as Claude Code version
✅ **Faster multi-file editing** with Composer
✅ **Inline code generation** with Tab autocomplete
✅ **Visual diff preview** before accepting changes
✅ **Git integration** for commits and PRs
✅ **Same token efficiency** - workflows loaded on-demand

---

## Version

**Version:** 1.0
**Created:** 2025-11-06
**Adapted from:** Claude Code workflows
**Compatible with:** Cursor IDE v0.30+

---

## License

MIT (or whatever license you prefer)
