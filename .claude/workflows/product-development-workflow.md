# Product Development Workflow

**Purpose:** Master workflow and instruction set for product development with Claude, from idea to implementation.

---

## Rules

- Never access the .env file directly
- Never copy or use any API keys or secrets
- Always ask questions sequentially so I can answer one at a time
- Always solve the issue in the simplest way possible

---

## Tools

- **Linear MCP** - Make sure you can connect to Linear via the MCP
- **GitHub** - Make sure you can connect to GitHub

---

## Prompts

**Starting new feature:**
```
I want to build [feature]. Let's follow the product-development-workflow.
```

**Have PRD only:**
```
I have a PRD for [feature]. Let's create a TDD using the tdd-creation-workflow.
```

**Have PRD + TDD:**
```
I have a PRD and TDD for [feature]. Let's break it down into tickets using the task-breakdown-workflow.
```

**Implement ticket:**
```
Implement Linear ticket [TICKET-ID] following the linear-ticket-workflow.
```

---

## Overview

This is the parent workflow that governs all product development activities. All other workflows (PRD, TDD, Task Breakdown, Linear Ticket) are child workflows that follow these core principles.

### The Complete Process

```
Product Idea
    ↓
PRD Creation (Define WHAT & WHY)
    ↓
TDD Creation (Design HOW)
    ↓
Task Breakdown (Create TICKETS)
    ↓
Implementation (Build each ticket with TDD)
    ↓
Delivery
```

---

## Core Principles (P0 - Non-Negotiable)

### 1. Always Ask Clarifying Questions

**Rule:** When requirements are ambiguous, incomplete, or have multiple valid interpretations, STOP and ask the user clarifying questions.

**Never assume:**
- Technical implementation details
- User preferences
- Business priorities
- Scope boundaries

**Example:**
```
❌ BAD: "I'll assume we want OAuth 2.0 for authentication"
✅ GOOD: "I see authentication is required. Which method do you prefer: OAuth 2.0, JWT, or session-based auth?"
```

### 2. Test-Driven Development (TDD) is Mandatory

**Rule:** Always write tests BEFORE implementation.

**Red-Green-Refactor cycle:**
1. Write failing test (Red)
2. Implement minimal code to pass (Green)
3. Refactor for quality (Refactor)
4. Repeat

**No exceptions.** Tests must exist before code is merged.

### 3. Document Everything with Traceability

**Rule:** Create a paper trail from idea to implementation.

**Traceability chain:**
- Code references → Linear ticket ID
- Linear ticket references → TDD section(s)
- TDD references → PRD requirement(s)
- PRD references → User research/feedback

**Example in code:**
```python
def request_asset(self, format: str) -> dict:
    """
    Request asset generation.

    Implements: PROJ-5
    TDD Reference: Section 6.1
    PRD Reference: User Story 2
    """
```

### 4. Update Documents as You Learn

**Rule:** PRD, TDD, and task breakdowns are LIVING DOCUMENTS.

**When to update:**
- Discover new edge cases → Update TDD
- Requirements change → Update PRD
- Technical approach changes → Update TDD
- Scope changes → Update PRD and task breakdown

**Always track changes in the changelog section.**

### 5. Manage Linear Ticket Status

**Rule:** Keep Linear tickets in sync with actual work status.

**Status flow:**
```
Todo → In Progress → Completed
```

**When to update:**
- **In Progress:** Immediately when starting work (Phase 1 of linear-ticket-workflow)
- **Completed:** After PR is merged (Phase 7 of linear-ticket-workflow)

**Use Linear MCP** to update status automatically.

### 6. Follow Git Workflow Standards

**Rule:** Consistent git practices across all work.

**Branch naming:**
- `feature/TICKET-ID-description` - New features
- `fix/TICKET-ID-description` - Bug fixes
- `refactor/TICKET-ID-description` - Code refactoring
- `docs/TICKET-ID-description` - Documentation only

**Commit messages:** Use Conventional Commits
```
<type>(<scope>): <subject>

<body>

Implements: TICKET-ID
TDD Reference: Section X.Y

🤖 Generated with Claude Code
Co-Authored-By: Claude <noreply@anthropic.com>
```

**Types:** feat, fix, docs, test, refactor, chore

### 7. Definition of Done is Universal

**Rule:** Every ticket must meet these criteria before completion.

**Checklist:**
- [ ] Tests written and passing (coverage >80%)
- [ ] No linter warnings
- [ ] Documentation updated (docstrings, README if needed)
- [ ] Code reviewed
- [ ] PR created and merged
- [ ] Linear ticket marked "Completed"

### 8. Right-Size All Work

**Rule:** No story should exceed 13 story points.

**If a story is >13 points:**
- Break it down into smaller stories
- Each story should deliver value independently
- Ensure dependencies are clear

**Estimation scale (Fibonacci):**
- 1-2 points: Hours
- 3-5 points: 1-2 days
- 8 points: 2-3 days
- 13 points: 3-5 days (maximum)

---

## Document Versioning & Change Management

### Why Version Documents?

PRD and TDD are **living documents** that evolve as you learn. However, work may be in progress based on earlier versions. Without versioning, you risk:

- Tickets built against old requirements
- Team confusion about "current" design
- Lost context about why decisions changed

### Semantic Versioning for Documents

**Format:** MAJOR.MINOR.PATCH

**Version Types:**

- **MAJOR (e.g., 1.0 → 2.0):** Breaking change
  - Scope change (feature removed/replaced)
  - Architecture change (database switch, API redesign)
  - Affects existing tickets significantly

- **MINOR (e.g., 1.0 → 1.1):** Additive change
  - New requirement added
  - Clarification that doesn't change existing work
  - Additional acceptance criteria

- **PATCH (e.g., 1.0.0 → 1.0.1):** Fix/typo
  - No functional impact
  - Formatting, spelling, grammar
  - Link updates

**Examples:**

```
PRD v1.0 → v1.1: Added new user story (minor)
PRD v1.1 → v2.0: Removed real-time requirement (major)

TDD v1.0 → v1.1: Added error handling details (minor)
TDD v1.1 → v2.0: Changed database from PostgreSQL to TimescaleDB (major)
```

### Change Management Process

**When PRD or TDD changes:**

1. **Update version number** in document header
2. **Add to changelog** with date, change description, and rationale
3. **Review impact on existing tickets**
   - MAJOR change: May require rework of in-progress tickets
   - MINOR change: Usually only affects future tickets
4. **Update affected tickets** with new references
5. **Communicate to team** (if applicable)

**Example Changelog Entry:**

```markdown
### Changelog

| Date | Version | Change | Rationale | Author |
|------|---------|--------|-----------|--------|
| 2025-01-15 | 1.0 | Initial draft | - | Mark |
| 2025-01-22 | 1.1 | Added Story 4: Export to CSV | User feedback from beta | Mark |
| 2025-02-03 | 2.0 | Changed from 30s to 5min refresh | Performance issues at scale | Mark |
```

### Ticket Referencing Best Practice

**Always include version in TDD references:**

❌ **Bad:** "See TDD Section 4.1"
✅ **Good:** "See TDD v2.1 Section 4.1"

This ensures engineers know which version of the design to follow.

### When Major Changes Happen Mid-Sprint

**Scenario:** TDD v1.0 → v2.0 during Sprint 2

**Process:**

1. **Assess impact:**
   - Which tickets are affected?
   - Are they already in progress?
   - Can they be updated or must they be scrapped?

2. **Update tickets:**
   - In Progress tickets: Add comment with v2.0 changes needed
   - Todo tickets: Update description to reference v2.0
   - Completed tickets: Usually no change needed

3. **Replan if needed:**
   - If major rework required, adjust sprint commitment
   - Create new tickets for rework
   - Communicate timeline impact

4. **Document decision:**
   - Why did we change?
   - What did we learn?
   - How can we avoid this next time?

**Example:**

```
PROJ-5 was started based on TDD v1.0 (PostgreSQL).
TDD updated to v2.0 (TimescaleDB).

Action:
- PROJ-5 paused mid-implementation
- Created PROJ-12: Migrate to TimescaleDB approach
- PROJ-5 will be completed after PROJ-12
- Sprint 2 capacity reduced by 5 points
```

---

## The Four Workflows

### 1. PRD Creation Workflow

**Purpose:** Define WHAT to build and WHY

**When to invoke:**
- Starting a new feature or product
- Requirements are unclear or not documented
- Need stakeholder alignment

**Command to invoke:**
```
Create a PRD for [feature] using the prd-creation-workflow
```

**Claude should:**
1. Ask clarifying questions about the problem
2. Identify user personas and pain points
3. Define measurable success metrics
4. Write user stories with acceptance criteria
5. Specify functional and non-functional requirements
6. Define scope boundaries (in/out of scope)
7. Identify dependencies and risks
8. Create timeline

**Output:** Approved PRD document

**Reference:** [prd-creation-workflow.md](prd-creation-workflow.md)

**Template:** [prd-template-1pager.md](../reference/prd-template-1pager.md)

---

### 2. TDD Creation Workflow

**Purpose:** Design HOW to build it technically

**When to invoke:**
- Have an approved PRD
- Ready to start technical design
- Need to communicate technical approach

**Command to invoke:**
```
Create a TDD based on this PRD using the tdd-creation-workflow
```

**Claude should:**
1. Review PRD requirements
2. Design system architecture
3. Define data models and schemas
4. Specify API endpoints
5. Document core algorithms
6. Define error handling strategy
7. Plan testing approach
8. Design deployment strategy

**Output:** Approved TDD document

**Reference:** [tdd-creation-workflow.md](tdd-creation-workflow.md)

**Template:** [tdd-template.md](../reference/tdd-template.md)

---

### 3. Task Breakdown Workflow

**Purpose:** Break PRD + TDD into actionable tickets

**When to invoke:**
- Have completed PRD and TDD
- Ready to start implementation
- Need sprint planning

**Command to invoke:**
```
Break down this PRD and TDD into Linear tickets using the task-breakdown-workflow
```

**Claude should:**
1. Extract user stories from PRD
2. Map technical requirements from TDD
3. Create epic structure
4. Break stories into right-sized tasks (<13 points)
5. Estimate story points
6. Identify dependencies
7. Create sprint plan
8. Generate Linear tickets with full context

**Output:**
- Linear tickets created (via Linear MCP or CLI)
- Sprint plan
- Dependency map

**Reference:** [task-breakdown-workflow.md](task-breakdown-workflow.md)

**Template:** [task-breakdown-template.md](../reference/task-breakdown-template.md)

---

### 4. Linear Ticket Implementation Workflow

**Purpose:** Implement individual tickets with TDD

**When to invoke:**
- For EVERY Linear ticket implementation
- User says "Implement ticket [ID]"

**Command to invoke:**
```
Implement Linear ticket [TICKET-ID] following the linear-ticket-workflow
```

**Claude should:**
1. Fetch ticket details (Linear MCP)
2. Mark ticket "In Progress" (Linear MCP)
3. Create implementation plan
4. Create feature branch
5. Write FAILING tests first (TDD Red phase)
6. Implement code to pass tests (TDD Green phase)
7. Refactor if needed
8. Validate acceptance criteria
9. Run Definition of Done checks
10. Commit with conventional commit message
11. Create PR
12. After PR merge: Mark ticket "Completed" (Linear MCP)

**Output:**
- Feature implemented and merged
- Tests passing (>80% coverage)
- Ticket completed

**Reference:** [linear-ticket-workflow.md](linear-ticket-workflow.md)

---

## Decision Tree: Which Workflow to Use?

```
START: User describes a task or goal
    ↓
Does it involve defining a NEW feature/product?
├─ YES → Is there a PRD?
│        ├─ NO  → Use: prd-creation-workflow
│        └─ YES → Continue below
│
└─ NO → Continue below

Is there a technical design (TDD)?
├─ NO  → Use: tdd-creation-workflow
└─ YES → Continue below

Are there tickets in Linear?
├─ NO  → Use: task-breakdown-workflow
└─ YES → Continue below

Is user asking to implement a specific ticket?
├─ YES → Use: linear-ticket-workflow
└─ NO  → Ask: "What would you like to do?"
           Options:
           - Create new PRD
           - Update existing TDD
           - Break down into tickets
           - Implement a ticket
```

---

## Key Commands & Prompts

### Starting a New Feature

```
I want to build [feature]. Let's follow the product-development-workflow.
```

**Claude responds with:**
```
I'll help you build [feature] following the product development workflow.

Let's start with the PRD to define what we're building and why.

**Step 1: PRD Creation**
I'll ask you questions about:
- The problem you're solving
- Who experiences this problem
- Success metrics
- Requirements and scope

Ready to begin?
```

### When User Has Partial Documentation

**User has PRD only:**
```
I have a PRD for [feature]. Let's create a TDD using the tdd-creation-workflow.
```

**User has PRD + TDD:**
```
I have a PRD and TDD for [feature]. Let's break it down into tickets using the task-breakdown-workflow.
```

**User has tickets:**
```
Implement Linear ticket [TICKET-ID] following the linear-ticket-workflow.
```

### Checking Progress

```
What's the status of [feature/ticket]? What's left to do?
```

### Validating Quality

```
Review the [PRD/TDD/implementation] for completeness and quality.
```

---

## Best Practices

### Communication with User

**Always:**
- Explain what you're about to do before doing it
- Show your reasoning for technical decisions
- Provide examples when describing approaches
- Offer alternatives when multiple valid options exist
- Confirm before proceeding with major changes

**Never:**
- Assume user intent without clarification
- Make technology choices without explaining tradeoffs
- Skip validation steps
- Proceed if acceptance criteria are unclear

### Workflow Transitions

**Between workflows:**
```
✅ PRD is complete and approved.

Ready to move to the next step: Technical Design (TDD).

Use this command:
"Create a TDD based on this PRD using the tdd-creation-workflow"
```

### Error Handling

**If documents are missing:**
```
I need the TDD to implement this ticket properly.

Options:
1. Create a TDD using the tdd-creation-workflow
2. Provide a link to the TDD
3. Paste the relevant TDD section here

Which would you prefer?
```

**If requirements are unclear:**
```
I found some ambiguity in the requirements:

Question 1: Should authentication use OAuth 2.0 or JWT?
Question 2: What's the expected response time requirement?

Please clarify so I can proceed with the correct implementation.
```

### Quality Gates

**Before moving to next workflow:**

**PRD → TDD:**
- [ ] Problem clearly stated
- [ ] Success metrics defined
- [ ] All user stories have acceptance criteria
- [ ] Scope boundaries clear
- [ ] Stakeholder approval obtained

**TDD → Task Breakdown:**
- [ ] Architecture documented
- [ ] Data models defined
- [ ] API specs complete
- [ ] Testing strategy defined
- [ ] All PRD requirements addressed

**Task Breakdown → Implementation:**
- [ ] All stories estimated
- [ ] Dependencies identified
- [ ] Sprint plan created
- [ ] Tickets created in Linear

**Implementation → Done:**
- [ ] All acceptance criteria met
- [ ] Tests passing (>80% coverage)
- [ ] No linter warnings
- [ ] Documentation updated
- [ ] PR merged
- [ ] Ticket marked "Completed"

---

## Common Scenarios

### Scenario 1: Brand New Feature

**User:** "I want to build an API usage dashboard"

**Claude:**
```
I'll guide you through building an API usage dashboard following the product development workflow.

Step 1: PRD Creation

Let's define what we're building and why. I'll ask you some questions:

1. **Problem:** What problem does this solve? Who experiences it?
2. **Goals:** What does success look like? How will we measure it?
3. **Users:** Who will use this? What are their needs?

Let's start with the problem. Can you describe:
- What pain point are users experiencing?
- How are they handling this today?
- What's the business impact?
```

### Scenario 2: Have PRD, Need Implementation

**User:** "I have a PRD for user authentication. Help me implement it."

**Claude:**
```
I see you have a PRD for user authentication. Before we implement, we need to create a Technical Design Document (TDD).

Current state: PRD ✅ | TDD ❌ | Tickets ❌ | Implementation ❌

Next step: Create TDD

The TDD will define:
- Authentication architecture (OAuth, JWT, session-based?)
- Database schema (users table, tokens, etc.)
- API endpoints (login, logout, refresh)
- Security measures (password hashing, token expiry)
- Testing strategy

Ready to create the TDD? Use:
"Create a TDD based on this PRD using the tdd-creation-workflow"
```

### Scenario 3: Have Ticket, Ready to Code

**User:** "Implement ticket PROJ-42"

**Claude:**
```
I'll implement ticket PROJ-42 following the linear-ticket-workflow.

Phase 1: Ticket Analysis
Let me fetch the ticket details from Linear...

[Fetches ticket via Linear MCP]

Ticket: PROJ-42 - Implement user registration endpoint
Status: Todo
Priority: P1
TDD Reference: Section 4.2

I'll now:
1. Mark ticket as "In Progress"
2. Create implementation plan
3. Create feature branch
4. Write tests first (TDD)
5. Implement the feature
6. Create PR
7. Mark ticket "Completed" after merge

Let me start by marking this ticket as "In Progress"...
```

### Scenario 4: Mid-Implementation Questions

**User:** "I'm working on the dashboard, but I'm not sure if we need real-time updates or polling is okay"

**Claude:**
```
Good question! This affects the technical implementation significantly.

Let me check the PRD and TDD for guidance...

[Checks PRD]
PRD states: "Dashboard updates every 30 seconds"
Non-functional requirement: "Data latency <30 seconds"

This suggests polling with 30-second intervals is acceptable, not real-time WebSocket updates.

**Recommendation: Use polling (30s interval)**

Pros:
- Simpler implementation
- Meets PRD requirement (<30s latency)
- Less server load

Cons:
- Not "truly" real-time
- Slightly higher client resource usage

Alternative: WebSocket for true real-time
Would require PRD update and more complex infrastructure.

**Should we proceed with 30-second polling as specified in the PRD?**
```

---

## Workflow Integration

### Linear MCP Integration

**Claude should use Linear MCP for:**
- Fetching ticket details
- Updating ticket status
- Adding comments to tickets
- Creating new tickets

**Example usage:**
```python
# Fetch ticket
ticket = linear.get_issue("PROJ-42")

# Update status
linear.update_issue("PROJ-42", status="In Progress")

# Add comment
linear.create_comment(
    issue_id="PROJ-42",
    body="Implementation started. Created branch: feature/PROJ-42-user-registration"
)
```

### GitHub Integration

**Claude should use `gh` CLI for:**
- Creating pull requests
- Linking PRs to Linear tickets

**Always include Linear ticket ID in PR:**
```bash
gh pr create \
  --title "feat(auth): implement user registration (PROJ-42)" \
  --body "Closes PROJ-42"
```

---

## Quality Checklists

### PRD Completeness

Before considering PRD complete:
- [ ] Problem statement is clear and validated
- [ ] User personas defined with pain points
- [ ] Success metrics are measurable (with targets)
- [ ] All user stories have acceptance criteria (Given/When/Then)
- [ ] Functional requirements listed with priorities
- [ ] Non-functional requirements specified (performance, security, etc.)
- [ ] Scope boundaries defined (in/out of scope)
- [ ] Dependencies identified
- [ ] Risks assessed with mitigation
- [ ] Timeline defined
- [ ] Stakeholder approval obtained

### TDD Completeness

Before considering TDD complete:
- [ ] Architecture diagram created
- [ ] All components documented
- [ ] Database schema defined (tables, indexes, relationships)
- [ ] API endpoints specified (request/response with examples)
- [ ] Core algorithms documented
- [ ] Error handling strategy defined
- [ ] Security considerations addressed
- [ ] Testing strategy complete (unit, integration, performance)
- [ ] Deployment process documented
- [ ] Monitoring approach defined
- [ ] All PRD requirements mapped to technical design

### Task Breakdown Completeness

Before considering task breakdown complete:
- [ ] All PRD requirements mapped to stories
- [ ] All TDD sections referenced in tickets
- [ ] All stories right-sized (<13 points)
- [ ] All stories have acceptance criteria
- [ ] All stories estimated
- [ ] Dependencies identified and documented
- [ ] Sprint goals defined
- [ ] Sprint capacity realistic
- [ ] Critical path identified
- [ ] Tickets created in Linear (via MCP or CLI)

### Implementation Completeness (Per Ticket)

Before marking ticket complete:
- [ ] Ticket marked "In Progress" at start
- [ ] Tests written BEFORE implementation
- [ ] All tests passing
- [ ] Code coverage >80%
- [ ] No linter warnings
- [ ] All acceptance criteria validated
- [ ] Documentation updated (docstrings, README)
- [ ] Code reviewed
- [ ] PR created with conventional commit
- [ ] PR includes "Closes TICKET-ID"
- [ ] PR merged to main
- [ ] Ticket marked "Completed"

---

## Failure & Rollback Procedures

Real projects encounter failures. These procedures ensure you can recover quickly and learn from issues.

### When PR Breaks Production

**Symptoms:**
- Error rate spike after deployment
- User reports of broken functionality
- Monitoring alerts triggered

**Immediate Actions (within 15 minutes):**

1. **Revert the PR:**
   ```bash
   git revert <commit-sha>
   git push origin main
   ```

2. **Deploy revert immediately:**
   ```bash
   # Trigger deployment of revert commit
   # Or rollback to previous version
   kubectl rollout undo deployment/service-name
   ```

3. **Notify team:**
   - Post in team channel
   - Update incident tracker
   - Notify stakeholders if user-facing

**Follow-up Actions (within 24 hours):**

4. **Root cause analysis:**
   - Why didn't tests catch this?
   - What was the failure mode?
   - What environments were affected?

5. **Add tests to prevent recurrence:**
   - Write test that reproduces the bug
   - Add to CI pipeline
   - Verify test fails without fix, passes with fix

6. **Re-implement properly:**
   - Create hotfix ticket (priority P0)
   - Follow linear-ticket-workflow with new tests
   - Get additional review before merge

**Example:**

```
PROJ-42 merged but caused 500 errors in /api/v1/usage endpoint

Immediate:
- Reverted commit abc123 within 10 minutes
- Service recovered, errors stopped
- Posted incident report in #engineering

Follow-up:
- Root cause: Didn't test with empty database (edge case)
- Added test: test_usage_endpoint_no_data()
- Created PROJ-43 (hotfix): Handle empty data gracefully
- Additional review: 2 engineers instead of 1
- Deployed PROJ-43 successfully 24h later
```

---

### When Sprint Goal Not Met

**Definition:** <70% of committed story points completed by sprint end

**Immediate Actions (sprint retrospective):**

1. **Analyze what went wrong:**
   - Were estimates accurate?
   - Were there blockers?
   - Did scope creep occur?
   - Were there team interruptions?

2. **Categorize incomplete work:**
   - Nearly done (>80% complete): Move to next sprint (high priority)
   - Partially done (30-80%): Re-estimate remaining work
   - Not started: Return to backlog

3. **Adjust velocity:**
   ```
   Old velocity: 20 points/sprint (planned)
   Actual completion: 12 points
   New velocity: 15 points/sprint (conservative)

   Next sprint planning: Commit to 15 points, not 20
   ```

4. **Re-estimate remaining work:**
   - Don't assume "10% left" means 1 point
   - Re-estimate from scratch based on actual progress

**Communication:**

5. **Update stakeholders:**
   ```markdown
   Sprint 2 Update:
   - Planned: 20 points
   - Completed: 12 points (60%)
   - Reason: Database migration took longer than expected
   - Impact: Feature launch delayed by 1 sprint (2 weeks)
   - Mitigation: Adjusted velocity, added buffer for Sprint 3
   ```

**Prevention:**

6. **Identify root cause:**
   - Technical: Unknown complexity, technical debt
   - Process: Poor estimation, unclear requirements
   - External: Dependencies, blockers, team changes

7. **Implement improvements:**
   - Add spike tickets for unknowns
   - Break down stories smaller
   - Front-load risky work
   - Leave 20% buffer in sprint planning

---

### When Feature Fails User Acceptance

**Symptoms:**
- Beta users don't use the feature
- Negative feedback after launch
- Success metrics not improving

**Immediate Actions (within 1 week):**

1. **Gather feedback:**
   - Talk to users (interviews, surveys)
   - Analyze usage data
   - Check error logs
   - Review support tickets

2. **Document learnings:**
   ```markdown
   Feature: API Usage Dashboard
   Expected: 70% adoption in first week
   Actual: 15% adoption

   User Feedback:
   - "Too complicated - too many filters"
   - "Doesn't show what I care about (costs)"
   - "Loads too slowly (5+ seconds)"

   Learnings:
   - We built what WE wanted, not what USERS needed
   - Didn't validate designs with beta users
   - Performance requirement (2s) not met in production
   ```

3. **Update PRD with insights:**
   - Add "What we learned" section
   - Update success metrics if they were wrong
   - Revise user stories based on real needs

**Iteration Plan:**

4. **Create v2 iteration:**
   - Create new PRD v2.0
   - Focus on top user pain points
   - Simplify based on feedback
   - Address performance issues

5. **Don't abandon - iterate:**
   ```
   Instead of: "Feature failed, move on"
   Do this: "Feature v1 taught us X, Y, Z. v2 will address this"

   Epic: Usage Dashboard v2
   - PROJ-50: Simplify to 1 default view (remove complexity)
   - PROJ-51: Add cost projection (what users actually want)
   - PROJ-52: Performance optimization (2s → 500ms)
   ```

6. **Ship incremental improvements:**
   - Don't wait for perfect v2
   - Ship improvements weekly
   - Measure impact of each change
   - Iterate based on data

**Example:**

```
Dashboard v1.0 failed (15% adoption)

Week 1: User interviews (found: too complex, missing costs)
Week 2: Simplified to single view (adoption: 15% → 30%)
Week 3: Added cost estimates (adoption: 30% → 50%)
Week 4: Performance fix (adoption: 50% → 65%)
Week 8: Hit 70% adoption target

Result: Success through iteration, not abandonment
```

---

### When Dependencies Block Work

**Scenario:** External team/service blocks your work

**Immediate Actions (same day):**

1. **Mark as blocked in Linear:**
   ```
   Status: Blocked
   Blocker: Data Team - Kafka topic not ready
   Impact: PROJ-2 cannot start, blocks PROJ-4, PROJ-6
   ```

2. **Communicate with dependency owner:**
   ```
   Hi Data Team,

   PROJ-2 depends on the Kafka topic for API events (discussed Jan 5).
   Original ETA was Jan 15, current status shows "In Progress."

   Questions:
   - Is Jan 15 still achievable?
   - Any blockers we can help with?
   - Alternative: Can we get sample data to develop against?

   Impact: Blocking our Sprint 1 goal (usage tracking).
   ```

3. **Escalate if no response (24 hours):**
   - Notify your manager
   - Ask for help unblocking
   - Involve their manager if needed

**Alternative Work (within 1 day):**

4. **Identify parallel work:**
   ```
   Blocked: PROJ-2 (5 points)
   Alternative: PROJ-8 (5 points, independent)

   Action: Start PROJ-8 while waiting for dependency
   ```

5. **Create workaround if possible:**
   ```
   Blocked: Real Kafka topic
   Workaround: Mock Kafka data for local development

   Benefit: Can develop and test locally
   Limitation: Can't deploy to staging yet
   ```

**Replan Sprint:**

6. **Adjust sprint commitment:**
   ```
   Original Sprint 1:
   - PROJ-1, PROJ-2, PROJ-3 (18 points)

   Replanned Sprint 1 (dependency blocked):
   - PROJ-1, PROJ-8, PROJ-9 (18 points)
   - Move PROJ-2, PROJ-3 to Sprint 2
   ```

7. **Document impact:**
   ```
   Dependency Delay:
   - Blocker: Data Team Kafka topic
   - Impact: 2-week delay on usage tracking feature
   - Mitigation: Worked on independent alerts feature instead
   - Communication: Stakeholders notified of delay
   ```

---

### When Tests Pass Locally But Fail in CI

**Common Causes:**

- Environment differences (dependencies, versions)
- Timing issues (race conditions)
- Resource constraints (memory, CPU)
- Test data issues

**Debug Process:**

1. **Check CI logs:**
   ```bash
   # Look for differences
   - Python version: local 3.11, CI 3.10?
   - Dependencies: different versions?
   - Database: SQLite local, Postgres CI?
   ```

2. **Reproduce locally:**
   ```bash
   # Run tests in CI-like environment
   docker run --rm -v $(pwd):/app python:3.11 pytest
   ```

3. **Fix and verify:**
   - Fix the issue
   - Run locally AND in CI
   - Both must pass before merging

**Prevention:**

- Use Docker for consistent environments
- Pin dependency versions
- Test against production-like databases
- Add timing assertions to catch race conditions

---

### General Recovery Principles

**1. Fail Fast, Recover Faster**
- Detect issues quickly (monitoring, alerts)
- Have rollback plan before deploying
- Practice rollbacks in staging

**2. Learn and Improve**
- Every failure is a learning opportunity
- Document what went wrong
- Add tests/safeguards to prevent recurrence
- Share learnings with team

**3. Don't Blame, Fix Systems**
- Humans make mistakes
- Fix the process, not the person
- Add automation to prevent human error

**4. Communicate Proactively**
- Tell stakeholders early when things go wrong
- Under-promise, over-deliver on fixes
- Provide regular updates during incidents

---

## Troubleshooting

### "I don't have time for all this process"

**Response depends on project size:**

**Small (<5 points, <1 day):**
- Lightweight PRD (bullet points, 15 min)
- Minimal TDD (key APIs and data models, 30 min)
- Direct implementation with tests

**Medium (5-20 points, 2-5 days):**
- 1-page PRD (30 min)
- Focused TDD (1-2 hours)
- Full task breakdown (1 hour)

**Large (>20 points, >1 week):**
- Complete PRD with stakeholder review
- Comprehensive TDD
- Detailed task breakdown with sprint planning

**Rule of thumb:** Documentation = ~10% of development time

### "Requirements keep changing"

**This is expected. Update the documents:**

1. Update PRD with new requirements
2. Update TDD with new technical approach
3. Update task breakdown (add/modify tickets)
4. Track changes in changelog

**Living documents adapt to changing requirements.**

### "We're Agile, not Waterfall"

**This IS agile:**
- PRD = User stories + Acceptance criteria
- TDD = Architecture decision records + Spike outcomes
- Task Breakdown = Sprint planning
- Implementation = Story development with TDD

**Documents are living, not frozen.**

---

## Success Metrics

Track these to measure workflow effectiveness:

**Quality:**
- Defect rate (bugs per feature)
- Rework rate (% of work redone)
- Test coverage (target: >80%)

**Efficiency:**
- Sprint completion rate (% of committed work done)
- Estimation accuracy (actual vs estimated)
- Cycle time (ticket creation → done)

**Team:**
- Developer satisfaction
- Onboarding time (new dev to productive)
- Context switching frequency

**Target improvements:**
- 50% reduction in rework
- 20% better estimation accuracy
- 30% faster onboarding

---

## Summary: Claude's Responsibilities

When following this workflow, Claude will:

1. **Guide the process** - Help user navigate workflows
2. **Ask clarifying questions** - Never assume when unclear
3. **Follow TDD** - Always write tests first
4. **Maintain traceability** - Link everything (code → ticket → TDD → PRD)
5. **Update Linear** - Keep ticket status current (via MCP)
6. **Ensure quality** - Run all Definition of Done checks
7. **Document thoroughly** - Update PRD/TDD as needed
8. **Communicate clearly** - Explain decisions and provide options

**Golden Rule:** Quality over speed. Better to ask questions and get it right than assume and build the wrong thing.

---

## Quick Reference

### Commands

| Command | Workflow |
|---------|----------|
| `Create a PRD for [feature] using the prd-creation-workflow` | PRD Creation |
| `Create a TDD based on this PRD using the tdd-creation-workflow` | TDD Creation |
| `Break down this PRD and TDD into tickets using the task-breakdown-workflow` | Task Breakdown |
| `Implement Linear ticket [ID] following the linear-ticket-workflow` | Implementation |

### File Locations

| Type | Location |
|------|----------|
| Workflows | `/workflows/*.md` |
| Templates | `/reference/*-template*.md` |
| This document | `/workflows/product-development-workflow.md` |

---

**Version:** 2.0
**Last Updated:** 2025-11-06
**Maintainer:** Mark
**Status:** Parent workflow - governs all other workflows
