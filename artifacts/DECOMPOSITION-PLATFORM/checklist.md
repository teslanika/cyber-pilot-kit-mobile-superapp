# DECOMPOSITION-PLATFORM Checklist

**Artifact**: DECOMPOSITION-PLATFORM  
**Kit**: mobile-superapp  
**Level**: L0 (Platform)

This checklist provides semantic quality criteria for Platform-level Decomposition documents in mobile SuperApp projects.

---

## Table of Contents

1. [MUST HAVE Requirements](#must-have-requirements)
2. [SHOULD HAVE Requirements](#should-have-requirements)
3. [MUST NOT HAVE (Violations)](#must-not-have-violations)
4. [Mobile-Specific Criteria](#mobile-specific-criteria)
5. [Reporting](#reporting)

---

## MUST HAVE Requirements

### DECOMP-PLATFORM-001: Overview Section

**Priority**: CRITICAL

The DECOMPOSITION MUST include:

- [ ] Clear purpose statement
- [ ] Link to Platform PRD
- [ ] Link to Platform DESIGN
- [ ] Overall implementation status marker

**Why it matters**: Overview establishes context for decomposition.

### DECOMP-PLATFORM-002: MiniApp Entries Structure

**Priority**: CRITICAL

Each MiniApp entry MUST include:

- [ ] MiniApp ID following `cpt-{platform}-miniapp-{miniapp}` pattern
- [ ] Link to MiniApp folder
- [ ] Priority (HIGH, MEDIUM, LOW)
- [ ] Purpose description (few sentences)
- [ ] Target users (actor references)
- [ ] Dependencies (Kernel, other MiniApps)
- [ ] Scope (in-scope list)
- [ ] Out-of-scope (explicit exclusions)

**Why it matters**: Complete entries enable independent MiniApp development.

### DECOMP-PLATFORM-003: Requirements Coverage

**Priority**: CRITICAL

Each MiniApp entry MUST document:

- [ ] Requirements covered list with IDs
- [ ] `cpt-{platform}-fr-{slug}` references for each FR
- [ ] Requirement summary for each
- [ ] Priority marker for each requirement
- [ ] Checkbox for implementation status

**Why it matters**: Coverage ensures all Platform FRs are allocated to MiniApps.

### DECOMP-PLATFORM-004: Platform Components

**Priority**: HIGH

Each MiniApp entry MUST list:

- [ ] Platform components from DESIGN used by this MiniApp
- [ ] `cpt-{platform}-component-{slug}` references
- [ ] Priority marker for each component
- [ ] Checkbox for implementation status

**Why it matters**: Components trace DESIGN elements to MiniApps.

### DECOMP-PLATFORM-005: Integration Points

**Priority**: HIGH

Each MiniApp entry MUST document:

- [ ] External integration references
- [ ] `cpt-{platform}-integration-{slug}` IDs
- [ ] Integration description

**Why it matters**: Integrations define external dependencies.

### DECOMP-PLATFORM-006: Shared Kernel Components

**Priority**: CRITICAL

The DECOMPOSITION MUST include:

- [ ] Kernel components table
- [ ] Component ID, name, and MiniApps using each
- [ ] Auth, Storage, Network, Notifications kernel modules

**Why it matters**: Kernel components are shared dependencies.

### DECOMP-PLATFORM-007: MiniApp Dependencies

**Priority**: HIGH

The DECOMPOSITION MUST include:

- [ ] Dependency diagram (text or visual)
- [ ] Dependency rationale for each relationship
- [ ] Kernel as root dependency
- [ ] Inter-MiniApp communication patterns (deep links, events)

**Why it matters**: Dependencies determine implementation order.

### DECOMP-PLATFORM-008: Release Roadmap

**Priority**: HIGH

The DECOMPOSITION MUST include:

- [ ] Release roadmap table (quarter, MiniApps, milestone)
- [ ] Chronological ordering
- [ ] Milestone descriptions

**Why it matters**: Roadmap enables release planning.

---

## SHOULD HAVE Requirements

### DECOMP-PLATFORM-009: Target Release Per MiniApp

**Priority**: MEDIUM

Each MiniApp entry SHOULD include:

- [ ] Target release (Q{X} 202{Y})
- [ ] Alignment with roadmap table

### DECOMP-PLATFORM-010: Full Coverage Validation

**Priority**: MEDIUM

The DECOMPOSITION SHOULD verify:

- [ ] All Platform FRs appear in at least one MiniApp
- [ ] No Platform FRs are orphaned
- [ ] Coverage can be traced to DESIGN components

### DECOMP-PLATFORM-011: MiniApp Isolation

**Priority**: MEDIUM

The DECOMPOSITION SHOULD document:

- [ ] MiniApps are loosely coupled
- [ ] Communication only via deep links and events
- [ ] No direct MiniApp-to-MiniApp calls

---

## MUST NOT HAVE (Violations)

### DECOMP-PLATFORM-NO-001: No Epic Details

**Priority**: HIGH

The DECOMPOSITION MUST NOT contain:

- [ ] Epic-level breakdowns (belongs in DECOMPOSITION-MINIAPP)
- [ ] Screen definitions (belongs in MiniApp)
- [ ] Feature lists (belongs in MiniApp)

**Why it matters**: Platform DECOMPOSITION only covers MiniApps.

### DECOMP-PLATFORM-NO-002: No Implementation Details

**Priority**: HIGH

The DECOMPOSITION MUST NOT contain:

- [ ] Code locations (belongs in DESIGN/IMPL)
- [ ] Module structures (belongs in DESIGN)
- [ ] Technical specifications (belongs in DESIGN)

**Why it matters**: Decomposition is organizational, not technical.

### DECOMP-PLATFORM-NO-003: No Missing Traceability

**Priority**: CRITICAL

The DECOMPOSITION MUST NOT have:

- [ ] MiniApps without requirement coverage
- [ ] Requirements without MiniApp allocation
- [ ] Components without MiniApp assignment

**Why it matters**: Full traceability is the purpose of decomposition.

### DECOMP-PLATFORM-NO-004: No Inconsistent Priorities

**Priority**: MEDIUM

The DECOMPOSITION MUST NOT have:

- [ ] Priority mismatches between MiniApp level and requirements
- [ ] P1 requirements in LOW priority MiniApps without justification

**Why it matters**: Priorities should align across hierarchy.

---

## Mobile-Specific Criteria

### MOBILE-DECOMP-001: Kernel Dependencies

**Priority**: CRITICAL

All MiniApps MUST depend on:

- [ ] Auth Kernel (`cpt-{platform}-component-auth-kernel`)
- [ ] Storage Kernel (`cpt-{platform}-component-storage-kernel`)
- [ ] Network Kernel (`cpt-{platform}-component-network-kernel`)

### MOBILE-DECOMP-002: Platform-Specific Notes

**Priority**: MEDIUM

Where applicable, MiniApp entries SHOULD note:

- [ ] iOS-specific considerations
- [ ] Android-specific considerations
- [ ] Platform parity requirements

### MOBILE-DECOMP-003: Notification Integration

**Priority**: MEDIUM

MiniApps using notifications MUST reference:

- [ ] Notifications Kernel dependency
- [ ] Push notification integration point

### MOBILE-DECOMP-004: Offline-First MiniApps

**Priority**: MEDIUM

MiniApps with offline requirements SHOULD note:

- [ ] Offline capability in scope
- [ ] Storage Kernel usage for offline data

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
