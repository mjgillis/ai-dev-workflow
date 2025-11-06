# Quick Reference Card

**One-page cheat sheet for Claude product development workflows**

---

## When to Use Which Workflow

| Situation | Workflow | Command |
|-----------|----------|---------|
| 💡 I have an idea | PRD Creation | `Create a PRD for [feature] using the prd-creation-workflow` |
| 📄 I have a PRD | TDD Creation | `Create a TDD based on this PRD using the tdd-creation-workflow` |
| 🏗️ I have PRD + TDD | Task Breakdown | `Break down this PRD and TDD into tickets using the task-breakdown-workflow` |
| 🎫 I have a Linear ticket | Implementation | `Implement Linear ticket [ID] following the linear-ticket-workflow` |

---

## Quick Decision Tree

```
Idea → PRD → TDD → Tickets → Implementation → Done
  ↓       ↓      ↓       ↓           ↓
  1       2      3       4           5
```

1. **PRD Creation** - Define WHAT & WHY
2. **TDD Creation** - Design HOW
3. **Task Breakdown** - Create actionable tickets
4. **Implementation** - Build each ticket with TDD
5. **Done** - Feature shipped!

---

## Core Principles (The P0 Rules)

### 1. Always Ask Questions
- Never assume when unclear
- Clarify ambiguity before proceeding

### 2. TDD is Mandatory
- Write tests FIRST (Red phase)
- Implement to pass (Green phase)
- Refactor for quality

### 3. Document Everything
- Code → Ticket → TDD → PRD chain
- Always reference TDD version (e.g., "TDD v2.1 Section 4.1")

### 4. Living Documents
- Update PRD/TDD as you learn
- Track changes in changelog
- Use semantic versioning

### 5. Linear Status Management
```
Todo → In Progress → Completed
```
- Set "In Progress" when starting (Phase 1)
- Set "Completed" after PR merge (Phase 7)

### 6. Git Workflow
- Branch: `feature/TICKET-ID-description`
- Commits: Conventional format (`feat:`, `fix:`, etc.)
- PR: Include ticket ID, link to Linear

### 7. Definition of Done
- [ ] Tests passing (>80% coverage)
- [ ] No linter warnings
- [ ] Documentation updated
- [ ] Code reviewed
- [ ] PR merged
- [ ] Ticket completed

### 8. Right-Size Work
- Max 13 story points per ticket
- Break larger work into smaller stories

---

## Common Commands

### PRD Creation
```
Create a PRD for [feature] using the prd-creation-workflow
```

### TDD Creation
```
Create a TDD based on this PRD using the tdd-creation-workflow
```

### Task Breakdown
```
Break down this PRD and TDD into tickets using the task-breakdown-workflow
```

### Implement Ticket
```
Implement Linear ticket [TICKET-ID] following the linear-ticket-workflow
```

### Check Progress
```
What's the status of [feature/ticket]? What's left to do?
```

### Validate Quality
```
Review [PRD/TDD/implementation] for completeness and quality
```

---

## Story Point Reference (Fibonacci)

| Points | Time | Complexity | Example |
|--------|------|------------|---------|
| 1 | 1-2 hours | Trivial | Add field, update docs |
| 2 | 2-4 hours | Simple | Basic CRUD endpoint |
| 3 | 4-8 hours | Moderate | Endpoint with validation |
| 5 | 1-2 days | Complex | Feature with DB changes |
| 8 | 2-3 days | Very Complex | Multi-service integration |
| 13 | 3-5 days | Highly Complex | Multi-component feature |

**If >13 points:** Break it down further!

---

## Conventional Commit Format

```
<type>(<scope>): <subject>

<body>

Implements: TICKET-ID
TDD Reference: Section X.Y

🤖 Generated with Claude Code
Co-Authored-By: Claude <noreply@anthropic.com>
```

**Types:**
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation only
- `test`: Adding tests
- `refactor`: Code restructuring
- `chore`: Maintenance

---

## TDD Complexity Guide

| Feature Size | Use These Phases | Time |
|--------------|------------------|------|
| Small (<5 pts) | 1, 2, 3, 4, 9 | 2-4 hours |
| Medium (5-20 pts) | All except 8 (deployment) | 4-8 hours |
| Large (>20 pts) | All 9 phases | 1-2 days |

---

## Test Coverage Targets

```
      /\
     /E2E\      ← 10% (expensive, slow)
    /------\
   /Integr.\   ← 20% (moderate cost)
  /----------\
 /   Unit     \ ← 70% (cheap, fast)
/--------------\
```

**Minimum:** >80% overall coverage

---

## Definition of Done Checklist

**Code Quality:**
- [ ] Code reviewed
- [ ] No linter warnings (`ruff check`, `mypy`)
- [ ] Tests passing (`pytest`)
- [ ] Coverage >80% (`pytest --cov`)

**Documentation:**
- [ ] Docstrings added
- [ ] README updated (if needed)
- [ ] Inline comments for complex logic

**Testing:**
- [ ] Unit tests written and passing
- [ ] Edge cases covered
- [ ] Error scenarios tested

**Git:**
- [ ] Feature branch created
- [ ] Conventional commits
- [ ] PR created with ticket ID
- [ ] PR merged to main

**Linear:**
- [ ] Ticket marked "In Progress" at start
- [ ] Ticket marked "Completed" after merge

---

## Failure Recovery Quick Guide

### PR Breaks Production
1. **Revert immediately:** `git revert <commit>`
2. **Deploy revert**
3. **Root cause analysis** (within 24h)
4. **Add tests** to prevent recurrence
5. **Re-implement** with new tests

### Sprint Goal Not Met
1. **Analyze** what went wrong
2. **Adjust velocity** for next sprint
3. **Re-estimate** remaining work
4. **Communicate** to stakeholders

### Blocked by Dependency
1. **Mark as blocked** in Linear
2. **Communicate** with dependency owner (same day)
3. **Escalate** if no response (24h)
4. **Find alternative work**

---

## Document Versions

**Format:** MAJOR.MINOR.PATCH

- **MAJOR:** Breaking change (scope/architecture change)
- **MINOR:** Additive change (new requirement)
- **PATCH:** Fix/typo (no functional impact)

**Always reference version in tickets:**
- ✅ "See TDD v2.1 Section 4.1"
- ❌ "See TDD Section 4.1"

---

## Quality Gates

### PRD → TDD
- [ ] Problem clearly stated
- [ ] Success metrics defined
- [ ] All user stories have acceptance criteria
- [ ] Scope boundaries clear
- [ ] Stakeholder approval

### TDD → Task Breakdown
- [ ] Architecture documented
- [ ] Data models defined
- [ ] API specs complete
- [ ] Testing strategy defined
- [ ] All PRD requirements addressed

### Task Breakdown → Implementation
- [ ] All stories estimated
- [ ] Dependencies identified
- [ ] Sprint plan created
- [ ] Tickets created in Linear

### Implementation → Done
- [ ] All acceptance criteria met
- [ ] Tests passing (>80% coverage)
- [ ] No linter warnings
- [ ] Documentation updated
- [ ] PR merged
- [ ] Ticket marked "Completed"

---

## Tools Integration

### Linear MCP
```python
# Fetch ticket
ticket = linear.get_issue("PROJ-42")

# Update status
linear.update_issue("PROJ-42", status="In Progress")

# Add comment
linear.create_comment("PROJ-42", "Implementation started")
```

### GitHub CLI
```bash
# Create PR
gh pr create \
  --title "feat(scope): description (TICKET-ID)" \
  --body "Closes TICKET-ID" \
  --base main
```

---

## File Locations

| Type | Location |
|------|----------|
| Workflows | `/workflows/*.md` |
| Templates | `/reference/*-template.md` |
| Quick Ref | `/reference/quick-reference.md` |
| Parent Workflow | `/workflows/product-development-workflow.md` |

---

## When to Skip Workflows

### Skip PRD if:
- Obvious bug fix
- <2 hour change
- Single developer prototype
- Copy existing pattern

### Skip TDD if:
- Trivial PRD (<5 points)
- Reusing existing architecture
- No new components/APIs

### Always Use:
- linear-ticket-workflow (ensures quality)
- TDD approach (tests first)

---

## Getting Help

### Workflow Questions
```
I want to build [feature]. Which workflow should I use?
```

### Check Completeness
```
Is this [PRD/TDD/ticket breakdown] complete? What's missing?
```

### Validate Against Requirements
```
Does this implementation meet all acceptance criteria?
```

---

**Version:** 1.0
**Last Updated:** 2025-11-06
**For:** Claude Product Development Workflows
