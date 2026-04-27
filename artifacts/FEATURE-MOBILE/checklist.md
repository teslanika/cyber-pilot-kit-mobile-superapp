# FEATURE-MOBILE Checklist

**Artifact**: FEATURE-MOBILE  
**Kit**: mobile-superapp  
**Level**: L3 (Feature)

This checklist provides semantic quality criteria for Feature specification documents in mobile SuperApp projects.

---

## Table of Contents

1. [MUST HAVE Requirements](#must-have-requirements)
2. [SHOULD HAVE Requirements](#should-have-requirements)
3. [MUST NOT HAVE (Violations)](#must-not-have-violations)
4. [Mobile-Specific Criteria](#mobile-specific-criteria)
5. [Reporting](#reporting)

---

## MUST HAVE Requirements

### FEATURE-001: Feature Context

**Priority**: CRITICAL

The FEATURE MUST include context section:

- [ ] Feature ID following `cpt-{miniapp}-feature-{slug}` pattern
- [ ] Implementation status marker
- [ ] Overview (1-2 sentences)
- [ ] Purpose (why this feature exists)
- [ ] Actors table with role in feature
- [ ] References (Epic PRD, Epic DESIGN, DECOMPOSITION, Dependencies)

**Why it matters**: Context establishes feature scope and traceability.

### FEATURE-002: Actor Flows (CDSL)

**Priority**: CRITICAL

The FEATURE MUST include Actor Flows:

- [ ] Primary flow with ID `cpt-{miniapp}-flow-{feature-slug}-{slug}`
- [ ] Actor reference
- [ ] Success scenarios listed
- [ ] Error scenarios listed
- [ ] Numbered steps with checkboxes

**Why it matters**: Actor flows define user-facing interactions.

### FEATURE-003: CDSL Step Format

**Priority**: CRITICAL

Each CDSL step MUST follow format:

- [ ] Checkbox `[ ]`
- [ ] Priority marker (`p1`, `p2`, `p3`)
- [ ] Step description
- [ ] Instruction ID `inst-{step-id}`

**Why it matters**: Consistent format enables automation and tracking.

### FEATURE-004: Control Flow Keywords

**Priority**: HIGH

CDSL steps MUST use control flow keywords:

- [ ] **IF** / **ELSE** for conditionals
- [ ] **TRY** / **CATCH** for error handling
- [ ] **RETURN** for completion points
- [ ] **WHEN** for event handling
- [ ] Nested steps with indentation

**Why it matters**: Keywords enable flow analysis and code generation.

### FEATURE-005: API and DB Markers

**Priority**: HIGH

Steps involving data MUST include:

- [ ] **API**: `{METHOD} /api/v1/mobile/{path}` for API calls
- [ ] **DB**: `{OPERATION}` {table} ({key columns}) for database operations
- [ ] Request/response summary for API calls

**Why it matters**: Markers identify integration points.

### FEATURE-006: Platform Implementation Sections

**Priority**: CRITICAL

The FEATURE MUST include platform sections:

- [ ] Section 3.1: KMP Shared Logic
- [ ] Section 3.2: Android UI
- [ ] Section 3.3: iOS UI
- [ ] Each section with ID `cpt-{miniapp}-algo-{feature-slug}-{platform}`

**Why it matters**: Platform sections guide implementation.

### FEATURE-007: KMP Implementation (CDSL)

**Priority**: CRITICAL

KMP section MUST include:

- [ ] Algorithm ID `cpt-{miniapp}-algo-{feature-slug}-kmp`
- [ ] Location (`constructor-sdk/feature/{miniapp}/`)
- [ ] ViewModel steps (receive intent, call use case, update state, emit effects)
- [ ] Use Case steps (validate, call repo, transform, return)
- [ ] Repository steps (cache check, fetch, store, return)

**Why it matters**: KMP contains shared business logic.

### FEATURE-008: Android Implementation (CDSL)

**Priority**: CRITICAL

Android section MUST include:

- [ ] Algorithm ID `cpt-{miniapp}-algo-{feature-slug}-android`
- [ ] Location (`android-app/feature/{miniapp}/ui/`)
- [ ] Compose Screen steps (collect state, render, handle actions, handle effects)

**Why it matters**: Android UI implementation guidance.

### FEATURE-009: iOS Implementation (CDSL)

**Priority**: CRITICAL

iOS section MUST include:

- [ ] Algorithm ID `cpt-{miniapp}-algo-{feature-slug}-ios`
- [ ] Location (`ios-app/Features/{MiniApp}/Views/`)
- [ ] SwiftUI View steps (observe state, render body, handle actions, handle effects)

**Why it matters**: iOS UI implementation guidance.

### FEATURE-010: State Machine (CDSL)

**Priority**: CRITICAL

The FEATURE MUST include state machine:

- [ ] State ID `cpt-{miniapp}-state-{feature-slug}`
- [ ] States list (Loading, Content, Error, Empty)
- [ ] Initial State
- [ ] Transitions with FROM/TO/WHEN format
- [ ] Instruction IDs for each transition

**Why it matters**: State machines define valid state changes.

### FEATURE-011: Definitions of Done

**Priority**: CRITICAL

The FEATURE MUST include DoD:

- [ ] DoD ID following `cpt-{miniapp}-dod-{feature-slug}-{slug}` pattern
- [ ] Clear requirement ("The system MUST...")
- [ ] Implements (which flows)
- [ ] Touches (KMP, Android, iOS, API modules)
- [ ] Verification checklist (unit tests, UI tests, integration tests)

**Why it matters**: DoD defines completion criteria.

### FEATURE-012: Acceptance Criteria

**Priority**: HIGH

The FEATURE MUST include acceptance criteria:

- [ ] Functional criteria (testable)
- [ ] Platform-specific criteria (Android, iOS)
- [ ] Performance criteria (measurable thresholds)
- [ ] Offline criteria (if applicable)

**Why it matters**: Acceptance criteria enable validation.

### FEATURE-013: Traceability

**Priority**: HIGH

The FEATURE MUST include traceability links:

- [ ] Link to Epic PRD
- [ ] Link to Epic DESIGN
- [ ] Link to DECOMPOSITION
- [ ] Links to Implementation files (KMP, Android, iOS)

**Why it matters**: Traceability enables navigation and validation.

---

## SHOULD HAVE Requirements

### FEATURE-014: Alternative Flows

**Priority**: MEDIUM

The FEATURE SHOULD include:

- [ ] Alternative flows for edge cases
- [ ] Trigger for each alternative flow
- [ ] Steps following CDSL format

### FEATURE-015: WebView Integration

**Priority**: MEDIUM

If feature uses WebView:

- [ ] WebView algorithm ID `cpt-{miniapp}-algo-{feature-slug}-webview`
- [ ] WebView URL pattern
- [ ] Native → WebView steps
- [ ] WebView → Native steps

### FEATURE-016: Multiple DoDs

**Priority**: MEDIUM

Complex features SHOULD have:

- [ ] Multiple DoD sections for different aspects
- [ ] Priority markers for each DoD

---

## MUST NOT HAVE (Violations)

### FEATURE-NO-001: No Architecture Decisions

**Priority**: HIGH

The FEATURE MUST NOT contain:

- [ ] Architecture decisions (belongs in DESIGN)
- [ ] Component definitions (belongs in DESIGN)
- [ ] Module structures (belongs in DESIGN)

**Why it matters**: FEATURE implements DESIGN, doesn't define it.

### FEATURE-NO-002: No Missing Instruction IDs

**Priority**: CRITICAL

The FEATURE MUST NOT have:

- [ ] Steps without `inst-{id}` markers
- [ ] Transitions without instruction IDs
- [ ] Flows without IDs

**Why it matters**: IDs enable traceability to code markers.

### FEATURE-NO-003: No Incomplete Platform Coverage

**Priority**: CRITICAL

The FEATURE MUST NOT have:

- [ ] KMP section without steps
- [ ] Android section missing
- [ ] iOS section missing

**Why it matters**: All platforms must be implemented.

### FEATURE-NO-004: No Production Code

**Priority**: HIGH

The FEATURE MUST NOT contain:

- [ ] Complete class implementations
- [ ] Full method bodies
- [ ] Actual production code

**Why it matters**: Implementation belongs in code files.

### FEATURE-NO-005: No Vague DoD

**Priority**: HIGH

The FEATURE MUST NOT have:

- [ ] DoD without "MUST" statement
- [ ] DoD without verification checklist
- [ ] DoD without module references

**Why it matters**: Vague DoD cannot be validated.

---

## Mobile-Specific Criteria

### MOBILE-FEATURE-001: MVI Pattern in KMP

**Priority**: CRITICAL

KMP ViewModel steps MUST follow MVI:

- [ ] Receive Intent from UI
- [ ] Process through Use Case
- [ ] Update State
- [ ] Emit Effects for side effects

### MOBILE-FEATURE-002: Compose Pattern in Android

**Priority**: CRITICAL

Android steps MUST follow Compose pattern:

- [ ] Collect state with `collectAsStateWithLifecycle`
- [ ] Render UI based on state
- [ ] Send intents on user action
- [ ] Handle effects (navigation, snackbar, dialog)

### MOBILE-FEATURE-003: SwiftUI Pattern in iOS

**Priority**: CRITICAL

iOS steps MUST follow SwiftUI pattern:

- [ ] Observe state from ViewModel
- [ ] Render body based on state
- [ ] Call ViewModel methods on action
- [ ] Handle effects (navigation, alert, sheet)

### MOBILE-FEATURE-004: Cache-First Strategy

**Priority**: HIGH

Repository steps SHOULD implement:

- [ ] Check local cache first
- [ ] Return cached if valid
- [ ] Fetch from API if cache invalid
- [ ] Store in cache after fetch

### MOBILE-FEATURE-005: Error Mapping

**Priority**: HIGH

Use Case steps MUST include:

- [ ] TRY/CATCH for API calls
- [ ] Error mapping to domain errors
- [ ] Result<T> return type

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
