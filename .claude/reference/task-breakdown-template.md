# Task Breakdown: [Feature Name]

**Created:** [Date]
**Author:** [Name]
**PRD Reference:** [Link to PRD]
**TDD Reference:** [Link to TDD]
**Target Sprint:** [Sprint number/name]

---

## Overview

**Feature:** [Feature name]

**Goal:** [One sentence summary of what we're building]

**Total Story Points:** [Estimated total]

**Estimated Duration:** [Number of sprints/weeks]

---

## Epic Structure

### Epic: [Epic Name]

**Description:** [High-level grouping of related stories]

**Goal:** [What this epic accomplishes]

**Stories:** [Number of stories in this epic]

**Story Points:** [Total points for epic]

---

## Story Breakdown

### Story 1: [Story Title]

**Epic:** [Epic name]

**Priority:** P0 (Critical) | P1 (High) | P2 (Medium) | P3 (Low)

**Story:**

```
As a [user type]
I want [capability]
So that [benefit]
```

**Acceptance Criteria:**

```gherkin
Scenario: [Scenario name]
  Given [initial context]
  When [action taken]
  Then [expected outcome]

Scenario: [Another scenario]
  Given [initial context]
  When [action taken]
  Then [expected outcome]
```

**Technical Requirements:**

- [ ] [Technical requirement 1 - from TDD Section X]
- [ ] [Technical requirement 2 - from TDD Section Y]
- [ ] [Technical requirement 3]

**TDD Reference:** Section [X.X]

**Dependencies:**

- Depends on: [Story ID/Name]
- Blocks: [Story ID/Name]
- Related: [Story ID/Name]

**Estimation:**

- Story Points: [1, 2, 3, 5, 8, 13]
- Dev Time: [X days]
- Test Time: [X days]

**Labels:**

- Type: `feature` | `bug` | `refactor` | `docs` | `test`
- Component: `api` | `frontend` | `database` | `infra`
- Sprint: `sprint-X`

**Definition of Done:**

- [ ] Code reviewed and approved
- [ ] Unit tests written (coverage >80%)
- [ ] Integration tests passing
- [ ] No linter warnings
- [ ] Documentation updated
- [ ] Manual testing completed
- [ ] PR merged to main

---

### Story 2: [Story Title]

[Follow same structure as Story 1]

---

## Tasks (Sub-tickets)

### Story 1 - Task Breakdown

Each story can be broken into smaller tasks for tracking:

#### Task 1.1: [Task name]

**Description:** [What needs to be done]

**Type:** Setup | Implementation | Testing | Documentation

**Estimated Time:** [X hours]

**Checklist:**

- [ ] [Specific action item 1]
- [ ] [Specific action item 2]
- [ ] [Specific action item 3]

**Files to Modify/Create:**

- `src/components/FeatureName.tsx`
- `tests/test_feature.py`
- `docs/api-reference.md`

#### Task 1.2: [Task name]

[Follow same structure]

---

## Sprint Planning

### Sprint 1: [Sprint Name]

**Duration:** [Start date] - [End date]

**Goal:** [Sprint goal aligned with epic/stories]

**Capacity:** [Total story points team can handle]

**Stories Included:**

| Story ID | Title | Points | Assignee | Status |
|----------|-------|--------|----------|--------|
| PROJ-1 | [Story title] | 5 | [Name] | Todo |
| PROJ-2 | [Story title] | 3 | [Name] | Todo |
| PROJ-3 | [Story title] | 8 | [Name] | Todo |

**Total Points:** 16

**Dependencies:**

- PROJ-1 must complete before PROJ-3 can start
- PROJ-2 is independent (can start immediately)

**Risks:**

- [Risk description and mitigation]

---

### Sprint 2: [Sprint Name]

[Follow same structure as Sprint 1]

---

## Dependency Graph

```
PROJ-1 (Setup)
  ↓
PROJ-3 (Core Feature)
  ↓
PROJ-5 (Integration)

PROJ-2 (Parallel Work)
  ↓
PROJ-4 (Related Feature)
```

**Critical Path:**

PROJ-1 → PROJ-3 → PROJ-5 (Must complete in order)

**Parallel Tracks:**

- Track A: PROJ-1 → PROJ-3 → PROJ-5
- Track B: PROJ-2 → PROJ-4 (Can run simultaneously)

---

## Linear Ticket Template

Use this format when creating tickets in Linear:

### Ticket Title Format

```
[Type]: [Brief description] (Component)

Examples:
feat: Add asset request API endpoint (API)
fix: Handle duplicate request errors (API)
test: Add integration tests for asset creation (Testing)
docs: Update API reference for new endpoints (Docs)
```

### Ticket Description Template

```markdown
## User Story

As a [user type]
I want [capability]
So that [benefit]

## Context

[Why are we doing this? Link to PRD section]

## Acceptance Criteria

- [ ] [Specific, testable criterion 1]
- [ ] [Specific, testable criterion 2]
- [ ] [Specific, testable criterion 3]

## Technical Details

**TDD Reference:** Section [X.X]

**Implementation Approach:**
[Brief description of how to implement]

**API Changes:**
- New endpoint: POST /api/v1/resources
- New response schema: {id, status, created_at}

**Database Changes:**
- New table: resource_requests
- New index: idx_user_id_created

**Dependencies:**
- Depends on: PROJ-X
- Blocked by: PROJ-Y

## Testing Requirements

**Unit Tests:**
- [ ] Test happy path (200 response)
- [ ] Test error cases (400, 401, 409)
- [ ] Test edge cases (empty params, duplicates)

**Integration Tests:**
- [ ] Test end-to-end flow
- [ ] Test with real database
- [ ] Test error handling

## Files to Modify

- `src/api/routes/resources.py` - Add new endpoint
- `src/models/resource.py` - Add Resource model
- `tests/test_resources.py` - Add test suite
- `docs/api-reference.md` - Document new endpoint

## Estimation

**Story Points:** [1, 2, 3, 5, 8, 13]

**Breakdown:**
- Implementation: [X hours]
- Testing: [X hours]
- Documentation: [X hours]
- Review/QA: [X hours]

## Definition of Done

- [ ] Code reviewed and approved
- [ ] Unit tests passing (coverage >80%)
- [ ] Integration tests passing
- [ ] No linter warnings (ruff, mypy)
- [ ] Documentation updated
- [ ] Manual testing completed
- [ ] PR merged to main
- [ ] Deployed to staging

## Labels

- Priority: `p0-critical` | `p1-high` | `p2-medium` | `p3-low`
- Type: `feature` | `bug` | `refactor` | `docs` | `test`
- Component: `api` | `frontend` | `database` | `infrastructure`
- Sprint: `sprint-X`
- Epic: `[epic-name]`

## References

- PRD: [Link to PRD]
- TDD: [Link to TDD Section X.X]
- Design: [Link to design mocks]
- Related Tickets: PROJ-X, PROJ-Y
```

---

## Estimation Guide

### Story Point Scale (Fibonacci)

| Points | Complexity | Time | Example |
|--------|------------|------|---------|
| 1 | Trivial | 1-2 hours | Add a simple field, update docs |
| 2 | Simple | 2-4 hours | Basic CRUD endpoint, simple UI component |
| 3 | Moderate | 4-8 hours | API endpoint with validation, form with validation |
| 5 | Complex | 1-2 days | Feature with database changes, complex logic |
| 8 | Very Complex | 2-3 days | Integration with external service, major refactor |
| 13 | Highly Complex | 3-5 days | Multi-component feature, architectural changes |

**Note:** Stories >13 points should be broken down further.

### Estimation Factors

Consider these when estimating:

- **Complexity:** How difficult is the logic?
- **Uncertainty:** How well do we understand the requirements?
- **Dependencies:** How many external dependencies?
- **Testing:** How much testing is required?
- **Documentation:** How much documentation needs updating?

---

## Ticket Prioritization

### Priority Matrix

| Priority | Description | Timeline | Examples |
|----------|-------------|----------|----------|
| P0 | Critical | Immediate | Production bug, security issue, blocker |
| P1 | High | This sprint | Core feature, major improvement |
| P2 | Medium | Next 2 sprints | Enhancement, minor feature |
| P3 | Low | Future | Nice to have, technical debt |

### Prioritization Criteria

1. **User Impact:** How many users affected?
2. **Business Value:** How much revenue/engagement impact?
3. **Dependencies:** Is this blocking other work?
4. **Risk:** What's the risk of not doing this?
5. **Effort:** What's the ROI (value/effort)?

---

## Checklist for Task Breakdown

Before creating tickets, verify:

- [ ] All PRD requirements mapped to stories
- [ ] All TDD sections referenced in tickets
- [ ] Dependencies clearly identified
- [ ] Stories are right-sized (<13 points)
- [ ] Acceptance criteria are testable
- [ ] Definition of Done is clear
- [ ] Sprint capacity is realistic
- [ ] Critical path identified
- [ ] Risks documented
- [ ] Labels and metadata complete

---

## Example: Complete Story Breakdown

### Story: Implement Asset Request API

**Epic:** Asset Management API

**Priority:** P1 (High)

**User Story:**

```
As an API consumer
I want to request 3D asset generation via POST /api/v1/assets
So that I can initiate asynchronous asset creation
```

**Acceptance Criteria:**

```gherkin
Scenario: Successful asset request
  Given I have valid API credentials
  And I provide valid format and parameters
  When I POST to /api/v1/assets
  Then I receive a 202 Accepted response
  And I receive an asset_id, status, and created_at timestamp

Scenario: Duplicate request handling
  Given I have already requested the same asset
  When I POST the same request again
  Then I receive a 409 Conflict response
  And I receive the existing asset details

Scenario: Invalid format error
  Given I provide an unsupported format
  When I POST to /api/v1/assets
  Then I receive a 400 Bad Request response
  And I receive error details listing valid formats
```

**Technical Requirements:**

- [ ] Create POST /api/v1/assets endpoint (TDD Section 6.1)
- [ ] Implement request validation (TDD Section 7.2)
- [ ] Add database model for asset_requests (TDD Section 3.1)
- [ ] Implement deduplication logic (TDD Section 6.1.2)
- [ ] Add error handling for 400, 401, 409 (TDD Section 5)
- [ ] Write unit tests with >80% coverage (TDD Section 8.1)

**TDD Reference:** Section 6.1

**Dependencies:**

- Depends on: PROJ-10 (Database schema migration)
- Blocks: PROJ-12 (Asset status polling endpoint)

**Estimation:** 5 points (1-2 days)

**Task Breakdown:**

1. **Setup (1 hour)**
   - [ ] Create route file: `src/api/routes/assets.py`
   - [ ] Add route registration to FastAPI app

2. **Database Model (2 hours)**
   - [ ] Create AssetRequest model
   - [ ] Write migration script
   - [ ] Test migration on local database

3. **API Implementation (4 hours)**
   - [ ] Implement POST /api/v1/assets handler
   - [ ] Add request validation
   - [ ] Implement deduplication check
   - [ ] Add error handling

4. **Testing (3 hours)**
   - [ ] Write unit tests (success, duplicate, errors)
   - [ ] Write integration tests
   - [ ] Verify coverage >80%

5. **Documentation (1 hour)**
   - [ ] Update API reference docs
   - [ ] Add docstrings to all functions
   - [ ] Add example requests/responses

**Files to Modify:**

- `src/api/routes/assets.py` (create)
- `src/models/asset.py` (create)
- `tests/test_assets.py` (create)
- `docs/api-reference.md` (update)
- `alembic/versions/XXX_add_asset_requests.py` (create)

**Labels:**

- Type: `feature`
- Component: `api`
- Sprint: `sprint-5`
- Epic: `asset-management`
- Priority: `p1-high`

---

## Sprint Velocity Tracking

Track velocity to improve estimation:

| Sprint | Planned Points | Completed Points | Velocity |
|--------|----------------|------------------|----------|
| Sprint 1 | 20 | 18 | 90% |
| Sprint 2 | 21 | 21 | 100% |
| Sprint 3 | 22 | 20 | 91% |

**Average Velocity:** 20 points per sprint

**Use this to plan future sprints:** If average velocity is 20, plan ~18-20 points per sprint to avoid over-commitment.

---

## Appendix

### Common Ticket Types

**Feature:** New capability or enhancement
**Bug:** Something broken that needs fixing
**Refactor:** Code improvement without behavior change
**Test:** Adding or improving tests
**Docs:** Documentation updates
**Chore:** Maintenance work (dependency updates, etc.)

### Useful Linear Commands

```bash
# Create ticket via CLI (if using Linear CLI)
linear issue create \
  --title "feat: Add asset request endpoint" \
  --description "$(cat ticket-description.md)" \
  --priority 1 \
  --label feature \
  --label api \
  --estimate 5

# Link tickets
linear issue PROJ-3 \
  --add-link "blocks PROJ-5"
```

### References

- [Link to PRD]
- [Link to TDD]
- [Link to Sprint Planning Guide]
