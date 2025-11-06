# Task Breakdown & Sprint Planning Workflow

**Purpose:** A structured process for breaking down PRD and TDD into actionable Linear tickets organized into sprints.

---

## Overview

This workflow ensures:

-  Every PRD requirement mapped to tickets
-  All TDD sections referenced in implementation tasks
-  Stories sized appropriately (<13 points)
-  Dependencies clearly identified
-  Sprint capacity is realistic
-  Critical path defined
-  Tickets contain all necessary context

---

## Quick Start

When ready to break down a project, say:

> "I have a PRD and TDD for [feature]. Let's create a task breakdown using the task-breakdown-workflow."

Or:

> "Break down the API usage dashboard into Linear tickets and create a sprint plan"

---

## The Workflow

### **Phase 1: Review PRD & TDD**

#### Step 1.1: Extract User Stories

**Claude will review the PRD and extract:**

- All user stories
- Acceptance criteria for each
- Priority levels (Must Have / Should Have / Nice to Have)
- Success metrics

**Example:**

```
User Stories from PRD:

Story 1: View Real-Time Usage Dashboard
- As a developer
- I want to see my API usage in real-time
- So that I can monitor usage and avoid unexpected charges
- Priority: Must Have
- Acceptance Criteria: 8 items

Story 2: Filter Usage by Project
- As a developer
- I want to filter usage by project
- So that I can track usage per project
- Priority: Must Have
- Acceptance Criteria: 4 items

Story 3: Set Usage Alerts
- As a developer
- I want to set usage alerts
- So that I get notified before hitting limits
- Priority: Should Have
- Acceptance Criteria: 6 items
```

#### Step 1.2: Map Technical Requirements

**Claude will review the TDD and extract:**

- Components to build
- Database changes needed
- API endpoints to create
- Infrastructure requirements

**Example:**

```
Technical Components from TDD:

1. Database Schema (TDD Section 3.1)
   - Create api_usage_metrics table
   - Add indexes
   - Set up partitioning

2. Dashboard API (TDD Section 4)
   - GET /api/v1/usage - retrieve metrics
   - GET /api/v1/usage/summary - aggregated stats
   - POST /api/v1/alerts - create alert

3. Frontend Dashboard (TDD Section 2.2)
   - Usage chart component
   - Filter controls
   - Alert configuration UI

4. Background Services (TDD Section 6.1)
   - Kafka consumer for tracking
   - Alert checker (cron job)
```

---

### **Phase 2: Define Epic Structure**

#### Step 2.1: Group Related Work

**Claude will help you organize stories into epics:**

- Epic = High-level theme or feature area
- Contains multiple related stories
- Has a clear goal

**Example:**

```
Epic 1: Usage Tracking Infrastructure
Goal: Set up backend systems to collect and store API usage data
Stories: 4
Estimated Points: 21

Epic 2: Usage Dashboard
Goal: Build user-facing dashboard to view usage metrics
Stories: 3
Estimated Points: 18

Epic 3: Usage Alerts
Goal: Enable users to set and receive usage alerts
Stories: 2
Estimated Points: 13

Total: 9 stories, 52 points (~2-3 sprints for team of 3)
```

#### Step 2.2: Prioritize Epics

**Claude will ask:**

- Which epic is foundational (must be done first)?
- Which epic delivers the most user value?
- Which epic has the most risk?

**Priority Order:**

```
Priority 1: Usage Tracking Infrastructure (foundational)
Priority 2: Usage Dashboard (high user value)
Priority 3: Usage Alerts (enhancement)
```

---

### **Phase 3: Break Down Stories into Tasks**

#### Step 3.1: Decompose Each Story

**For each user story, Claude will create tasks:**

- Database changes
- API implementation
- Frontend implementation
- Testing
- Documentation

**Example:**

```
Story: View Real-Time Usage Dashboard

Task 1: Database Setup
- Create api_usage_metrics table
- Add indexes (user_id, timestamp)
- Set up monthly partitioning
- Write migration script
- TDD Reference: Section 3.1
- Estimate: 3 points

Task 2: Implement GET /api/v1/usage Endpoint
- Create FastAPI route
- Implement query logic with time_bucket aggregation
- Add caching (Redis, 5-min TTL)
- Handle error cases (400, 401, 404)
- TDD Reference: Section 4.1, 6.1
- Estimate: 5 points

Task 3: Build Dashboard UI Component
- Create UsageDashboard React component
- Integrate Chart.js for time-series graph
- Add date range picker
- Handle loading and error states
- TDD Reference: Section 2.2
- Estimate: 5 points

Task 4: Write Tests
- Unit tests for API endpoint
- Integration tests for database queries
- Frontend component tests
- TDD Reference: Section 8.1
- Estimate: 3 points

Task 5: Documentation
- API reference docs
- User guide (how to read dashboard)
- Inline code comments
- Estimate: 2 points

Total for Story: 18 points
```

**Claude will note:** "This story is >13 points, so we should split it into smaller stories."

#### Step 3.2: Right-Size Stories

**Claude will help you split large stories:**

- Break by technical layer (backend vs frontend)
- Break by functionality (view vs filter)
- Ensure each story delivers value independently

**Example:**

```
Original Story: View Real-Time Usage Dashboard (18 points)

Split into:

Story 1A: Usage API Endpoint (Backend)
- Database setup
- API implementation
- Tests
- TDD Reference: Sections 3.1, 4.1, 6.1
- Estimate: 8 points

Story 1B: Usage Dashboard UI (Frontend)
- React component
- Chart integration
- Tests
- Depends on: Story 1A
- TDD Reference: Section 2.2
- Estimate: 5 points

Story 1C: Documentation
- API docs
- User guide
- Depends on: Story 1A, Story 1B
- Estimate: 2 points

Now each story is <13 points 
```

---

### **Phase 4: Estimation**

#### Step 4.1: Estimate Story Points

**Claude will use Fibonacci scale:**

| Points | Complexity | Time | Example |
|--------|------------|------|---------|
| 1 | Trivial | 1-2 hours | Add field, update docs |
| 2 | Simple | 2-4 hours | Basic CRUD, simple component |
| 3 | Moderate | 4-8 hours | Endpoint with validation |
| 5 | Complex | 1-2 days | Feature with DB changes |
| 8 | Very Complex | 2-3 days | Integration with external service |
| 13 | Highly Complex | 3-5 days | Multi-component feature |

**Claude will ask:**

- How complex is the logic?
- How well understood are the requirements?
- How many dependencies?
- How much testing is needed?

**Example:**

```
Story: Implement GET /api/v1/usage Endpoint

Complexity: Moderate-Complex
- Database query with time_bucket (moderate)
- Caching logic (simple)
- Error handling (simple)
- Authentication integration (simple)

Understanding: High (TDD Section 4.1 is detailed)

Dependencies: 1 (database schema must exist)

Testing: Standard (unit + integration)

Estimate: 5 points 
```

#### Step 4.2: Validate Estimates

**Claude will check:**

- Total points reasonable for team size?
- Any stories >13 points? (should split)
- Balanced across sprints?

---

### **Phase 5: Identify Dependencies**

#### Step 5.1: Map Story Dependencies

**Claude will create dependency graph:**

```
PROJ-1: Database Schema
  �
PROJ-2: Usage API Endpoint
  �
PROJ-4: Usage Dashboard UI
  �
PROJ-6: End-to-End Tests

PROJ-3: Alert API Endpoint (parallel track)
  �
PROJ-5: Alert UI (parallel track)

Critical Path: PROJ-1 � PROJ-2 � PROJ-4 � PROJ-6
Parallel Track: PROJ-3 � PROJ-5
```

**Dependencies types:**

- **Blocks:** PROJ-1 blocks PROJ-2 (must complete first)
- **Depends on:** PROJ-4 depends on PROJ-2
- **Related:** PROJ-3 and PROJ-2 are related but independent

#### Step 5.2: Identify External Dependencies

**Claude will list:**

- Dependencies on other teams
- Third-party integrations
- Infrastructure requirements

**Example:**

```
External Dependencies:

- Data Team: Kafka topic for API events (ETA: Jan 15)
  Blocks: PROJ-1 (can't test without real data)

- Design Team: Dashboard mockups (ETA: Jan 10)
  Blocks: PROJ-4 (need designs to build UI)

- DevOps: TimescaleDB setup in staging (ETA: Jan 12)
  Blocks: PROJ-2 (need DB to develop against)

Action: Track these dependencies, create tickets for follow-up
```

---

### **Phase 6: Create Sprint Plan**

#### Step 6.1: Define Sprint Goals

**Claude will help you set goals for each sprint:**

```
Sprint 1 (Jan 15 - Jan 26)
Goal: Build backend infrastructure for usage tracking
Capacity: 20 points (team of 3, velocity ~20)

Stories:
- PROJ-1: Database schema (3 points)
- PROJ-2: Usage API endpoint (5 points)
- PROJ-3: Alert API endpoint (5 points)
- PROJ-7: Kafka consumer setup (5 points)
Total: 18 points

Sprint 2 (Jan 29 - Feb 9)
Goal: Build frontend dashboard and integrate with backend
Capacity: 20 points

Stories:
- PROJ-4: Usage dashboard UI (5 points)
- PROJ-5: Alert UI (5 points)
- PROJ-8: Integration testing (3 points)
- PROJ-9: Performance optimization (5 points)
Total: 18 points

Sprint 3 (Feb 12 - Feb 23)
Goal: Polish, docs, and launch prep
Capacity: 20 points

Stories:
- PROJ-6: End-to-end tests (3 points)
- PROJ-10: Documentation (2 points)
- PROJ-11: User onboarding flow (5 points)
- PROJ-12: Beta rollout (3 points)
- PROJ-13: Monitoring setup (3 points)
Total: 16 points
```

#### Step 6.2: Balance Sprints

**Claude will check:**

- Is each sprint within capacity?
- Does each sprint deliver value?
- Are dependencies respected?

**Claude will warn:**

```
�  Sprint 1 has PROJ-2 and PROJ-3, but PROJ-2 depends on PROJ-1.
Recommendation: Ensure PROJ-1 completes in first week so PROJ-2 can start.

 Sprint 2 looks balanced
 Sprint 3 has buffer (16 vs 20 capacity) for unexpected work
```

---

### **Phase 7: Generate Linear Tickets**

#### Step 7.1: Create Ticket for Each Story

**Claude will generate tickets using this template:**

```markdown
Title: feat: Implement GET /api/v1/usage endpoint (API)

## User Story

As a developer
I want to retrieve my API usage metrics via API
So that I can display usage in the dashboard

## Context

This implements the backend API for the usage dashboard. Users will call this
endpoint to fetch their usage data for a given date range.

**PRD Reference:** User Story 1
**TDD Reference:** Section 4.1 (API Specification), Section 6.1 (Core Logic)

## Acceptance Criteria

- [ ] Endpoint accepts start_date, end_date, granularity query params
- [ ] Returns total requests, requests over time, avg response time, error rate
- [ ] Response time <200ms (p95)
- [ ] Caches results for 5 minutes
- [ ] Handles errors: 400 (invalid params), 401 (unauthorized), 404 (no data)
- [ ] Unit tests with >80% coverage
- [ ] Integration tests with real database

## Technical Details

**TDD Reference:** Section 4.1, 6.1

**Implementation:**
- Create FastAPI route: GET /api/v1/usage
- Query TimescaleDB with time_bucket aggregation
- Cache in Redis (5-min TTL)
- Return JSON with UsageMetrics schema

**Database Query:**
```sql
SELECT
  time_bucket('1 hour', timestamp) AS bucket,
  COUNT(*) as count,
  AVG(response_time_ms) as avg_response_time
FROM api_usage_metrics
WHERE user_id = %s AND timestamp BETWEEN %s AND %s
GROUP BY bucket
ORDER BY bucket
```

**Files to Modify:**
- `src/api/routes/usage.py` (create)
- `src/models/usage.py` (create)
- `tests/test_usage_api.py` (create)

**Dependencies:**
- Depends on: PROJ-1 (database schema must exist)
- Blocks: PROJ-4 (frontend needs API)

## Testing Requirements

**Unit Tests:**
- [ ] Test successful query (200 response)
- [ ] Test invalid date range (400 error)
- [ ] Test unauthorized (401 error)
- [ ] Test no data (404 error)
- [ ] Test cache hit (no DB query)

**Integration Tests:**
- [ ] Test with real TimescaleDB
- [ ] Test with 1M rows of data
- [ ] Verify response time <200ms

## Estimation

**Story Points:** 5

**Breakdown:**
- Implementation: 4 hours
- Testing: 3 hours
- Code review: 1 hour

## Definition of Done

- [ ] Code reviewed and approved
- [ ] Unit tests passing (coverage >80%)
- [ ] Integration tests passing
- [ ] No linter warnings (ruff, mypy)
- [ ] Documentation updated (docstrings, API reference)
- [ ] Manual testing completed
- [ ] PR merged to main

## Labels

- Priority: `p1-high`
- Type: `feature`
- Component: `api`
- Sprint: `sprint-1`
- Epic: `usage-dashboard`
- Estimate: `5`

## References

- PRD: [Link to PRD - User Story 1]
- TDD: [Link to TDD - Section 4.1, 6.1]
```

#### Step 7.2: Create Tickets in Linear

**Claude will help you create tickets:**

Option 1: Use Linear CLI

```bash
linear issue create \
  --title "feat: Implement GET /api/v1/usage endpoint (API)" \
  --description "$(cat ticket-description.md)" \
  --priority 1 \
  --label feature \
  --label api \
  --estimate 5 \
  --project "Usage Dashboard"
```

Option 2: Use Linear MCP

Claude can use Linear MCP (Model Context Protocol) to create tickets directly through the MCP integration.

Option 3: Manual creation (Claude provides formatted description to paste)

**Claude will say:**

```
I've created 9 ticket descriptions. Here are options for creating them in Linear:

1. Use Linear CLI (recommended): I can generate bash commands
2. Use Linear MCP: I can create tickets directly through MCP integration
3. Manual: Copy-paste each description into Linear web UI

Which would you prefer?
```

---

### **Phase 8: Review & Validate**

#### Step 8.1: Completeness Check

**Claude will verify:**

- [ ] All PRD requirements mapped to stories
- [ ] All TDD sections referenced in tickets
- [ ] All stories have acceptance criteria
- [ ] All stories are estimated
- [ ] All dependencies identified
- [ ] Sprint capacity is realistic
- [ ] Critical path identified

**Example:**

```
Completeness Check:

 PRD User Stories: 3 � Tickets created: 9 (stories split for sizing)
 TDD Sections: 8 � All referenced in tickets
 Acceptance Criteria: All tickets have 4-8 criteria
 Estimates: All tickets sized (1-8 points)
 Dependencies: 6 dependencies documented
 Sprint Capacity: 18, 18, 16 vs capacity 20 
 Critical Path: PROJ-1 � PROJ-2 � PROJ-4 � PROJ-6
```

#### Step 8.2: Validate Against PRD Goals

**Claude will check:**

- Do these tickets deliver all PRD requirements?
- Will this meet the success metrics?
- Is anything missing?

**Example:**

```
PRD Goals Validation:

Goal: Enable developers to monitor API usage in real-time

 PROJ-2: Usage API endpoint (delivers metrics)
 PROJ-4: Usage dashboard UI (displays metrics)
 PROJ-7: Kafka consumer (enables real-time tracking)
 All acceptance criteria from PRD covered

Success Metric: 70% of users view dashboard in first week

 PROJ-11: User onboarding flow (encourages adoption)
 PROJ-12: Beta rollout (early user testing)

All PRD goals covered 
```

#### Step 8.3: Risk Assessment

**Claude will identify risks:**

```
Risks:

1. PROJ-1 delayed by Data Team dependency
   - Impact: Blocks entire Sprint 1
   - Mitigation: Daily check-ins with Data Team, have backup plan (mock data)

2. PROJ-4 larger than estimated (5 points)
   - Impact: Sprint 2 overrun
   - Mitigation: Break into smaller tasks, pair programming

3. New technology (TimescaleDB) learning curve
   - Impact: Slower development in Sprint 1
   - Mitigation: Spike ticket for learning (1-2 days), documentation

Actions:
- Add PROJ-0: TimescaleDB learning spike (2 points, Sprint 1)
- Track Data Team dependency weekly
- Schedule mid-sprint check-in for PROJ-4
```

---

## Task Breakdown Template

**Claude will use this template:** See [reference/task-breakdown-template.md](../reference/task-breakdown-template.md)

---

## Best Practices

### 1. Keep Stories Independent

Each story should deliver value on its own. Avoid stories like "Create database table" that don't provide user value independently.

 Good: "Implement usage API endpoint" (includes DB + API + tests)
L Bad: "Create usage table" (no user value alone)

### 2. Size Stories Consistently

Use the same team to estimate. Over time, velocity will stabilize.

Track actual time vs estimates to improve future estimates.

### 3. Front-Load Risk

Put risky or uncertain work in early sprints. Don't save hard problems for the end.

### 4. Build Vertical Slices

Each sprint should deliver an end-to-end feature (backend + frontend + tests), not just "backend sprint" then "frontend sprint."

### 5. Leave Buffer

Don't plan to 100% capacity. Leave 10-20% buffer for:

- Bug fixes
- Unplanned work
- Overruns

### 6. Reference TDD Sections

Every ticket should reference specific TDD sections. This ensures engineers have all the context they need.

---

## Example Conversation Flow

**You:**

```
I have a PRD and TDD for the API usage dashboard. Let's break this down into tickets and create a sprint plan.
```

**Claude:**

```
I'll help you break down the API usage dashboard into actionable Linear tickets.

Let me start by reviewing the PRD and TDD.

[Reviews documents]

I've identified:
- 3 user stories from PRD
- 8 technical components from TDD
- Estimated 52 story points total (~2-3 sprints)

Before we proceed, I have a few questions:

1. What's your team size and typical sprint velocity?
2. What's your target launch date?
3. Are there any hard dependencies I should know about?
```

**You:**

```
Team size: 3 developers
Sprint velocity: ~20 points per sprint
Target launch: End of February (10 weeks, ~5 sprints available)
Dependencies: Data team needs to set up Kafka topic by Jan 15
```

**Claude:**

```
Perfect! With 3 developers and velocity of 20 points/sprint, we can plan:

Sprint 1 (Jan 15-26): Infrastructure (18 points)
Sprint 2 (Jan 29-Feb 9): Frontend (18 points)
Sprint 3 (Feb 12-23): Polish & Launch Prep (16 points)

Total: 52 points across 3 sprints (2 sprints buffer before end of Feb) 

I've identified 1 external dependency:
- Data Team: Kafka topic setup (Jan 15)
  This blocks PROJ-1, so we need confirmation it's on track.

Shall I proceed with creating the epic structure and breaking down stories?
```

---

## Prompts You Can Use

### Starting task breakdown

```
Break down this PRD and TDD into Linear tickets using the task-breakdown-workflow
```

### Creating sprint plan

```
Create a 3-sprint plan for this feature breakdown
```

### Estimating stories

```
Help me estimate story points for these tasks
```

### Identifying dependencies

```
What are the dependencies between these stories?
```

### Generating tickets

```
Generate Linear ticket descriptions for all stories
```

---

## Integration with Linear Ticket Workflow

Once tickets are created in Linear:

```
Tickets created! Ready to start implementation.

To implement a ticket, use the linear-ticket-workflow:
"Implement Linear ticket PROJ-1 following the workflow"
```

Engineers will use the linear-ticket-workflow to implement each ticket with TDD.

---

## Checklist

Before finalizing task breakdown:

- [ ] All PRD user stories mapped to tickets
- [ ] All TDD sections referenced
- [ ] Stories right-sized (<13 points)
- [ ] Acceptance criteria clear and testable
- [ ] Dependencies identified and documented
- [ ] Sprint goals defined
- [ ] Sprint capacity realistic (not over-committed)
- [ ] Critical path identified
- [ ] Risks assessed and mitigated
- [ ] Tickets contain all context (PRD, TDD references)
- [ ] Definition of Done clear
- [ ] Labels and metadata complete

---

## Continuous Refinement

**After each sprint:**

- Update velocity based on actual completion
- Adjust future sprint capacity
- Reprioritize backlog if needed
- Refine estimates based on actuals

**Claude can help:**

```
Update the sprint plan based on Sprint 1 results:
- Completed: 16/18 points
- Carried over: PROJ-2 (2 points remaining)
- New velocity: 18 points (down from 20)
```

---

**Version:** 1.0
**Last Updated:** 2025-11-05
