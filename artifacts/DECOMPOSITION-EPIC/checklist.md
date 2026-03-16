# DECOMPOSITION-EPIC Checklist

**Artifact**: DECOMPOSITION-EPIC  
**Kit**: mobile-superapp  
**Level**: L2 (Epic)

This checklist provides semantic quality criteria for Epic-level Decomposition documents in mobile SuperApp projects.

---

## Table of Contents

1. [MUST HAVE Requirements](#must-have-requirements)
2. [SHOULD HAVE Requirements](#should-have-requirements)
3. [MUST NOT HAVE (Violations)](#must-not-have-violations)
4. [Mobile-Specific Criteria](#mobile-specific-criteria)
5. [Reporting](#reporting)

---

## MUST HAVE Requirements

### DECOMP-EPIC-001: Overview Section

**Priority**: CRITICAL

The DECOMPOSITION MUST include:

- [ ] Clear purpose statement
- [ ] Link to Epic PRD
- [ ] Link to Epic DESIGN
- [ ] Link to SubApp DECOMPOSITION
- [ ] Overall implementation status marker with ID `cpt-{subapp}-{epic}-status-overall`

**Why it matters**: Overview establishes context for Feature decomposition.

### DECOMP-EPIC-002: Feature Entries Structure

**Priority**: CRITICAL

Each Feature entry MUST include:

- [ ] Feature ID following `cpt-{subapp}-feature-{feature}` pattern
- [ ] Link to Feature folder
- [ ] Priority (HIGH, MEDIUM, LOW)
- [ ] Purpose description
- [ ] Depends On (other Features or "None")
- [ ] Scope (in-scope list)
- [ ] Out of scope (explicit exclusions)

**Why it matters**: Complete entries enable independent Feature development.

### DECOMP-EPIC-003: Requirements Coverage

**Priority**: CRITICAL

Each Feature entry MUST document:

- [ ] Requirements covered list
- [ ] `cpt-{subapp}-epic-{epic}-fr-{slug}` references
- [ ] Priority marker for each requirement
- [ ] Checkbox for implementation status

**Why it matters**: Coverage ensures all Epic FRs are allocated to Features.

### DECOMP-EPIC-004: Design Components

**Priority**: HIGH

Each Feature entry MUST list:

- [ ] Design components from Epic DESIGN
- [ ] `cpt-{subapp}-{epic}-component-{slug}` references
- [ ] Screen/widget references
- [ ] Use case references
- [ ] Priority marker for each

**Why it matters**: Components trace DESIGN elements to Features.

### DECOMP-EPIC-005: Screen/Widget References

**Priority**: HIGH

Each Feature entry MUST include:

- [ ] Screen reference `cpt-{subapp}-{epic}-screen-{slug}`
- [ ] Widget references `cpt-{subapp}-{epic}-widget-{slug}`
- [ ] Checkboxes for implementation status

**Why it matters**: Screen/widget mapping guides UI implementation.

### DECOMP-EPIC-006: Use Case References

**Priority**: HIGH

Each Feature entry SHOULD include:

- [ ] Use case reference `cpt-{subapp}-{epic}-usecase-{slug}`
- [ ] Checkbox for implementation status

**Why it matters**: Use cases map to Feature business logic.

### DECOMP-EPIC-007: Platform Implementation

**Priority**: CRITICAL

Each Feature entry MUST include:

- [ ] Platform implementation table
- [ ] KMP module and location
- [ ] Android component and location
- [ ] iOS component and location

**Why it matters**: Platform locations guide code implementation.

### DECOMP-EPIC-008: API Endpoints

**Priority**: HIGH

Each Feature entry SHOULD include:

- [ ] API endpoints used
- [ ] HTTP methods (GET, POST, etc.)
- [ ] Endpoint paths

**Why it matters**: API mapping enables backend coordination.

### DECOMP-EPIC-009: Feature Dependencies

**Priority**: HIGH

The DECOMPOSITION MUST include:

- [ ] Dependency diagram (text or visual)
- [ ] Dependency rationale for each relationship
- [ ] Foundation Features identified

**Why it matters**: Dependencies determine implementation order.

### DECOMP-EPIC-010: Coverage Matrices

**Priority**: CRITICAL

The DECOMPOSITION MUST include:

- [ ] Requirements → Features matrix (requirement, feature, priority, status)
- [ ] Design Components → Features matrix
- [ ] Platform Implementation matrix (Feature, KMP, Android, iOS)

**Why it matters**: Matrices enable coverage validation.

### DECOMP-EPIC-011: Implementation Order

**Priority**: HIGH

The DECOMPOSITION MUST include:

- [ ] Implementation order table (phase, Features, rationale)
- [ ] Foundation Features first
- [ ] Dependent Features ordered properly
- [ ] Parallel Features identified

**Why it matters**: Order enables sprint planning.

### DECOMP-EPIC-012: Acceptance Criteria Summary

**Priority**: HIGH

The DECOMPOSITION MUST include:

- [ ] Acceptance criteria table (Feature, key criteria)
- [ ] 1-2 key criteria per Feature

**Why it matters**: Summary enables quick validation scope understanding.

---

## SHOULD HAVE Requirements

### DECOMP-EPIC-013: State Management References

**Priority**: MEDIUM

Features with state SHOULD include:

- [ ] State reference `cpt-{subapp}-{epic}-state`
- [ ] State management component reference

### DECOMP-EPIC-014: API Contract References

**Priority**: MEDIUM

Features using APIs SHOULD reference:

- [ ] API ID from DESIGN
- [ ] Contract location

---

## MUST NOT HAVE (Violations)

### DECOMP-EPIC-NO-001: No CDSL Flows

**Priority**: HIGH

The DECOMPOSITION MUST NOT contain:

- [ ] Actor flow definitions (belongs in FEATURE)
- [ ] Algorithm steps (belongs in FEATURE)
- [ ] State machine definitions (belongs in FEATURE)

**Why it matters**: CDSL belongs in FEATURE documents.

### DECOMP-EPIC-NO-002: No Implementation Code

**Priority**: HIGH

The DECOMPOSITION MUST NOT contain:

- [ ] Code snippets (belongs in DESIGN/IMPL)
- [ ] Class definitions (belongs in DESIGN)
- [ ] Method signatures (belongs in DESIGN)

**Why it matters**: Decomposition is organizational, not technical.

### DECOMP-EPIC-NO-003: No Missing Traceability

**Priority**: CRITICAL

The DECOMPOSITION MUST NOT have:

- [ ] Features without requirement coverage
- [ ] Requirements without Feature allocation
- [ ] Components without Feature assignment
- [ ] Platform implementations missing

**Why it matters**: Full traceability is the purpose of decomposition.

### DECOMP-EPIC-NO-004: No DoD Definitions

**Priority**: HIGH

The DECOMPOSITION MUST NOT contain:

- [ ] Definition of Done sections (belongs in FEATURE)
- [ ] Verification steps (belongs in FEATURE)
- [ ] Test requirements (belongs in FEATURE)

**Why it matters**: DoD belongs in FEATURE documents.

---

## Mobile-Specific Criteria

### MOBILE-DECOMP-001: Tri-Platform Implementation

**Priority**: CRITICAL

Platform Implementation matrix MUST show:

- [ ] KMP column with module names
- [ ] Android column with component names
- [ ] iOS column with component names
- [ ] Checkbox status for each cell

### MOBILE-DECOMP-002: Code Location Pattern

**Priority**: HIGH

Platform locations MUST follow patterns:

- [ ] KMP: `constructor-sdk/feature/{subapp}/`
- [ ] Android: `android-app/feature/{subapp}/ui/`
- [ ] iOS: `ios-app/Features/{SubApp}/Views/`

### MOBILE-DECOMP-003: Shared vs Platform-Specific

**Priority**: MEDIUM

Features SHOULD note:

- [ ] Which components are shared (KMP)
- [ ] Which components are platform-specific

### MOBILE-DECOMP-004: WebView Features

**Priority**: MEDIUM

Features using WebView SHOULD note:

- [ ] WebView integration type
- [ ] JS bridge requirements

---

## Reporting

### Report Format

For each issue found, report:

```markdown
## Issue: {CHECKLIST-ID}

**Severity**: CRITICAL | HIGH | MEDIUM | LOW

**Why Applicable**: {Why this requirement applies}

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
