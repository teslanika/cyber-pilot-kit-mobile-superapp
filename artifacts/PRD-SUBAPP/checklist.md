# PRD-SUBAPP Checklist

**Artifact**: PRD-SUBAPP  
**Kit**: mobile-superapp  
**Level**: L1 (SubApp)

This checklist provides semantic quality criteria for SubApp-level Product Requirements Documents in mobile SuperApp projects.

---

## Table of Contents

1. [MUST HAVE Requirements](#must-have-requirements)
2. [SHOULD HAVE Requirements](#should-have-requirements)
3. [MUST NOT HAVE (Violations)](#must-not-have-violations)
4. [Mobile-Specific Criteria](#mobile-specific-criteria)
5. [Reporting](#reporting)

---

## MUST HAVE Requirements

### PRD-SUBAPP-001: Overview Completeness

**Priority**: CRITICAL

The SubApp PRD MUST include:

- [ ] Clear purpose statement (1-2 paragraphs)
- [ ] Link to parent Platform PRD
- [ ] Version and status metadata
- [ ] In-scope capabilities list
- [ ] Out-of-scope exclusions list

**Why it matters**: Without clear scope definition, development will drift and stakeholders will have misaligned expectations.

### PRD-SUBAPP-002: Platform Traceability

**Priority**: CRITICAL

The PRD MUST include traces to Platform PRD:

- [ ] Table mapping SubApp to Platform requirements
- [ ] Relation type for each trace (refines, inherits, extends)
- [ ] `cpt-superapp-fr-{slug}` references for refined FRs
- [ ] `cpt-superapp-nfr-{slug}` references for inherited NFRs

**Why it matters**: SubApp requirements must demonstrate they contribute to Platform-level goals.

### PRD-SUBAPP-003: Actor Definition

**Priority**: HIGH

The PRD MUST define actors:

- [ ] Primary actors table with SubApp-specific context
- [ ] Actor IDs following `cpt-superapp-actor-{slug}` pattern
- [ ] Description of how each actor uses this SubApp

**Why it matters**: Actor definitions ensure requirements are user-centered and traceable.

### PRD-SUBAPP-004: Functional Requirements Structure

**Priority**: CRITICAL

Each Functional Requirement MUST include:

- [ ] Unique ID following `cpt-{subapp}-fr-{slug}` pattern
- [ ] Traces To field (parent Platform FR or "SubApp-specific")
- [ ] Priority (P1, P2, P3)
- [ ] Actor reference
- [ ] Description (what the system must do)
- [ ] Acceptance criteria (measurable)

**Why it matters**: Well-structured FRs enable traceability, prioritization, and validation.

### PRD-SUBAPP-005: Non-Functional Requirements

**Priority**: HIGH

Each NFR MUST include:

- [ ] Unique ID following `cpt-{subapp}-nfr-{slug}` pattern
- [ ] Traces To field (parent Platform NFR)
- [ ] Category (Performance, Security, Usability, etc.)
- [ ] Measurable metric
- [ ] Target value
- [ ] Rationale for SubApp-specific value

**Why it matters**: NFRs ensure quality attributes are explicitly defined and measurable.

### PRD-SUBAPP-006: Use Cases

**Priority**: HIGH

The PRD MUST include use cases:

- [ ] Unique ID following `cpt-{subapp}-usecase-{slug}` pattern
- [ ] Traces To field (which FR it implements)
- [ ] Primary actor reference
- [ ] Preconditions
- [ ] Main flow (numbered steps)
- [ ] Postconditions
- [ ] Exception handling

**Why it matters**: Use cases bridge requirements to implementation by describing user journeys.

### PRD-SUBAPP-007: Dependencies

**Priority**: HIGH

The PRD MUST document dependencies:

- [ ] Platform dependencies table (Kernel services)
- [ ] External dependencies table (Backend, APIs)
- [ ] Dependency types (Required, Optional)
- [ ] Integration descriptions

**Why it matters**: Dependencies define integration scope and external team coordination.

### PRD-SUBAPP-008: Traceability Matrix

**Priority**: CRITICAL

The PRD MUST include traceability matrices:

- [ ] Platform FR → SubApp FR coverage table
- [ ] Coverage status (Full, Partial, Not in scope)
- [ ] SubApp FR → Epic coverage table
- [ ] Status for each mapping

**Why it matters**: Traceability ensures complete coverage and enables change impact analysis.

---

## SHOULD HAVE Requirements

### PRD-SUBAPP-009: SubApp-Specific Tags

**Priority**: MEDIUM

Requirements that don't trace to Platform SHOULD:

- [ ] Have `subapp-specific` tag
- [ ] Include rationale for why it's SubApp-level only
- [ ] Not duplicate Platform-level requirements

### PRD-SUBAPP-010: Acceptance Criteria Checklist

**Priority**: MEDIUM

The PRD SHOULD include summary acceptance criteria:

- [ ] All Platform FRs in scope are refined
- [ ] All SubApp FRs have epic-level detailing
- [ ] All use cases have corresponding features
- [ ] Traceability matrix complete

### PRD-SUBAPP-011: ID Reference Appendix

**Priority**: LOW

The PRD SHOULD include ID pattern reference:

- [ ] ID patterns documented (PRD, FR, NFR, UseCase)
- [ ] Examples for each pattern
- [ ] Purpose of each ID type

---

## MUST NOT HAVE (Violations)

### PRD-SUBAPP-NO-001: No Technical Implementation

**Priority**: HIGH

The PRD MUST NOT contain:

- [ ] Architecture decisions (belongs in DESIGN)
- [ ] Module structures (belongs in DESIGN)
- [ ] Code examples (belongs in DESIGN/FEATURE)
- [ ] API contracts (belongs in DESIGN)

**Why it matters**: PRD defines WHAT, not HOW.

### PRD-SUBAPP-NO-002: No Platform Duplication

**Priority**: HIGH

The PRD MUST NOT:

- [ ] Redefine Platform-level requirements (only refine)
- [ ] Duplicate actor definitions (reference Platform actors)
- [ ] Repeat Platform constraints verbatim

**Why it matters**: Duplication creates inconsistency and maintenance burden.

### PRD-SUBAPP-NO-003: No Untraceable Requirements

**Priority**: CRITICAL

The PRD MUST NOT contain requirements without:

- [ ] Unique ID
- [ ] Clear traceability (to Platform or marked as SubApp-specific)
- [ ] Priority assignment

**Why it matters**: Untraceable requirements cannot be validated or prioritized.

### PRD-SUBAPP-NO-004: No Vague Acceptance Criteria

**Priority**: HIGH

The PRD MUST NOT contain:

- [ ] Acceptance criteria without measurable outcomes
- [ ] Subjective terms ("fast", "good", "user-friendly") without metrics
- [ ] Incomplete criteria (missing success/failure conditions)

**Why it matters**: Vague criteria cannot be tested or verified.

---

## Mobile-Specific Criteria

### MOBILE-PRD-001: Offline Requirements

**Priority**: HIGH

SubApp PRD MUST address offline behavior:

- [ ] Core offline capabilities defined
- [ ] Data sync requirements specified
- [ ] Offline limitations documented

### MOBILE-PRD-002: Cross-Platform Parity

**Priority**: HIGH

SubApp PRD MUST specify platform parity:

- [ ] iOS-specific requirements (if any)
- [ ] Android-specific requirements (if any)
- [ ] Shared requirements clearly marked
- [ ] Platform differences documented

### MOBILE-PRD-003: Deep Link Requirements

**Priority**: MEDIUM

SubApp PRD SHOULD include:

- [ ] Deep link entry points
- [ ] Deep link parameters
- [ ] Deep link handling requirements

### MOBILE-PRD-004: Push Notification Requirements

**Priority**: MEDIUM

If SubApp uses notifications:

- [ ] Notification types defined
- [ ] Notification triggers documented
- [ ] User preference requirements

---

## Reporting

### Report Format

For each issue found, report:

```markdown
## Issue: {CHECKLIST-ID}

**Severity**: CRITICAL | HIGH | MEDIUM | LOW

**Why Applicable**: {Why this requirement applies to this SubApp}

**Issue**: {What is wrong}

**Evidence**: {Quote from document or "Not found"}

**Impact**: {Why this matters}

**Proposal**: {How to fix}
```

### Reporting Commitment

- [ ] I reported all issues I found
- [ ] I used the exact report format
- [ ] I included evidence for each issue
- [ ] I proposed concrete fixes
- [ ] I did not hide or omit known problems
