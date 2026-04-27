# DECOMPOSITION-MINIAPP Checklist

**Artifact**: DECOMPOSITION-MINIAPP  
**Kit**: mobile-superapp  
**Level**: L1 (MiniApp)

This checklist provides semantic quality criteria for MiniApp-level Decomposition documents in mobile SuperApp projects.

---

## Table of Contents

1. [MUST HAVE Requirements](#must-have-requirements)
2. [SHOULD HAVE Requirements](#should-have-requirements)
3. [MUST NOT HAVE (Violations)](#must-not-have-violations)
4. [Mobile-Specific Criteria](#mobile-specific-criteria)
5. [Reporting](#reporting)

---

## MUST HAVE Requirements

### DECOMP-MINIAPP-001: Overview Section

**Priority**: CRITICAL

The DECOMPOSITION MUST include:

- [ ] Clear purpose statement
- [ ] Link to MiniApp PRD
- [ ] Link to MiniApp DESIGN
- [ ] Link to Platform DECOMPOSITION
- [ ] Overall implementation status marker with ID

**Why it matters**: Overview establishes context for Epic decomposition.

### DECOMP-MINIAPP-002: Epic Categories

**Priority**: CRITICAL

The DECOMPOSITION MUST organize Epics by category:

- [ ] Screens section (Screen Epics)
- [ ] Capabilities section (cross-cutting Epics)
- [ ] Flows section (multi-screen journey Epics)

**Why it matters**: Categories clarify Epic types and dependencies.

### DECOMP-MINIAPP-003: Screen Epic Entries

**Priority**: CRITICAL

Each Screen Epic entry MUST include:

- [ ] Epic ID following `cpt-{miniapp}-epic-{screen}` pattern
- [ ] Link to Epic folder
- [ ] Priority (HIGH, MEDIUM, LOW)
- [ ] Category: Screen
- [ ] Purpose description
- [ ] Actors (actor references)
- [ ] Depends On (other Epics or "None")
- [ ] Scope (widgets/features list)
- [ ] Out of scope (explicit exclusions)

**Why it matters**: Complete entries enable independent Epic development.

### DECOMP-MINIAPP-004: Capability Epic Entries

**Priority**: HIGH

Each Capability Epic entry MUST include:

- [ ] Epic ID following `cpt-{miniapp}-epic-{capability}` pattern
- [ ] Category: Capability (cross-cutting)
- [ ] Purpose description
- [ ] Kernel integration references
- [ ] Scope of capability

**Why it matters**: Capabilities are shared across screens.

### DECOMP-MINIAPP-005: Flow Epic Entries

**Priority**: HIGH

Each Flow Epic entry MUST include:

- [ ] Epic ID following `cpt-{miniapp}-epic-{flow}` pattern
- [ ] Category: Flow (multi-screen journey)
- [ ] Purpose description
- [ ] Screens involved (ordered list)
- [ ] Depends On (screen Epics involved)

**Why it matters**: Flows define user journeys spanning screens.

### DECOMP-MINIAPP-006: Requirements Coverage

**Priority**: CRITICAL

Each Epic entry MUST document:

- [ ] Requirements covered list
- [ ] `cpt-{miniapp}-fr-{slug}` references for FRs
- [ ] `cpt-{miniapp}-nfr-{slug}` references for NFRs (if applicable)
- [ ] Priority marker for each requirement
- [ ] Checkbox for implementation status

**Why it matters**: Coverage ensures all MiniApp FRs are allocated to Epics.

### DECOMP-MINIAPP-007: Design Components

**Priority**: HIGH

Each Epic entry MUST list:

- [ ] Design components from MiniApp DESIGN
- [ ] `cpt-{miniapp}-component-{slug}` references
- [ ] Priority marker for each component

**Why it matters**: Components trace DESIGN elements to Epics.

### DECOMP-MINIAPP-008: Epic Dependencies

**Priority**: HIGH

The DECOMPOSITION MUST include:

- [ ] Dependency diagram (text or visual)
- [ ] Dependency rationale for each relationship
- [ ] Cross-cutting capabilities noted

**Why it matters**: Dependencies determine implementation order.

### DECOMP-MINIAPP-009: Coverage Matrices

**Priority**: CRITICAL

The DECOMPOSITION MUST include:

- [ ] Requirements coverage matrix (requirement ID → Epic → status)
- [ ] Design component coverage matrix (component ID → Epic → status)
- [ ] All items with checkbox status

**Why it matters**: Matrices enable coverage validation.

### DECOMP-MINIAPP-010: Implementation Order

**Priority**: HIGH

The DECOMPOSITION MUST include:

- [ ] Implementation order table (phase, Epics, rationale)
- [ ] Foundation Epics first
- [ ] Dependent Epics ordered by dependencies
- [ ] Parallel Epics identified

**Why it matters**: Order enables sprint planning.

---

## SHOULD HAVE Requirements

### DECOMP-MINIAPP-011: Target Release Per Epic

**Priority**: MEDIUM

Each Epic entry SHOULD include:

- [ ] Target release (Q{X} 202{Y})
- [ ] Alignment with Platform roadmap

### DECOMP-MINIAPP-012: KMP Module References

**Priority**: MEDIUM

Screen/Capability Epics SHOULD include:

- [ ] KMP module reference `cpt-{miniapp}-component-kmp-{slug}`
- [ ] Module location hint

### DECOMP-MINIAPP-013: Widget Lists

**Priority**: LOW

Screen Epics SHOULD list:

- [ ] Key widgets in scope
- [ ] Widget-to-Epic allocation

---

## MUST NOT HAVE (Violations)

### DECOMP-MINIAPP-NO-001: No Feature Details

**Priority**: HIGH

The DECOMPOSITION MUST NOT contain:

- [ ] Feature-level breakdowns (belongs in DECOMPOSITION-EPIC)
- [ ] CDSL flows (belongs in FEATURE)
- [ ] DoD definitions (belongs in FEATURE)

**Why it matters**: MiniApp DECOMPOSITION only covers Epics.

### DECOMP-MINIAPP-NO-002: No Implementation Details

**Priority**: HIGH

The DECOMPOSITION MUST NOT contain:

- [ ] Code locations (belongs in DESIGN/IMPL)
- [ ] API contracts (belongs in DESIGN)
- [ ] State definitions (belongs in DESIGN)

**Why it matters**: Decomposition is organizational, not technical.

### DECOMP-MINIAPP-NO-003: No Missing Traceability

**Priority**: CRITICAL

The DECOMPOSITION MUST NOT have:

- [ ] Epics without requirement coverage
- [ ] Requirements without Epic allocation
- [ ] Components without Epic assignment

**Why it matters**: Full traceability is the purpose of decomposition.

### DECOMP-MINIAPP-NO-004: No Platform DECOMPOSITION Duplication

**Priority**: MEDIUM

The DECOMPOSITION MUST NOT:

- [ ] Repeat MiniApp entry details from Platform DECOMPOSITION
- [ ] Redefine MiniApp scope (reference only)

**Why it matters**: Reference Platform DECOMPOSITION for MiniApp context.

---

## Mobile-Specific Criteria

### MOBILE-DECOMP-001: Platform Implementation Matrix

**Priority**: HIGH

Coverage matrices SHOULD include:

- [ ] KMP implementation column
- [ ] Android implementation column
- [ ] iOS implementation column
- [ ] Status checkboxes per platform

### MOBILE-DECOMP-002: Kernel Integration References

**Priority**: HIGH

Capability Epics MUST reference:

- [ ] Kernel services used
- [ ] `cpt-{platform}-component-{kernel}` IDs

### MOBILE-DECOMP-003: Navigation Dependencies

**Priority**: MEDIUM

Screen Epics SHOULD note:

- [ ] Entry point screens (no dependencies)
- [ ] Navigation flow dependencies

### MOBILE-DECOMP-004: Offline Epics

**Priority**: MEDIUM

Epics with offline capability SHOULD note:

- [ ] Offline capability in scope
- [ ] Storage requirements

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
