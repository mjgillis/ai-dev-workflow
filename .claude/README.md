# Claude Product Development Workflows

A complete set of workflows for product development with Claude Code, from ideation to implementation.

---

## What's Included

### Workflows

Located in [`/workflows`](workflows/):

1. **[product-development-workflow.md](workflows/product-development-workflow.md)** - Overview and entry point
2. **[prd-creation-workflow.md](workflows/prd-creation-workflow.md)** - Create Product Requirements Documents
3. **[tdd-creation-workflow.md](workflows/tdd-creation-workflow.md)** - Create Technical Design Documents
4. **[task-breakdown-workflow.md](workflows/task-breakdown-workflow.md)** - Break down into Linear tickets
5. **[linear-ticket-workflow.md](workflows/linear-ticket-workflow.md)** - Implement individual tickets

### Reference Templates

Located in [`/reference`](reference/):

1. **[prd-template.md](reference/prd-template.md)** - Simple but comprehensive PRD template
2. **[tdd-template.md](reference/tdd-template.md)** - Technical design document template
3. **[task-breakdown-template.md](reference/task-breakdown-template.md)** - Task breakdown and sprint planning template
4. **[adr-template.md](reference/adr-template.md)** - Architecture decision record template
5. **[quick-reference.md](reference/quick-reference.md)** - One-page cheat sheet for quick lookups

---

## Quick Start

### Installation

```bash
# Copy the .claude folder to your project
cp -r /path/to/ai-dev-workflow/.claude /path/to/your-project/

# That's it! Claude Code will automatically load the instructions
```

### Workflow Commands

Simply tell Claude which workflow to use:

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

### Complete Example

```
You: "I want to build an API usage dashboard using the prd-creation-workflow"

Claude: [Guides you through PRD creation with questions]

You: "Now create a TDD using the tdd-creation-workflow"

Claude: [Helps design technical architecture]

You: "Break this down using the task-breakdown-workflow"

Claude: [Creates sprint plan with Linear tickets]

You: "Implement ticket PROJ-1 using the linear-ticket-workflow"

Claude: [Implements with TDD approach]
```

---

## Using in Your Projects

### Simple Setup

1. **Copy the `.claude` folder to your project:**
   ```bash
   cp -r /path/to/ai-dev-workflow/.claude /path/to/your-project/
   ```

2. **Start using workflows:**
   ```bash
   # Just say "using the [workflow-name]" in your prompts
   "Create a PRD for user authentication using the prd-creation-workflow"
   ```

3. **Customize (optional):**
   ```bash
   # Edit .claude/instructions.md to add project-specific rules
   ```

### That's It!

Claude Code automatically:
- Loads `.claude/instructions.md` (core principles + workflow commands)
- Reads workflow files on-demand when you mention them
- Keeps context clean (~2.5K tokens permanent vs ~50K if all workflows loaded)

---

## Command Reference

Quick reference for workflow commands:

| When You Want To... | Say This to Claude |
|---------------------|-------------------|
| Define requirements | `"Create a PRD for [feature] using the prd-creation-workflow"` |
| Design implementation | `"Create a TDD for [feature] using the tdd-creation-workflow"` |
| Break into tickets | `"Break down this PRD and TDD using the task-breakdown-workflow"` |
| Implement a ticket | `"Implement ticket [TICKET-ID] using the linear-ticket-workflow"` |
| See quick reference | `"Show me the quick reference"` (reads `reference/quick-reference.md`) |

**Pattern:** Just say **"using the [workflow-name]"** and Claude will load and follow it.

---

## Workflows Overview

### 1. Product Development Workflow (Master)

**Purpose:** Overview of entire process from idea to implementation

**When to use:** Starting any new product development effort

**Output:** Understanding of which workflow to use when

**Read:** [product-development-workflow.md](workflows/product-development-workflow.md)

---

### 2. PRD Creation Workflow

**Purpose:** Define what to build and why

**When to use:**
- Starting a new feature
- Need stakeholder approval
- Requirements are unclear

**Output:**
- Problem statement
- User stories with acceptance criteria
- Success metrics
- Scope and timeline

**Read:** [prd-creation-workflow.md](workflows/prd-creation-workflow.md)

**Template:** [prd-template-1pager.md](reference/prd-template-1pager.md)

---

### 3. TDD Creation Workflow

**Purpose:** Design technical implementation

**When to use:**
- Have approved PRD
- Need to communicate technical approach
- Before implementation

**Output:**
- Architecture design
- Database schemas
- API specifications
- Testing strategy
- Deployment plan

**Read:** [tdd-creation-workflow.md](workflows/tdd-creation-workflow.md)

**Template:** [tdd-template.md](reference/tdd-template.md)

---

### 4. Task Breakdown Workflow

**Purpose:** Break PRD+TDD into actionable tickets

**When to use:**
- Have PRD and TDD
- Ready to start development
- Need sprint planning

**Output:**
- Epic structure
- Right-sized stories (<13 points)
- Sprint plan
- Linear tickets with full context

**Read:** [task-breakdown-workflow.md](workflows/task-breakdown-workflow.md)

**Template:** [task-breakdown-template.md](reference/task-breakdown-template.md)

---

### 5. Linear Ticket Implementation Workflow

**Purpose:** Implement individual tickets with TDD

**When to use:**
- For every Linear ticket
- Want consistent quality
- Following TDD best practices

**Output:**
- Feature implemented
- Tests passing (>80% coverage)
- PR created and reviewed
- Ticket marked complete

**Read:** [linear-ticket-workflow.md](workflows/linear-ticket-workflow.md)

---

## Decision Tree

### Visual Workflow Selection

```
                        ┌─────────────────────┐
                        │   I have an idea!   │
                        │  or feature request │
                        └──────────┬──────────┘
                                   │
                                   ▼
                        ┌──────────────────────┐
                        │ Do I have a PRD with │
                        │ requirements & user  │
                        │      stories?        │
                        └──────────┬───────────┘
                                   │
                    ┌──────────────┴──────────────┐
                    │ NO                         │ YES
                    ▼                            ▼
        ┌─────────────────────┐      ┌─────────────────────┐
        │  PRD Creation        │      │ Do I have a TDD     │
        │     Workflow         │      │ with technical      │
        │                      │      │     design?         │
        │ Define WHAT & WHY    │      └──────────┬──────────┘
        └─────────────────────┘                  │
                                  ┌──────────────┴──────────────┐
                                  │ NO                         │ YES
                                  ▼                            ▼
                      ┌─────────────────────┐      ┌─────────────────────┐
                      │  TDD Creation        │      │ Do I have tickets   │
                      │     Workflow         │      │   in Linear with    │
                      │                      │      │   breakdowns?       │
                      │   Design HOW         │      └──────────┬──────────┘
                      └─────────────────────┘                  │
                                              ┌─────────────────┴──────────────┐
                                              │ NO                            │ YES
                                              ▼                               ▼
                                  ┌─────────────────────┐         ┌─────────────────────┐
                                  │  Task Breakdown      │         │   Linear Ticket     │
                                  │     Workflow         │         │ Implementation      │
                                  │                      │         │     Workflow        │
                                  │  Create TICKETS      │         │                     │
                                  └─────────────────────┘         │   Build FEATURE     │
                                                                  └─────────────────────┘

```

### Quick Decision Guide

| I have... | I need... | Use this workflow |
|-----------|-----------|-------------------|
| Just an idea | Requirements & goals | [prd-creation-workflow](workflows/prd-creation-workflow.md) |
| PRD | Technical design | [tdd-creation-workflow](workflows/tdd-creation-workflow.md) |
| PRD + TDD | Actionable tickets | [task-breakdown-workflow](workflows/task-breakdown-workflow.md) |
| A Linear ticket | To implement it | [linear-ticket-workflow](workflows/linear-ticket-workflow.md) |

### Simple Text Version

```
Do you have requirements?
├─ NO  → Use: prd-creation-workflow
└─ YES → Do you have technical design?
         ├─ NO  → Use: tdd-creation-workflow
         └─ YES → Do you have tickets?
                  ├─ NO  → Use: task-breakdown-workflow
                  └─ YES → Use: linear-ticket-workflow
```

---

## Benefits

### For Solo Developers

- ✅ Prevents scope creep
- ✅ Ensures nothing is forgotten
- ✅ Creates documentation for future you
- ✅ Improves estimation over time

### For Teams

- ✅ Shared understanding of requirements
- ✅ Clear technical direction
- ✅ Faster onboarding
- ✅ Reduced rework
- ✅ Better sprint planning

### For Stakeholders

- ✅ Visibility into progress
- ✅ Clear requirements documentation
- ✅ Predictable delivery
- ✅ Traceable decisions

---

## Customization

These workflows are designed to be customized:

1. **Tech Stack:** Update TDD template for your languages/frameworks
2. **Tools:** Adapt for Jira, GitHub Issues, etc. (not just Linear)
3. **Process:** Adjust for your team's workflow
4. **Templates:** Add/remove sections based on needs

---

## Philosophy

These workflows follow key principles:

1. **Progressive Elaboration:** Start high-level, add detail as you learn
2. **Living Documents:** Update PRD/TDD as you discover new information
3. **Context Preservation:** Every decision is documented and traceable
4. **TDD First:** Write tests before implementation
5. **Small Batches:** Right-size work to <13 story points
6. **Continuous Validation:** Check against requirements at every step

---

## Example Timeline

**Feature:** API Usage Dashboard (52 points, team of 3)

| Week | Activity | Workflow | Time |
|------|----------|----------|------|
| 1 | PRD Creation | prd-creation-workflow | 4 hours |
| 2 | Technical Design | tdd-creation-workflow | 8 hours |
| 3 | Task Breakdown | task-breakdown-workflow | 4 hours |
| 4-9 | Implementation (3 sprints) | linear-ticket-workflow | 6 weeks |

**Total:** 9 weeks from idea to production

---

## FAQs

### "Isn't this waterfall?"

No! These are living documents:
- Update as you learn
- Iterate on design
- Refine estimates
- Start implementation as soon as first tickets are ready

### "This seems like a lot of documentation"

Documentation effort scales with complexity:
- **Small feature (<5 points):** Lightweight (1-2 hours total)
- **Medium feature (5-20 points):** Standard (4-8 hours)
- **Large feature (>20 points):** Comprehensive (1-2 days)

Rule of thumb: ~10% of development time

### "My team is agile, we don't plan this much"

This supports agile:
- Sprint planning → Task breakdown workflow
- User stories → PRD workflow
- Technical spikes → TDD workflow
- Definition of Done → In every workflow

### "What if I just want to code?"

For throwaway prototypes: Skip workflows, just code.

For production features: 2 hours of planning saves days of rework.

---

## Success Stories

Track these metrics to measure impact:

- **Rework reduction:** How often do you rewrite code?
- **Estimation accuracy:** Estimated vs actual story points
- **Defect rate:** Bugs per feature
- **Team satisfaction:** Developer happiness
- **Onboarding time:** Time for new dev to contribute

**Target improvements:**
- 50% less rework
- 20% better estimates
- 30% faster onboarding

---

## Contributing

Improvements welcome! These workflows should evolve based on real-world use.

To suggest changes:
1. Try the workflow on a real project
2. Note what works and what doesn't
3. Propose specific improvements
4. Share learnings with the team

---

## Resources

### Workflow Files

- [product-development-workflow.md](workflows/product-development-workflow.md)
- [prd-creation-workflow.md](workflows/prd-creation-workflow.md)
- [tdd-creation-workflow.md](workflows/tdd-creation-workflow.md)
- [task-breakdown-workflow.md](workflows/task-breakdown-workflow.md)
- [linear-ticket-workflow.md](workflows/linear-ticket-workflow.md)

### Template Files

- [prd-template-1pager.md](reference/prd-template-1pager.md)
- [tdd-template.md](reference/tdd-template.md)
- [task-breakdown-template.md](reference/task-breakdown-template.md)

---

## Getting Started

### First Time Setup

1. **Copy .claude folder to your project:**
   ```bash
   cp -r /path/to/ai-dev-workflow/.claude /path/to/your-project/
   ```

2. **Open your project in Claude Code**

3. **Start with a simple prompt:**
   ```
   "I want to build [your feature] using the prd-creation-workflow"
   ```

### Your First Feature

Try this complete flow on a small feature:

```bash
# Step 1: Define requirements
"Create a PRD for [simple feature] using the prd-creation-workflow"

# Step 2: Design solution
"Create a TDD for this feature using the tdd-creation-workflow"

# Step 3: Create tickets
"Break this down using the task-breakdown-workflow"

# Step 4: Implement
"Implement ticket [TICKET-ID] using the linear-ticket-workflow"
```

### Next Steps

- Read [product-development-workflow.md](workflows/product-development-workflow.md) for full details
- Customize `.claude/instructions.md` with your project-specific rules
- See [quick-reference.md](reference/quick-reference.md) for one-page cheat sheet
  - Use for quick lookups, onboarding, or print as reference card
  - Not a replacement for detailed workflows

---

**Version:** 1.0
**Created:** 2025-11-05
**License:** MIT (or whatever license you prefer)

