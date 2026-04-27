# DESIGN-EPIC Checklist

**Artifact**: DESIGN-EPIC  
**Kit**: mobile-superapp  
**Level**: L2 (Epic)

This checklist provides semantic quality criteria for Epic-level Technical Design documents in mobile SuperApp projects.

---

## Table of Contents

1. [MUST HAVE Requirements](#must-have-requirements)
2. [SHOULD HAVE Requirements](#should-have-requirements)
3. [MUST NOT HAVE (Violations)](#must-not-have-violations)
4. [Mobile-Specific Criteria](#mobile-specific-criteria)
5. [Reporting](#reporting)

---

## MUST HAVE Requirements

### ARCH-EPIC-001: Epic Overview

**Priority**: CRITICAL

The Epic DESIGN MUST include:

- [ ] Purpose statement (1-2 paragraphs)
- [ ] Link to parent MiniApp DESIGN
- [ ] Requirements coverage table (requirement ID → design response)
- [ ] ADR references

**Why it matters**: Overview connects Epic design to requirements.

### ARCH-EPIC-002: Component Architecture

**Priority**: CRITICAL

The DESIGN MUST include component architecture:

- [ ] Component diagram (Mermaid or visual)
- [ ] UI layer components
- [ ] ViewModel layer components
- [ ] Domain layer components
- [ ] Data layer components
- [ ] Component ID `cpt-{miniapp}-epic-{epic}-component-overview`

**Why it matters**: Component architecture guides implementation structure.

### ARCH-EPIC-003: Screen Components

**Priority**: CRITICAL

For each screen, the DESIGN MUST include:

- [ ] Screen ID following `cpt-{miniapp}-{epic}-screen-{slug}` pattern
- [ ] Responsibility description
- [ ] Platform implementation table (KMP, Android, iOS locations)
- [ ] Priority marker

**Why it matters**: Screen components are primary implementation units.

### ARCH-EPIC-004: Widget Components

**Priority**: HIGH

For each widget, the DESIGN MUST include:

- [ ] Widget ID following `cpt-{miniapp}-{epic}-widget-{slug}` pattern
- [ ] Responsibility description
- [ ] States (default, loading, error, empty, success)
- [ ] Props/parameters with types
- [ ] Priority marker

**Why it matters**: Widgets are reusable UI building blocks.

### ARCH-EPIC-005: State Management

**Priority**: CRITICAL

The DESIGN MUST document MVI state management:

- [ ] State class structure (Kotlin data class)
- [ ] ScreenState sealed class (Loading, Content, Error)
- [ ] Intent sealed class (user actions)
- [ ] Effect sealed class (side effects)
- [ ] State ID `cpt-{miniapp}-{epic}-state`

**Why it matters**: Consistent MVI pattern enables predictable behavior.

### ARCH-EPIC-006: Use Cases

**Priority**: HIGH

For each use case, the DESIGN MUST include:

- [ ] Use case ID following `cpt-{miniapp}-{epic}-usecase-{slug}` pattern
- [ ] Input type
- [ ] Output type (Result<T>)
- [ ] Steps (validate, call, transform, return)
- [ ] Code snippet

**Why it matters**: Use cases encapsulate business logic.

### ARCH-EPIC-007: Repository Operations

**Priority**: HIGH

The DESIGN MUST document repository:

- [ ] Repository ID following `cpt-{miniapp}-{epic}-repo-{slug}` pattern
- [ ] Operations table (operation, method, source, caching)
- [ ] Cache strategy (cache-first, network-first, write-through)

**Why it matters**: Repository defines data access patterns.

### ARCH-EPIC-008: Navigation

**Priority**: HIGH

The DESIGN MUST include navigation:

- [ ] Navigation ID following `cpt-{miniapp}-{epic}-nav` pattern
- [ ] Entry points (source, deep link)
- [ ] Exit points (destination, action)
- [ ] Navigation parameters table

**Why it matters**: Navigation defines user journey through Epic.

### ARCH-EPIC-009: Error Handling

**Priority**: HIGH

The DESIGN MUST specify error handling:

- [ ] Error states table (type, UI response, recovery action)
- [ ] Network error handling
- [ ] Auth error handling
- [ ] Validation error handling
- [ ] Server error handling

**Why it matters**: Error handling ensures graceful degradation.

### ARCH-EPIC-010: Traceability Section

**Priority**: HIGH

The DESIGN MUST include:

- [ ] Link to Epic PRD
- [ ] Link to MiniApp DESIGN
- [ ] Link to ADRs folder
- [ ] Link to DECOMPOSITION
- [ ] Link to Features folder

**Why it matters**: Traceability enables navigation and validation.

---

## SHOULD HAVE Requirements

### ARCH-EPIC-011: API Contracts

**Priority**: MEDIUM

The DESIGN SHOULD include:

- [ ] API contracts table (method, endpoint, request, response)
- [ ] API ID `cpt-{miniapp}-{epic}-api-{slug}`
- [ ] Authentication requirements

### ARCH-EPIC-012: Offline Behavior

**Priority**: MEDIUM

If Epic supports offline:

- [ ] Offline capable flag
- [ ] Read behavior offline
- [ ] Write behavior offline
- [ ] Sync behavior
- [ ] Offline ID `cpt-{miniapp}-{epic}-offline`

### ARCH-EPIC-013: WebView Integration

**Priority**: MEDIUM

If Epic uses WebView:

- [ ] WebView URL pattern
- [ ] JS bridge methods
- [ ] Native → WebView events
- [ ] WebView → Native events
- [ ] WebView ID `cpt-{miniapp}-{epic}-webview`

---

## MUST NOT HAVE (Violations)

### ARCH-EPIC-NO-001: No Feature-Level Details

**Priority**: HIGH

The DESIGN MUST NOT contain:

- [ ] CDSL flow definitions (belongs in FEATURE)
- [ ] Step-by-step instructions (belongs in FEATURE)
- [ ] Definition of Done (belongs in FEATURE)
- [ ] Acceptance criteria (belongs in PRD/FEATURE)

**Why it matters**: Epic DESIGN defines architecture, not implementation steps.

### ARCH-EPIC-NO-002: No MiniApp Architecture Duplication

**Priority**: MEDIUM

The DESIGN MUST NOT:

- [ ] Redefine MiniApp-level patterns
- [ ] Duplicate kernel service specifications
- [ ] Redefine navigation architecture

**Why it matters**: Reference MiniApp DESIGN instead of duplicating.

### ARCH-EPIC-NO-003: No Production Code

**Priority**: HIGH

The DESIGN MUST NOT contain:

- [ ] Complete class implementations
- [ ] Full method bodies beyond snippets
- [ ] Actual production code

**Why it matters**: Implementation belongs in code files.

### ARCH-EPIC-NO-004: No Missing IDs

**Priority**: CRITICAL

The DESIGN MUST NOT have:

- [ ] Screens without IDs
- [ ] Widgets without IDs
- [ ] Use cases without IDs
- [ ] States without IDs

**Why it matters**: IDs enable traceability to Features and code.

---

## Mobile-Specific Criteria

### MOBILE-EPIC-001: Platform Implementation Table

**Priority**: CRITICAL

Each component MUST have:

- [ ] KMP module location (`constructor-sdk/feature/{miniapp}/...`)
- [ ] Android location (`android-app/feature/{miniapp}/...`)
- [ ] iOS location (`ios-app/Features/{MiniApp}/...`)

### MOBILE-EPIC-002: Android-Specific Section

**Priority**: HIGH

The DESIGN MUST include Android section:

- [ ] Compose specifics
- [ ] Lifecycle handling
- [ ] Configuration change handling
- [ ] Android ID `cpt-{miniapp}-{epic}-android`

### MOBILE-EPIC-003: iOS-Specific Section

**Priority**: HIGH

The DESIGN MUST include iOS section:

- [ ] SwiftUI specifics
- [ ] Scene phase handling
- [ ] iOS ID `cpt-{miniapp}-{epic}-ios`

### MOBILE-EPIC-004: MVI Consistency

**Priority**: CRITICAL

State management MUST follow MVI:

- [ ] State is immutable data class
- [ ] Intents are sealed class
- [ ] Effects are sealed class
- [ ] ViewModel processes Intent → State + Effects

### MOBILE-EPIC-005: Navigation Parameters

**Priority**: HIGH

Navigation parameters MUST include:

- [ ] Parameter type (String, Int, etc.)
- [ ] Required/optional flag
- [ ] Description

---

## Reporting

### Report Format

For each issue found, report:

```markdown
## Issue: {CHECKLIST-ID}

**Severity**: CRITICAL | HIGH | MEDIUM | LOW

**Why Applicable**: {Why this requirement applies to this Epic}

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
