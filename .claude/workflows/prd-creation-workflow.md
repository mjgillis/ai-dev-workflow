# PRD Creation Workflow

**Purpose:** A structured process for creating comprehensive Product Requirements Documents with Claude.

---

## Overview

This workflow ensures every PRD includes:

-  Clear problem statement and user needs
-  Well-defined goals and success metrics
-  Detailed user stories with acceptance criteria
-  Functional and non-functional requirements
-  Scope boundaries and timeline
-  Risk assessment and dependencies

---

## Quick Start

When starting a new PRD, say:

> "I want to create a PRD for [feature/product]. Let's follow the prd-creation-workflow."

Or:

> "Help me create a PRD for a user authentication system"

---

## The Workflow

### **Phase 1: Discovery & Problem Definition**

#### Step 1.1: Identify the Problem

**Claude will ask:**

- What problem are you trying to solve?
- Who experiences this problem?
- How do they experience it currently?
- What's the impact of this problem?

**You should provide:**

- Description of the pain point
- Affected user personas
- Current workarounds (if any)
- Business impact or user feedback

**Example:**

```
Problem: Users can't easily track their API usage across multiple projects.
Who: Developers managing multiple API integrations
Current state: Manual log parsing and spreadsheet tracking
Impact: Wasted time (avg 2 hours/week per developer), billing errors
```

#### Step 1.2: Define "Why Now?"

**Claude will ask:**

- Why is this important to solve now?
- What's changed that makes this a priority?
- What happens if we don't solve this?

**Consider:**

- Market conditions
- Competitive pressure
- User demand/feedback volume
- Strategic priorities
- Technical dependencies

**Example:**

```
Why now:
- Received 47 support requests in past month
- Competitor just launched similar feature
- Blocks enterprise sales (3 deals on hold)
- New API pricing model requires usage visibility
```

---

### **Phase 2: User Research & Validation**

#### Step 2.1: Define User Personas

**Claude will help you document:**

For each persona:

- **Name/Role:** [e.g., "Sarah - Frontend Developer"]
- **Goals:** What they're trying to accomplish
- **Pain Points:** Current frustrations
- **Needs:** What would help them succeed

**Example:**

```
Persona 1: Sarah - Frontend Developer
- Goals: Build features quickly, stay within API budget
- Pain Points: No visibility into API usage until bill arrives
- Needs: Real-time usage dashboard, alerts before limits

Persona 2: Mike - Engineering Manager
- Goals: Optimize costs, prevent service disruptions
- Pain Points: Can't allocate usage by project/team
- Needs: Usage breakdown by project, trend analysis
```

#### Step 2.2: Validate the Problem

**Claude will ask:**

- Have you talked to users about this?
- What did they say?
- How many users requested this?
- What would they pay for this solution?

**Document:**

- User interview findings
- Support ticket trends
- Survey results
- Usage analytics

---

### **Phase 3: Goals & Success Metrics**

#### Step 3.1: Define Primary Goal

**Claude will help you articulate:**

```
Primary Goal: [One clear sentence]

Example: Enable developers to monitor and optimize their API usage in real-time.
```

#### Step 3.2: Define Success Metrics

**Claude will guide you through:**

**Leading Indicators** (early signals):

- Feature adoption rate
- Time to first value
- User engagement (DAU/WAU)

**Lagging Indicators** (outcome measures):

- Customer satisfaction (NPS, CSAT)
- Business impact (revenue, retention)
- Efficiency gains (time saved, costs reduced)

**Example:**

```
Success Metrics:

Leading:
- 70% of active users view usage dashboard within first week
- Average 3 dashboards created per user
- 50% of users set up usage alerts

Lagging:
- 25% reduction in support tickets about billing
- 15% increase in API usage (due to confidence)
- NPS increase from 7.2 to 8.0
- $50K additional revenue from enterprise tier (usage analytics feature)

Target Timeline: 3 months post-launch
```

---

### **Phase 4: Requirements Gathering**

#### Step 4.1: Write User Stories

**Claude will help you write stories in this format:**

```
As a [user type]
I want [capability]
So that [benefit]
```

**For each story, define:**

- **Acceptance Criteria** (Given/When/Then format)
- **Priority** (Must Have / Should Have / Nice to Have)

**Example:**

```
Story 1: View Real-Time Usage Dashboard

As a developer
I want to see my current API usage in a dashboard
So that I can monitor usage and avoid unexpected charges

Acceptance Criteria:
- [ ] Dashboard shows requests/minute, requests/day, requests/month
- [ ] Dashboard updates in real-time (< 30 second delay)
- [ ] Dashboard displays usage by project (if multiple projects)
- [ ] Dashboard shows percentage of quota used
- [ ] Dashboard accessible via web UI and mobile

Priority: Must Have
```

#### Step 4.2: Define Functional Requirements

**Claude will ask about:**

- **Core Features:** What must the product do?
- **User Workflows:** How will users interact with it?
- **Data Requirements:** What data is needed?
- **Integrations:** What systems must it connect to?

**Template:**

```
1. Feature: Real-Time Usage Dashboard
   - Description: Display API usage metrics with <30s latency
   - Priority: Must Have
   - User Story Reference: Story 1
   - Acceptance Criteria:
     - [ ] Shows requests/min, requests/day, requests/month
     - [ ] Updates every 30 seconds
     - [ ] Filterable by date range, project, endpoint
```

#### Step 4.3: Define Non-Functional Requirements

**Claude will prompt for:**

- **Performance:** Response times, throughput, latency
- **Security:** Authentication, authorization, data protection
- **Scalability:** User capacity, data volume, growth handling
- **Usability:** Accessibility, browser support, mobile experience
- **Reliability:** Uptime, error rates, recovery time

**Example:**

```
Non-Functional Requirements:

Performance:
- Dashboard loads in <2 seconds
- API usage data updates every 30 seconds
- Support 10K concurrent dashboard viewers

Security:
- Dashboard requires authentication (OAuth 2.0)
- Usage data encrypted at rest (AES-256)
- API keys never displayed in full (show last 4 chars only)

Scalability:
- Support 100K users
- Store 90 days of usage history per user
- Handle 1M API calls/day tracked

Usability:
- WCAG 2.1 AA compliant
- Mobile responsive
- Support Chrome, Firefox, Safari (latest 2 versions)

Reliability:
- 99.9% uptime SLA
- <1% error rate
- Recovery time <5 minutes
```

---

### **Phase 5: Scope & Timeline Planning**

#### Step 5.1: Define What's In Scope

**Claude will help you list:**

- Features included in this release
- User stories being implemented
- Requirements being addressed

**Example:**

```
In Scope (v1.0):
- Real-time usage dashboard (web only)
- Basic usage alerts (email notifications)
- Usage history (30 days)
- Project-level breakdown
- CSV export
```

#### Step 5.2: Define What's Out of Scope

**Claude will help you clarify:**

- Features explicitly NOT included
- Deferred to future releases
- Related but separate work

**Example:**

```
Out of Scope (for v1.0):
- Mobile app (deferred to v2.0)
- Custom report builder (future consideration)
- Cost optimization recommendations (separate project)
- Third-party integrations (Slack, PagerDuty) - v1.1

Why: Focus on core monitoring experience first, gather user feedback, then expand.
```

#### Step 5.3: Identify Dependencies

**Claude will ask:**

- What needs to exist before you can build this?
- What teams/systems must you coordinate with?
- What external factors affect timeline?

**Document:**

```
Dependencies:

Technical:
- [ ] Usage tracking infrastructure (Data team - ETA: Jan 15)
- [ ] Authentication service supports OAuth 2.0 (Auth team - Done)
- [ ] Metrics API endpoint exists (Platform team - ETA: Jan 20)

Team:
- [ ] Design resources for dashboard UI (Design team - 2 weeks)
- [ ] Legal review of data retention policy (Legal - 1 week)

External:
- [ ] Cloud provider supports real-time metrics streaming (Confirmed)
```

#### Step 5.4: Define Timeline & Phases

**Claude will help you create:**

| Phase | Deliverable | Date |
|-------|-------------|------|
| Discovery | PRD Approved | Week of Jan 15 |
| Design | TDD Complete, Designs Ready | Week of Jan 29 |
| Development | Alpha (internal testing) | Week of Feb 19 |
| Testing | Beta (select users) | Week of Mar 4 |
| Launch | General Availability | Week of Mar 18 |

**Claude will ask:**

- What's your target launch date?
- Are there any hard deadlines?
- What milestones are critical?

---

### **Phase 6: Risk Assessment**

**Claude will guide you through:**

#### Identify Risks

For each risk, document:

- **Description:** What could go wrong?
- **Impact:** How bad would it be? (High/Medium/Low)
- **Likelihood:** How likely? (High/Medium/Low)
- **Mitigation:** How will you address it?

**Example:**

```
| Risk | Impact | Likelihood | Mitigation |
|------|--------|------------|------------|
| Metrics API doesn't meet latency requirements | High | Medium | Build cache layer, test early, have fallback to 5-min intervals |
| User adoption is low (<30%) | High | Low | User research upfront, beta program, in-app education |
| Data retention costs higher than expected | Medium | Medium | Implement data archival after 30 days, monitor costs weekly |
| Security vulnerability in dashboard | High | Low | Security review before launch, penetration testing, bug bounty |
```

---

### **Phase 7: Review & Iteration**

#### Step 7.1: Review Completeness

**Claude will check:**

- [ ] Problem clearly stated
- [ ] User personas defined
- [ ] Goals and success metrics specified
- [ ] User stories with acceptance criteria
- [ ] Functional requirements documented
- [ ] Non-functional requirements specified
- [ ] Scope boundaries clear (in/out of scope)
- [ ] Dependencies identified
- [ ] Timeline defined
- [ ] Risks assessed

#### Step 7.2: Ask Clarifying Questions

**Claude will identify gaps:**

- Missing user stories
- Unclear acceptance criteria
- Unmeasured success metrics
- Undefined edge cases
- Unidentified dependencies

**Claude will ask questions like:**

```
Questions for clarification:

1. What happens if a user exceeds their quota?
   - Should the dashboard show a warning?
   - Should we block requests or just alert?

2. How should usage be calculated for shared projects?
   - Per user or per project?
   - How to handle team accounts?

3. What's the data retention policy?
   - 30 days mentioned, but is that legally sufficient?
   - Any compliance requirements (GDPR, SOC 2)?
```

#### Step 7.3: Refine and Finalize

**Claude will help you:**

- Answer open questions
- Add missing details
- Clarify ambiguities
- Validate priorities
- Confirm scope

**Final check:**

```
Is this PRD ready for technical design?

 Problem is clear and validated
 Goals are measurable
 Requirements are specific
 Scope is well-defined
 Risks are identified
 Timeline is realistic
 Stakeholders can approve

Ready to proceed to TDD creation!
```

---

## PRD Template

**Claude will use this template:** See [reference/prd-template-1pager.md](../reference/prd-template-1pager.md)

---

## Best Practices

### 1. Start with "Why"

Always begin with the problem, not the solution. Understand the user pain before jumping to features.

### 2. Make Success Measurable

Every goal should have a metric. Avoid vague goals like "improve user experience" without defining how to measure improvement.

### 3. Use Acceptance Criteria, Not Implementation Details

Good: "User can filter dashboard by date range"
Bad: "Add a React date picker component to the dashboard"

The PRD defines *what*, not *how*.

### 4. Keep Scope Realistic

Better to ship a small, complete feature than a large, incomplete one. Use "Out of Scope" liberally.

### 5. Validate with Users

Before finalizing, show the PRD to actual users or stakeholders. Ask:

- Does this solve your problem?
- Is anything missing?
- What's most important to you?

### 6. Update as You Learn

PRDs are living documents. As you learn during design and development, update the PRD. Track changes in the Changelog section.

---

## Example Conversation Flow

**You:**

```
I want to create a PRD for an API usage dashboard. Let's follow the workflow.
```

**Claude:**

```
I'll help you create a comprehensive PRD for an API usage dashboard.

Let's start with Phase 1: Discovery & Problem Definition.

**Question 1:** What problem are you trying to solve?
- What pain point do users currently experience?
- How are they handling API usage tracking today?

**Question 2:** Who experiences this problem?
- What user roles or personas are affected?
- How many users does this impact?

**Question 3:** Why is this important to solve now?
- What's changed that makes this a priority?
- What happens if you don't build this?
```

**You:**

```
Developers can't see their API usage in real-time. They only find out when they
get the bill at the end of the month, which leads to unexpected charges.

About 500 active API users, mostly developers and engineering managers.

We're seeing 10-15 support tickets per week about billing surprises, and it's
blocking 3 enterprise deals who require usage visibility before signing.
```

**Claude:**

```
Got it! Let me document that:

**Problem Statement:**
Developers have no real-time visibility into API usage, leading to unexpected
billing charges and support burden.

**Affected Users:**
- Developers (individual contributors)
- Engineering Managers (team leads)
- ~500 active API users

**Current State:**
- Usage only visible in monthly bill
- 10-15 support tickets/week about billing surprises
- Blocking 3 enterprise deals

**Why Now:**
- High support burden
- Enterprise sales blocker
- User frustration impacting satisfaction

Now let's move to Phase 2: User Research & Validation.

Can you describe 2-3 user personas in more detail?
For each, I'd like to know:
- Their role/title
- What they're trying to accomplish
- Their current pain points
- What would make them successful
```

---

## Prompts You Can Use

### Starting PRD creation

```
Create a PRD for [feature/product] using the prd-creation-workflow
```

### Checking completeness

```
Review this PRD for completeness. What's missing?
```

### Refining requirements

```
Help me refine the user stories for [feature]
```

### Validating metrics

```
Are these success metrics measurable and realistic?
```

### Defining scope

```
Help me decide what should be in scope vs out of scope for v1.0
```

---

## Integration with TDD Workflow

Once the PRD is complete and approved:

```
This PRD looks complete. Ready to create the Technical Design Document?
Let's follow the tdd-creation-workflow next.
```

The TDD will reference the PRD and translate requirements into technical specifications.

---

## Common Pitfalls to Avoid

### 1. Solutionizing Too Early

L **Don't:** "Build a React dashboard with Chart.js"
 **Do:** "Display API usage metrics in a visual format"

The PRD should focus on *what* users need, not *how* to build it.

### 2. Vague Success Metrics

L **Don't:** "Improve user satisfaction"
 **Do:** "Increase NPS from 7.2 to 8.0 within 3 months"

### 3. Missing Acceptance Criteria

L **Don't:** "User can see usage"
 **Do:**
- [ ] User sees requests/minute, requests/day, requests/month
- [ ] Data updates every 30 seconds
- [ ] Data is filterable by project and date range

### 4. Undefined Edge Cases

Always ask:

- What happens when there's no data?
- What happens at scale (1M users, 1B requests)?
- What happens when dependencies fail?

### 5. Ignoring Non-Functional Requirements

Don't forget:

- Performance (how fast?)
- Security (how protected?)
- Scalability (how many users?)
- Accessibility (who can use it?)

---

## Checklist

Before marking PRD as complete:

- [ ] Problem clearly stated
- [ ] User personas documented
- [ ] Primary goal defined
- [ ] Success metrics are measurable
- [ ] User stories have acceptance criteria
- [ ] Functional requirements listed
- [ ] Non-functional requirements specified
- [ ] Scope boundaries clear (in/out)
- [ ] Dependencies identified
- [ ] Timeline defined
- [ ] Risks assessed with mitigation
- [ ] Open questions resolved
- [ ] Stakeholders have reviewed

---

**Version:** 1.0
**Last Updated:** 2025-11-05
