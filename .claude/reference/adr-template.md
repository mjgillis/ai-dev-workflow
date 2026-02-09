# ADR-[NUMBER]: [Short Title of Decision]

**Status:** [Proposed | Accepted | Deprecated | Superseded]

**Date:** [YYYY-MM-DD]

**Deciders:** [List of people involved in the decision]

**Technical Story:** [Link to Linear ticket, PRD, or TDD section]

---

## Context and Problem Statement

[Describe the context and problem statement in 2-3 sentences. What decision needs to be made? What are we trying to solve?]

**Example:**
> We need to choose a database for storing API usage metrics. The system must handle 1M requests/day with <200ms query latency and retain 90 days of data. Current PostgreSQL setup is not optimized for time-series data.

---

## Decision Drivers

What factors influenced this decision?

- [ ] **Performance requirement:** [Specific requirement, e.g., "<200ms p95 latency"]
- [ ] **Scalability requirement:** [e.g., "Handle 10K concurrent users"]
- [ ] **Cost constraint:** [e.g., "Stay under $500/month"]
- [ ] **Team expertise:** [e.g., "Team knows Python, not Go"]
- [ ] **Time constraint:** [e.g., "Must launch in 4 weeks"]
- [ ] **Existing infrastructure:** [e.g., "Already using AWS"]
- [ ] **Other:** [Describe]

---

## Considered Options

### Option 1: [Option Title]

**Description:** [Brief description of this option]

**Pros:**
- ✅ [Advantage 1]
- ✅ [Advantage 2]
- ✅ [Advantage 3]

**Cons:**
- ❌ [Disadvantage 1]
- ❌ [Disadvantage 2]
- ❌ [Disadvantage 3]

**Cost:** [Estimated cost - time, money, complexity]

**Example:**
```
Option 1: Stick with PostgreSQL

Pros:
- ✅ Team already knows PostgreSQL
- ✅ No migration needed
- ✅ Mature ecosystem

Cons:
- ❌ Not optimized for time-series queries
- ❌ Partitioning is manual and complex
- ❌ Slower than specialized time-series DBs

Cost: No immediate cost, but ongoing performance issues
```

---

### Option 2: [Option Title]

**Description:** [Brief description of this option]

**Pros:**
- ✅ [Advantage 1]
- ✅ [Advantage 2]
- ✅ [Advantage 3]

**Cons:**
- ❌ [Disadvantage 1]
- ❌ [Disadvantage 2]
- ❌ [Disadvantage 3]

**Cost:** [Estimated cost - time, money, complexity]

**Example:**
```
Option 2: TimescaleDB (PostgreSQL extension)

Pros:
- ✅ Optimized for time-series data
- ✅ Automatic partitioning
- ✅ Still uses SQL (familiar)
- ✅ Can coexist with regular Postgres tables

Cons:
- ❌ Learning curve for time-series features
- ❌ Extension setup required
- ❌ Slightly higher hosting cost

Cost: 2 days migration + $50/month additional hosting
```

---

### Option 3: [Option Title]

**Description:** [Brief description of this option]

**Pros:**
- ✅ [Advantage 1]
- ✅ [Advantage 2]

**Cons:**
- ❌ [Disadvantage 1]
- ❌ [Disadvantage 2]

**Cost:** [Estimated cost]

**Example:**
```
Option 3: InfluxDB (dedicated time-series DB)

Pros:
- ✅ Built specifically for time-series
- ✅ Best query performance
- ✅ Built-in retention policies

Cons:
- ❌ Different query language (InfluxQL, not SQL)
- ❌ Team has no experience
- ❌ Can't join with relational data easily
- ❌ Another database to manage

Cost: 1 week to learn + migration, $100/month hosting
```

---

## Decision Outcome

**Chosen option:** "[Option Title]" because [rationale in 1-2 sentences]

**Example:**
> Chosen option: "TimescaleDB" because it provides time-series optimization while keeping SQL familiarity, and can coexist with existing PostgreSQL data. The 2-day migration cost is acceptable given the long-term performance benefits.

---

## Consequences

### Positive Consequences

- ✅ [Good consequence 1]
- ✅ [Good consequence 2]
- ✅ [Good consequence 3]

**Example:**
- ✅ Query latency reduced from 800ms to 150ms (p95)
- ✅ Automatic partitioning saves 5 hours/month of manual work
- ✅ Can retain 90 days of data without performance degradation

### Negative Consequences

- ❌ [Bad consequence or trade-off 1]
- ❌ [Bad consequence or trade-off 2]

**Example:**
- ❌ Team needs to learn TimescaleDB-specific functions (1-2 days)
- ❌ Hosting cost increases by $50/month

### Neutral Consequences

- ℹ️ [Neutral consequence or observation 1]

**Example:**
- ℹ️ Migration requires 2 days of downtime for staging environment

---

## Validation

How will we know if this decision was correct?

**Success Criteria:**

- [ ] [Measurable criterion 1]
- [ ] [Measurable criterion 2]
- [ ] [Measurable criterion 3]

**Timeline:** [When to evaluate]

**Example:**
```
Success Criteria:
- [ ] Query latency <200ms (p95) - measure after 1 week
- [ ] No query timeouts - monitor for 1 month
- [ ] Team comfortable with TimescaleDB - survey after 1 month
- [ ] Data retention of 90 days without performance issues - verify after 3 months

Timeline: Re-evaluate after 3 months (April 15, 2025)
```

---

## Implementation Plan

**Steps to implement this decision:**

1. [Step 1]
2. [Step 2]
3. [Step 3]

**Estimated effort:** [Time estimate]

**Owner:** [Person responsible]

**Example:**
```
1. Set up TimescaleDB in staging environment
2. Migrate schema and sample data
3. Update application to use TimescaleDB-specific functions
4. Performance test with production-like load
5. Plan production migration (low-traffic window)
6. Execute production migration
7. Monitor for 1 week

Estimated effort: 2 days
Owner: Backend team
Deadline: Jan 20, 2025
```

---

## References

- [Link to PRD section]
- [Link to TDD section]
- [Link to benchmark results]
- [Link to vendor documentation]
- [Link to related ADRs]

**Example:**
```
- TDD v2.1 Section 3.1 (Data Model Design)
- TimescaleDB vs InfluxDB benchmark: [link]
- TimescaleDB docs: https://docs.timescale.com
- Supersedes: ADR-003 (Original PostgreSQL decision)
```

---

## Notes

[Optional section for additional context, meeting notes, or discussion highlights]

**Example:**
```
Discussion notes from Jan 5 architecture meeting:
- Considered MongoDB but rejected due to lack of ACID guarantees
- DynamoDB too expensive for our data volume
- Team consensus: SQL familiarity is important, rules out InfluxDB
```

---

## Changelog

| Date | Change | Author |
|------|--------|--------|
| YYYY-MM-DD | Initial decision | [Name] |
| YYYY-MM-DD | Updated based on [feedback/results] | [Name] |

**Example:**
```
| Date | Change | Author |
|------|--------|--------|
| 2025-01-10 | Initial decision: TimescaleDB | Mark |
| 2025-02-15 | Validation results: All success criteria met | Mark |
| 2025-06-01 | Deprecated: Moving to Clickhouse (see ADR-042) | Sarah |
```

---

## Template Usage Guide

### When to Create an ADR

Create an ADR for decisions that:
- Are **significant** (affect architecture, not just implementation details)
- Are **hard to reverse** (migration, vendor lock-in)
- Have **multiple valid options** (trade-offs involved)
- Need to be **explained to future team members**

**Examples of ADR-worthy decisions:**
- Database choice
- Cloud provider selection
- Framework/language choice
- Authentication method
- API design patterns
- Microservices vs monolith

**NOT ADR-worthy:**
- Code formatting style (use linter config instead)
- Variable naming (use style guide)
- Which library for a single use case (document in code comments)

### Numbering Convention

**Format:** `ADR-XXX` (zero-padded, e.g., ADR-001, ADR-042)

**Sequence:** Sequential numbering within project
- ADR-001: First decision
- ADR-002: Second decision
- etc.

### Status Lifecycle

- **Proposed:** Decision is being considered but not yet made
- **Accepted:** Decision has been made and is active
- **Deprecated:** Decision is no longer recommended but may still be in use
- **Superseded:** Decision has been replaced by a new ADR (reference the new ADR)

**Example:**
```
ADR-003: Use PostgreSQL for all data storage
Status: Superseded by ADR-015 (TimescaleDB for time-series data)
```

### Storage Location

Store ADRs in your project:
- `/docs/adr/ADR-001-use-timescaledb.md`
- `/docs/adr/ADR-002-authentication-with-oauth.md`

Or in a dedicated repo for multi-project decisions.

### Integration with Workflows

**Reference ADRs in:**
- TDD documents (Section 2.3: Technology Choices)
- Linear tickets (link to ADR for context)
- Code comments (for decisions affecting specific code)

**Example in TDD:**
```markdown
## Technology Decisions

### Database: TimescaleDB
- Why: See ADR-015
- Alternatives: PostgreSQL (ADR-003), InfluxDB (rejected)
- Tradeoffs: See ADR-015 for detailed analysis
```

---

**Version:** 1.0
**Last Updated:** 2025-11-06
**Based on:** [Michael Nygard's ADR template](https://github.com/joelparkerhenderson/architecture-decision-record)
