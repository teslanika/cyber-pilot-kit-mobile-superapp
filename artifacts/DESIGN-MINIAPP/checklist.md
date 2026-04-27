# DESIGN-MINIAPP Checklist

**Artifact**: DESIGN-MINIAPP  
**Kit**: mobile-superapp  
**Level**: L1 (MiniApp)

This checklist provides semantic quality criteria for MiniApp-level technical design documents in mobile SuperApp projects.

---

## Table of Contents

1. [MUST HAVE Requirements](#must-have-requirements)
2. [SHOULD HAVE Requirements](#should-have-requirements)
3. [MUST NOT HAVE (Violations)](#must-not-have-violations)
4. [Mobile-Specific Criteria](#mobile-specific-criteria)
5. [Reporting](#reporting)

---

## MUST HAVE Requirements

### ARCH-MINIAPP-001: MiniApp Overview Completeness

**Priority**: CRITICAL

The MiniApp DESIGN MUST include:

- [ ] Clear purpose statement (1-2 paragraphs)
- [ ] Link to parent Platform DESIGN
- [ ] Capabilities table mapping MiniApp PRD FRs to design responses
- [ ] NFR allocation table with design responses
- [ ] ADR references for key decisions

**Why it matters**: Without clear purpose and traceability, the MiniApp's role in the SuperApp ecosystem is unclear.

### ARCH-MINIAPP-002: Module Structure Definition

**Priority**: CRITICAL

The DESIGN MUST define module structure for all platforms:

- [ ] KMP shared logic modules (domain, data, presentation)
- [ ] Android UI modules with Compose structure
- [ ] iOS UI modules with SwiftUI structure
- [ ] Module dependencies clearly documented
- [ ] Code locations specified for each module

**Why it matters**: Mobile SuperApps require consistent module organization across platforms for maintainability.

### ARCH-MINIAPP-003: Navigation Architecture

**Priority**: HIGH

The DESIGN MUST include:

- [ ] Navigation graph (visual or Mermaid diagram)
- [ ] Screen inventory table (route, description, implementation type)
- [ ] Deep link schema with parameters
- [ ] Deep link handling flow description

**Why it matters**: Navigation is critical for mobile UX and MiniApp integration.

### ARCH-MINIAPP-004: State Management Pattern

**Priority**: CRITICAL

The DESIGN MUST document MVI pattern:

- [ ] State class structure (immutable data class)
- [ ] Intent sealed class (user actions)
- [ ] Effect sealed class (side effects)
- [ ] ViewModel flow diagram
- [ ] State persistence strategy (persisted vs transient)

**Why it matters**: Consistent state management is essential for predictable app behavior.

### ARCH-MINIAPP-005: Domain Model

**Priority**: HIGH

The DESIGN MUST define:

- [ ] Core entities table with descriptions and locations
- [ ] Entity relationships (diagram preferred)
- [ ] Repository interfaces with key methods
- [ ] Entity IDs following `cpt-{miniapp}-entity-{slug}` pattern

**Why it matters**: Domain model is the foundation of business logic.

### ARCH-MINIAPP-006: Kernel Integration

**Priority**: CRITICAL

The DESIGN MUST specify:

- [ ] Required kernel services table (Auth, Storage, Network, Notifications)
- [ ] Criticality of each service
- [ ] MiniApp contract interface implementation (code snippet)
- [ ] Lifecycle methods (initialize, start, handleDeepLink, onBackground, onForeground, dispose)

**Why it matters**: MiniApps must integrate properly with the host app's shared services.

### ARCH-MINIAPP-007: Traceability Section

**Priority**: HIGH

The DESIGN MUST include traceability links:

- [ ] MiniApp PRD reference
- [ ] Platform DESIGN reference
- [ ] ADRs folder reference
- [ ] DECOMPOSITION reference
- [ ] Epics folder references (screens/, capabilities/, flows/)

**Why it matters**: Traceability enables validation and change impact analysis.

---

## SHOULD HAVE Requirements

### ARCH-MINIAPP-008: API Layer Documentation

**Priority**: MEDIUM

The DESIGN SHOULD include:

- [ ] BFF endpoints table (method, endpoint, description, request, response)
- [ ] WebSocket connections (if applicable)
- [ ] Authentication requirements

### ARCH-MINIAPP-009: Screen Implementation Types

**Priority**: MEDIUM

For each screen in navigation inventory:

- [ ] Implementation type specified (Native / WebView / Hybrid)
- [ ] Rationale for WebView choices documented

### ARCH-MINIAPP-010: Module Dependencies

**Priority**: MEDIUM

The DESIGN SHOULD document:

- [ ] Android module dependencies (KMP shared, common/ui, common/navigation)
- [ ] iOS module dependencies (ConstructorSDK, Common/UI, Common/Navigation)
- [ ] External library dependencies

---

## MUST NOT HAVE (Violations)

### ARCH-MINIAPP-NO-001: No Implementation Code

**Priority**: HIGH

The DESIGN MUST NOT contain:

- [ ] Complete class implementations (beyond interface definitions)
- [ ] Full method bodies
- [ ] Production code snippets beyond illustrative examples

**Why it matters**: Implementation belongs in code, not documentation.

### ARCH-MINIAPP-NO-002: No Feature-Level Details

**Priority**: MEDIUM

The DESIGN MUST NOT contain:

- [ ] Detailed UI flows (belongs in DESIGN-EPIC)
- [ ] Widget specifications (belongs in DESIGN-EPIC)
- [ ] Acceptance criteria (belongs in FEATURE)

**Why it matters**: DESIGN-MINIAPP is architectural, not feature-specific.

### ARCH-MINIAPP-NO-003: No Product Requirements

**Priority**: HIGH

The DESIGN MUST NOT contain:

- [ ] Business requirements (belongs in PRD)
- [ ] User stories (belongs in PRD)
- [ ] Acceptance criteria (belongs in PRD/FEATURE)

**Why it matters**: Separation of concerns between PRD and DESIGN.

### ARCH-MINIAPP-NO-004: No Platform DESIGN Duplication

**Priority**: MEDIUM

The DESIGN MUST NOT:

- [ ] Redefine Platform-level patterns
- [ ] Duplicate kernel service specifications
- [ ] Redefine actors (reference Platform actors)

**Why it matters**: Avoid inconsistency with Platform DESIGN.

---

## Mobile-Specific Criteria

### MOBILE-MINIAPP-001: KMP Module Organization

**Priority**: HIGH

KMP modules MUST follow structure:

- [ ] `domain/` — domain entities and rules
- [ ] `data/` — repository implementations, API clients, local sources
- [ ] `presentation/` — ViewModels, State, Intent, Effect

### MOBILE-MINIAPP-002: Android Module Organization

**Priority**: HIGH

Android modules MUST follow structure:

- [ ] `ui/` — Compose screens and components
- [ ] `navigation/` — Navigation graph
- [ ] Hilt DI modules documented

### MOBILE-MINIAPP-003: iOS Module Organization

**Priority**: HIGH

iOS modules MUST follow structure:

- [ ] `Views/` — SwiftUI views
- [ ] `Navigation/` — Coordinators
- [ ] KMP integration pattern documented

### MOBILE-MINIAPP-004: MVI Implementation Consistency

**Priority**: CRITICAL

State management MUST be consistent:

- [ ] State is immutable data class
- [ ] Intents are sealed class
- [ ] Effects are sealed class
- [ ] ViewModel processes Intent → State + Effects

### MOBILE-MINIAPP-005: Deep Link Schema

**Priority**: HIGH

Deep links MUST follow pattern:

- [ ] Format: `constructor://{miniapp}/{path}?{params}`
- [ ] Parameters documented
- [ ] Handling flow described

---

## Reporting

### Report Format

For each issue found, report:

```markdown
## Issue: {CHECKLIST-ID}

**Severity**: CRITICAL | HIGH | MEDIUM | LOW

**Why Applicable**: {Why this requirement applies to this MiniApp}

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
