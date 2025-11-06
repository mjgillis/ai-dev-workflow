# Linear Ticket Implementation Workflow

**Purpose:** A repeatable process for implementing Linear stories using Claude Code with TDD principles.

---

## Overview

This workflow ensures that every Linear ticket is implemented consistently with:

- ✅ Test-Driven Development (TDD) approach
- ✅ Proper git workflow
- ✅ Complete acceptance criteria validation
- ✅ Documentation updates
- ✅ Definition of Done checklist

---

## Quick Start

When starting a new ticket, say:

> "I want to implement Linear ticket [TICKET-ID]. Let's follow the linear-ticket-workflow."

Or for a specific ticket:

> "Implement ticket ACME-123 following the workflow"

---

## The Workflow

### **Phase 1: Ticket Analysis & Planning**

#### Step 1.1: Fetch Ticket Details

**Claude should:**

- Ask for the Linear ticket ID (e.g., `ACME-123`)
- Fetch ticket details using Linear API or ask user to paste ticket description
- Display:
  - Title
  - User story (As a... I want... So that...)
  - Acceptance Criteria
  - Definition of Done
  - Labels (priority, type, repo)
  - Estimate

**Example Prompt:**

```
Fetch Linear ticket ACME-5 and display its details.
```

#### Step 1.2: Review Related Documentation

**Claude should:**

- Check if ticket references TDD sections (e.g., "See TDD Section 6.1")
- Read relevant documentation files
- Identify dependencies or blockers
- Ask clarifying questions if anything is ambiguous

**Example:**

```
Ticket references "TDD Section 6.1". Let me read that:
- Section 6.1 covers request_asset() method
- Expected inputs: format (str), parameters (dict)
- Expected output: dict with asset_id, status, created_at
```

#### Step 1.3: Create Implementation Plan

**Claude should:**

- Break down acceptance criteria into actionable steps
- Identify test cases from Given/When/Then scenarios
- Propose implementation approach
- Ask for user approval before proceeding

**Example:**

```
Implementation Plan for ACME-5:
1. Write unit tests for request_asset() (TDD approach)
   - Test 202 success response
   - Test 409 duplicate handling
2. Implement request_asset() method
   - POST to /api/v1/assets
   - Return dict with asset_id, status
3. Run tests and verify they pass
4. Update documentation (docstrings)
5. Mark acceptance criteria as complete

Proceed with this plan? [yes/no]
```

---

### **Phase 2: Git Workflow Setup**

#### Step 2.1: Create Feature Branch

**Claude should:**

- Check current branch
- Create feature branch following naming convention: `feature/ACME-123-short-description`
- Verify clean working directory

**Example:**

```bash
git checkout -b feature/ACME-5-implement-request-asset
```

**Naming Convention:**

- `feature/` - for new features
- `fix/` - for bug fixes
- `refactor/` - for refactoring
- `docs/` - for documentation only

#### Step 2.2: Verify Starting State

**Claude should:**

- Run existing tests to ensure clean baseline
- Check that environment is set up correctly
- List any prerequisites

---

### **Phase 3: Test-Driven Development (TDD)**

#### Step 3.1: Write Failing Tests FIRST

**Claude should:**

- Create test file if it doesn't exist
- Write tests based on acceptance criteria
- Use Given/When/Then from ticket
- Run tests to verify they FAIL (Red phase)

**Example:**

```python
# tests/test_client.py

def test_request_asset_success():
    """
    Given valid format and parameters
    When I call client.request_asset()
    Then I receive asset_id and status
    """
    # Arrange
    client = AssetClient(api_url="http://test", api_key="test_key")

    # Mock the response
    with responses.RequestsMock() as rsps:
        rsps.add(
            responses.POST,
            "http://test/api/v1/assets",
            json={"asset_id": "123", "status": "pending"},
            status=202
        )

        # Act
        result = client.request_asset(parameters={"output_format": "gltf"})

        # Assert
        assert result["asset_id"] == "123"
        assert result["status"] == "pending"
```

**Key Point:** Tests should fail initially because implementation doesn't exist yet.

#### Step 3.2: Implement Minimal Code to Pass Tests (Green phase)

**Claude should:**

- Write just enough code to make tests pass
- Follow the TDD section specifications
- Keep implementation simple and focused

**Example:**

```python
# src/asset_client/client.py

def request_asset(self, format: str, parameters: dict) -> dict:
    """Request 3D asset generation from middleware.

    Args:
        format: Asset format (e.g., "gltf", "obj")
        parameters: Generation parameters

    Returns:
        dict with asset_id, status, created_at

    Raises:
        ValidationError: If parameters are invalid
        AuthenticationError: If API key is invalid
    """
    response = self.session.post(
        f"{self.api_url}/api/v1/assets",
        json={"format": format, "parameters": parameters}
    )

    if response.status_code == 202:
        return response.json()
    elif response.status_code == 409:
        # Duplicate request - return existing asset
        return response.json()
    elif response.status_code == 400:
        raise ValidationError(response.text)
    elif response.status_code == 401:
        raise AuthenticationError("Invalid API key")
    else:
        raise APIError(f"Unexpected status: {response.status_code}")
```

#### Step 3.3: Run Tests and Verify Green

**Claude should:**

- Run test suite: `pytest tests/test_client.py::test_request_asset_success -v`
- Show test output
- Fix any failures
- Confirm all tests pass

#### Step 3.4: Refactor (if needed)

**Claude should:**

- Review code for improvements
- Extract common patterns
- Improve readability
- Re-run tests to ensure they still pass

---

### **Phase 4: Acceptance Criteria Validation**

**Claude should:**

- Go through each acceptance criterion checkbox
- Verify implementation satisfies it
- Show evidence (code snippets, test results)
- Mark each as complete

**Example:**

```
Acceptance Criteria Validation:

✅ [ ] POST to /api/v1/assets with format and parameters
   Evidence: Line 45 in client.py

✅ [ ] Returns dict with asset_id, status, created_at on 202
   Evidence: test_request_asset_success passes

✅ [ ] Handles 409 (duplicate) - returns existing asset
   Evidence: test_request_asset_duplicate passes

✅ [ ] Unit tests cover all response codes
   Evidence: 4 tests covering 202, 409, 400, 401
```

---

### **Phase 5: Definition of Done**

**Claude should go through the DoD checklist:**

#### Code Quality

- [ ] Code reviewed (by Claude, or ask user to review)
- [ ] No linter warnings: `ruff check src/`
- [ ] Type hints present: `mypy src/`
- [ ] Tests passing: `pytest`
- [ ] Code coverage >80%: `pytest --cov=src --cov-report=term`

#### Documentation

- [ ] Docstrings added to all public methods
- [ ] README updated (if needed)
- [ ] Inline comments for complex logic
- [ ] References to TDD sections included

#### Testing

- [ ] Unit tests written and passing
- [ ] Edge cases covered
- [ ] Error scenarios tested
- [ ] Manual testing performed (if applicable)

**Claude should run these commands and report results:**

```bash
# Linting
ruff check src/

# Type checking
mypy src/

# Tests with coverage
pytest --cov=src --cov-report=term-missing

# Show coverage report
```

---

### **Phase 6: Documentation Updates**

#### Step 6.1: Update Docstrings

**Claude should:**

- Ensure all new functions have docstrings
- Follow Google or NumPy docstring format
- Include examples where helpful

**Example:**

```python
def request_asset(self, format: str, parameters: dict) -> dict:
    """Request 3D asset generation from middleware.

    This method initiates an asynchronous asset generation request.
    Use wait_for_completion() to poll for completion.

    Args:
        format: Asset format (e.g., "gltf", "obj")
        parameters: Generation parameters dict

    Returns:
        dict: Contains asset_id, status, created_at

    Raises:
        ValidationError: If format or parameters are invalid
        AuthenticationError: If API key is invalid
        APIError: For other HTTP errors

    Example:
        >>> client = AssetClient(api_url, api_key)
        >>> result = client.request_asset("gltf", {"quality": "high"})
        >>> print(result["asset_id"])
        550e8400-e29b-41d4-a716-446655440000

    See Also:
        - wait_for_completion(): Poll for asset completion
        - get_asset_status(): Check current status
    """
```

#### Step 6.2: Update README (if needed)

**Claude should:**

- Update API reference section
- Add examples if new public method
- Update table of contents

---

### **Phase 7: Commit & PR Preparation**

#### Step 7.1: Review Changes

**Claude should:**

- Show `git status`
- Show `git diff` for review
- Confirm changes are correct

#### Step 7.2: Commit with Conventional Commits

**Claude should use this format:**

```
<type>(<scope>): <subject>

<body>

<footer>
```

**Types:**

- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation only
- `test`: Adding tests
- `refactor`: Code restructuring

**Example:**

```bash
git add src/asset_client/client.py tests/test_client.py
git commit -m "feat(client): implement request_asset() method

- Add request_asset() to initiate asset generation
- Handle 202 (success) and 409 (duplicate) responses
- Add error handling for 400, 401 status codes
- Add comprehensive unit tests with mocked responses
- Test coverage: 95%

Implements: ACME-5
TDD Reference: Section 6.1
"
```

#### Step 7.3: Push Branch

```bash
git push -u origin feature/ACME-5-implement-request-asset
```

#### Step 7.4: Create GitHub PR

**IMPORTANT: Create PR before updating Linear ticket.**

```bash
gh pr create \
  --title "feat(client): implement request_asset() method (ACME-5)" \
  --body "$(cat <<'EOF'
## Description
Implements request_asset() method for initiating asset generation requests.

## Linear Ticket
Closes ACME-5

## Changes
- Added `request_asset()` method to AssetClient
- Implemented error handling for 400, 401, 409 responses
- Added unit tests with mocked HTTP responses
- Updated docstrings and README

## Testing
- ✅ All tests passing (pytest)
- ✅ Code coverage: 95%
- ✅ No linter warnings
- ✅ Type checking passes

## Acceptance Criteria
- [x] POST to /api/v1/assets with format and parameters
- [x] Returns dict with asset_id, status, created_at on 202
- [x] Handles 409 (duplicate) - returns existing asset
- [x] Unit tests cover all response codes

## Definition of Done
- [x] Code reviewed
- [x] Tests passing with >80% coverage
- [x] No linter warnings
- [x] Documentation updated
EOF
)" \
  --base main
```

**PR Title Format:**
- `feat(scope): description (TICKET-ID)`
- `fix(scope): description (TICKET-ID)`
- `docs(scope): description (TICKET-ID)`

#### Step 7.5: Update Linear Ticket & Link PR

**Claude should:**

- Mark ticket as "In Review" (not "Complete" - wait for PR approval)
- Add comment with PR link and implementation details

**Example Linear Comment:**

```
✅ Implementation complete - Ready for review

**PR:** https://github.com/org/repo/pull/123
**Branch:** feature/ACME-5-implement-request-asset
**Commit:** abc123def
**Coverage:** 95%

All acceptance criteria met:
- ✅ request_asset() implemented
- ✅ Error handling complete
- ✅ Unit tests passing (47/47 passing)
- ✅ Documentation updated

Ready for code review.
```

**Linear Integration:**

Linear automatically detects GitHub PR links when:
- PR title or description contains the Linear ticket ID (e.g., "ACME-5")
- PR description includes `Closes ACME-5` or `Fixes ACME-5`
- This creates a bidirectional link (Linear → GitHub, GitHub → Linear)

**After PR is approved and merged:**
- Update Linear ticket to "Done"
- Linear may automatically mark as Done if PR includes `Closes ACME-5`

---

### **Phase 8: Create GitHub PR & Link to Linear**

**Required for visibility and code review workflow.**

Claude will create a GitHub PR and link it to the Linear ticket:

**PR Template:**

```markdown
## Description
Implements request_asset() method for initiating asset generation requests.

## Linear Ticket
Closes ACME-5

## Changes
- Added `request_asset()` method to AssetClient
- Implemented error handling for 400, 401, 409 responses
- Added unit tests with mocked HTTP responses
- Updated docstrings and README

## Testing
- ✅ All tests passing (pytest)
- ✅ Code coverage: 95%
- ✅ No linter warnings
- ✅ Type checking passes

## Acceptance Criteria
- [x] POST to /api/v1/assets with format and parameters
- [x] Returns dict with asset_id, status, created_at on 202
- [x] Handles 409 (duplicate) - returns existing asset
- [x] Unit tests cover all response codes

## Definition of Done
- [x] Code reviewed
- [x] Tests passing with >80% coverage
- [x] No linter warnings
- [x] Documentation updated
```

---

## Best Practices for Claude Code + Linear

### 1. **One Ticket = One Branch = One PR**

- Keep work isolated
- Easier to review
- Can be merged independently

### 2. **Always Start with Tests (TDD)**

- Write failing test first (Red)
- Implement minimal code (Green)
- Refactor (Refactor)
- This matches your TDD document

### 3. **Reference Everything**

- Link to Linear ticket in commits
- Link to TDD sections in code comments
- Link to branch in Linear comments

### 4. **Small, Focused Commits**

- Commit after each logical change
- Makes git history readable
- Easier to review and revert if needed

### 5. **Use Claude Code to Validate**

Before marking ticket complete, ask Claude:

```
Review the implementation for ACME-5 against the acceptance criteria.
Did we miss anything?
```

### 6. **Checkpoint Progress**

For multi-day tickets, commit work-in-progress:

```bash
git add .
git commit -m "wip(client): partial implementation of request_asset

- Added basic HTTP POST logic
- TODO: Error handling
- TODO: Tests

Ref: ACME-5
"
```

---

## Example Conversation Flow

**You:**

```
I want to implement Linear ticket ACME-5. Let's follow the workflow.
```

**Claude:**

```
Let me fetch ticket ACME-5 details...

[Shows ticket details]

I see this ticket requires implementing request_asset() method.
TDD Reference: Section 6.1

Let me create an implementation plan:
1. Write unit tests (TDD approach)
2. Implement method
3. Validate acceptance criteria
4. Update docs

Should I proceed with creating a feature branch?
```

**You:**

```
Yes, proceed
```

**Claude:**

```
✓ Created branch: feature/ACME-5-implement-request-asset
✓ Starting TDD Phase - Writing tests first...

[Writes test file]

I've created test_request_asset_success().
Running tests to verify they fail (Red phase)...

[Shows test failure]

Good! Test fails as expected. Now implementing request_asset()...

[Implements code]

Running tests again...

[Shows test passing]

✅ All tests pass!

Now validating acceptance criteria...
```

---

## Prompts You Can Use

### Starting a ticket

```
Implement Linear ticket ACME-5 following the linear-ticket-workflow
```

### Checking progress

```
What's the status of ACME-5? What acceptance criteria are left?
```

### Validating completion

```
Validate that ACME-5 is complete according to Definition of Done
```

### Creating commit

```
Create a conventional commit for ACME-5 with all changes
```

### Updating Linear

```
Draft a Linear comment for ACME-5 summarizing the implementation
```

---

## Integration with Linear API

You can enhance this workflow by creating a script that:

- Fetches ticket details from Linear API
- Updates ticket status automatically
- Posts comments with implementation progress

**Example script:** `.claude/scripts/linear_helper.py`

This would allow Claude to:

```python
# Fetch ticket
ticket = linear.get_ticket("ACME-5")

# Update status
linear.update_status("ACME-5", "In Progress")

# Add comment
linear.add_comment("ACME-5", "Implementation started on branch feature/ACME-5...")
```

---

## Summary Checklist

For every Linear ticket, Claude should:

1. **Analyze** 📋
   - [ ] Fetch ticket details
   - [ ] Read TDD references
   - [ ] Create implementation plan

2. **Setup** 🔧
   - [ ] Create feature branch
   - [ ] Verify clean baseline

3. **TDD** 🧪
   - [ ] Write failing tests (Red)
   - [ ] Implement code (Green)
   - [ ] Refactor
   - [ ] Validate tests pass

4. **Validate** ✅
   - [ ] Check acceptance criteria
   - [ ] Run Definition of Done checks
   - [ ] Verify coverage >80%

5. **Document** 📝
   - [ ] Add docstrings
   - [ ] Update README
   - [ ] Add code comments

6. **Commit & PR** 💾
   - [ ] Review changes
   - [ ] Conventional commit
   - [ ] Push branch
   - [ ] Create GitHub PR (include Linear ticket ID)
   - [ ] Update Linear ticket to "In Review" (with PR link)

---

## Notes

- This workflow is **optimized for solo development** with Claude Code
- For team environments, add code review steps
- Adapt the workflow as needed for your project
- Keep the TDD document as source of truth for technical specs

---

**Version:** 1.0
**Last Updated:** 2025-10-20
**Owner:** Mark
