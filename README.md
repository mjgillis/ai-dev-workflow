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

1. **[prd-template-1pager.md](reference/prd-template-1pager.md)** - Simple but comprehensive PRD template
2. **[tdd-template.md](reference/tdd-template.md)** - Technical design document template
3. **[task-breakdown-template.md](reference/task-breakdown-template.md)** - Task breakdown and sprint planning template

---

## Quick Start

### The Complete Flow

```
1. PRD Creation
   "Create a PRD for [feature] using the prd-creation-workflow"

2. TDD Creation
   "Create a TDD based on this PRD using the tdd-creation-workflow"

3. Task Breakdown
   "Break down this PRD and TDD into tickets using the task-breakdown-workflow"

4. Implementation (per ticket)
   "Implement Linear ticket [ID] following the linear-ticket-workflow"
```

### Example

```
You: "I want to build an API usage dashboard. Let's create a PRD using the prd-creation-workflow."

Claude: [Guides you through PRD creation with questions]

You: "Great! Now create a TDD using the tdd-creation-workflow."

Claude: [Helps design technical architecture]

You: "Break this down into Linear tickets using the task-breakdown-workflow."

Claude: [Creates sprint plan with tickets]

You: "Implement ticket PROJ-1 following the linear-ticket-workflow."

Claude: [Implements with TDD approach]
```

---

## Using in Your Projects

### Option 1: Copy to `.claude` Directory

```bash
# Copy workflows and templates to your project
cp -r workflows /path/to/your/project/.claude/
cp -r reference /path/to/your/project/.claude/
```

### Option 2: Create Slash Commands

Create `.claude/commands/` with shortcuts:

**`.claude/commands/prd.md`:**
```
Create a PRD using .claude/workflows/prd-creation-workflow.md
```

**`.claude/commands/tdd.md`:**
```
Create a TDD using .claude/workflows/tdd-creation-workflow.md
```

Then simply use: `/prd`, `/tdd`, etc.

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

1. **Read:** Start with [product-development-workflow.md](workflows/product-development-workflow.md)
2. **Try:** Pick a small feature and walk through all workflows
3. **Refine:** Customize templates for your needs
4. **Scale:** Use on larger projects

**First prompt to Claude:**

```
I want to build [your feature]. Let's follow the product-development-workflow
from .claude/workflows/product-development-workflow.md
```

---

**Version:** 1.0
**Created:** 2025-11-05
**License:** MIT (or whatever license you prefer)

