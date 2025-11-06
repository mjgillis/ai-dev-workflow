# Product Development Workflows

This project contains structured workflows for product development with Claude Code.

---

## Core Principles (P0 - Always Follow)

### 1. Always Ask Clarifying Questions
When requirements are ambiguous, STOP and ask the user clarifying questions.

### 2. Test-Driven Development (TDD) is Mandatory
Always write tests BEFORE implementation (Red-Green-Refactor cycle).

### 3. Document Everything with Traceability
Maintain chain: Code → Ticket → TDD → PRD
Always include version: "TDD v2.1 Section 4.1" (not just "Section 4.1")

### 4. Update Documents as You Learn
PRD, TDD, and task breakdowns are LIVING DOCUMENTS. Update and version them.

### 5. Manage Linear Ticket Status
```
Todo → In Progress (when start) → Completed (after PR merge)
```

### 6. Follow Git Workflow Standards
- Branch: `feature/TICKET-ID-description`
- Commits: Conventional format (`feat:`, `fix:`, etc.)
- PR: Include ticket ID, link to Linear

### 7. Definition of Done (Universal)
- [ ] Tests passing (>80% coverage)
- [ ] No linter warnings
- [ ] Documentation updated
- [ ] Code reviewed
- [ ] PR merged
- [ ] Ticket completed

### 8. Right-Size All Work
Max 13 story points per ticket. Break down larger work.

---

## How to Invoke Workflows

When the user mentions a workflow, read the corresponding file and follow it step-by-step.

### Workflow Commands

| User Says | Read This File | Purpose |
|-----------|---------------|---------|
| "Create PRD using prd-creation-workflow" | `workflows/prd-creation-workflow.md` | Define WHAT & WHY |
| "Create TDD using tdd-creation-workflow" | `workflows/tdd-creation-workflow.md` | Design HOW |
| "Break down using task-breakdown-workflow" | `workflows/task-breakdown-workflow.md` | Create TICKETS |
| "Implement ticket [ID] using linear-ticket-workflow" | `workflows/linear-ticket-workflow.md` | Build FEATURE |

### Quick Reference

For cheat sheet, read: `reference/quick-reference.md`

---

## Decision Tree

```
Idea → PRD → TDD → Tickets → Implementation
  ↓       ↓      ↓       ↓           ↓
  1       2      3       4           5
```

---

## Tools

- **Linear MCP** - Update ticket status, create tickets
- **GitHub CLI** - Create PRs with `gh pr create`

---

## Document Versioning

PRD and TDD use semantic versioning: MAJOR.MINOR.PATCH

Always reference version in tickets:
- ✅ "See TDD v2.1 Section 4.1"
- ❌ "See TDD Section 4.1"

---

## File Locations

- Workflows: `/workflows/*.md`
- Templates: `/reference/*-template.md`
- Quick Ref: `/reference/quick-reference.md`
- ADR Template: `/reference/adr-template.md`

---

**Version:** 1.0
**Last Updated:** 2025-11-06
