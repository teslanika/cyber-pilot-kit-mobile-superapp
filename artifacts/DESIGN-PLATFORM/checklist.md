# DESIGN-PLATFORM Checklist

**Artifact**: DESIGN-PLATFORM  
**Kit**: mobile-superapp  
**Level**: L0 (Platform)

This checklist provides semantic quality criteria for Platform-level Technical Design documents in mobile SuperApp projects.

---

## Table of Contents

1. [MUST HAVE Requirements](#must-have-requirements)
2. [SHOULD HAVE Requirements](#should-have-requirements)
3. [MUST NOT HAVE (Violations)](#must-not-have-violations)
4. [Mobile-Specific Criteria](#mobile-specific-criteria)
5. [Reporting](#reporting)

---

## MUST HAVE Requirements

### ARCH-PLATFORM-001: Architectural Vision

**Priority**: CRITICAL

The Platform DESIGN MUST include:

- [ ] Architectural vision statement (2-3 paragraphs)
- [ ] Key architectural decisions summary
- [ ] Design philosophy
- [ ] ADR references following `cpt-{platform}-adr-{slug}` pattern

**Why it matters**: Vision aligns all MiniApp implementations with Platform goals.

### ARCH-PLATFORM-002: Architecture Drivers

**Priority**: CRITICAL

The DESIGN MUST document architecture drivers:

- [ ] Functional drivers table (requirement → design response)
- [ ] NFR allocation table (NFR ID, summary, allocated to, design response, verification)
- [ ] Priority markers for each driver

**Why it matters**: Drivers justify architectural decisions and enable traceability.

### ARCH-PLATFORM-003: Platform Layers

**Priority**: CRITICAL

The DESIGN MUST define platform layers:

- [ ] Layer diagram (visual or ASCII)
- [ ] Layers table (layer, responsibility, technology, location)
- [ ] Presentation layer (Native UI shell)
- [ ] Application layer (KMP SDK)
- [ ] Domain layer (Business model)
- [ ] Infrastructure layer (Platform APIs)
- [ ] Layer IDs following `cpt-{platform}-layer-{name}` pattern

**Why it matters**: Clear layering enables consistent implementation across teams.

### ARCH-PLATFORM-004: Cross-Platform Strategy

**Priority**: CRITICAL

The DESIGN MUST specify hybrid strategy:

- [ ] Native vs WebView decision matrix
- [ ] Implementation type for each content type
- [ ] Rationale for each decision
- [ ] ADR reference for hybrid approach

**Why it matters**: Hybrid strategy affects all feature implementations.

### ARCH-PLATFORM-005: KMP SDK Scope

**Priority**: CRITICAL

The DESIGN MUST define KMP boundaries:

- [ ] Included in KMP list (entities, logic, ViewModels, repos, network, storage)
- [ ] NOT in KMP list (UI components, navigation, permissions, biometrics)
- [ ] Code sharing matrix (module, Android, iOS, KMP Shared)
- [ ] Principle ID `cpt-{platform}-principle-kmp-scope`

**Why it matters**: KMP scope affects code organization for all MiniApps.

### ARCH-PLATFORM-006: MiniApp Architecture

**Priority**: CRITICAL

The DESIGN MUST define MiniApp model:

- [ ] MiniApp container diagram
- [ ] MiniApp interface contract (code snippet)
- [ ] Lifecycle methods (initialize, start, handleDeepLink, onBackground, onForeground, dispose)
- [ ] Component ID `cpt-{platform}-component-miniapp-container`

**Why it matters**: MiniApp model is the foundation for all MiniApp integrations.

### ARCH-PLATFORM-007: MiniApp Lifecycle

**Priority**: HIGH

The DESIGN MUST document lifecycle:

- [ ] States defined (REGISTERED, INITIALIZING, READY, ACTIVE, BACKGROUND, DISPOSED)
- [ ] Initial state specified
- [ ] State transitions documented
- [ ] State ID `cpt-{platform}-state-miniapp-lifecycle`

**Why it matters**: Lifecycle management ensures proper resource handling.

### ARCH-PLATFORM-008: Shared Kernel

**Priority**: CRITICAL

The DESIGN MUST specify kernel modules:

- [ ] Authentication module (responsibilities, technology, location)
- [ ] Storage module (responsibilities, technology, location)
- [ ] Networking module (responsibilities, technology, location)
- [ ] Notifications module (responsibilities, technology, location)
- [ ] Component IDs for each kernel module

**Why it matters**: Kernel modules are shared by all MiniApps.

### ARCH-PLATFORM-009: External Integrations

**Priority**: HIGH

The DESIGN MUST document integrations:

- [ ] Learn Backend integration
- [ ] Proctor Service integration (if applicable)
- [ ] Groups Service integration (if applicable)
- [ ] Notification Service integration
- [ ] Protocol, direction, key contracts for each
- [ ] Integration IDs following `cpt-{platform}-integration-{slug}` pattern

**Why it matters**: Integrations define external dependencies.

### ARCH-PLATFORM-010: Traceability Section

**Priority**: HIGH

The DESIGN MUST include traceability:

- [ ] Link to Platform PRD
- [ ] Link to ADRs folder
- [ ] Link to DECOMPOSITION
- [ ] Link to MiniApps folder

**Why it matters**: Traceability enables navigation and validation.

---

## SHOULD HAVE Requirements

### ARCH-PLATFORM-011: MiniApp Communication

**Priority**: MEDIUM

The DESIGN SHOULD document:

- [ ] Inter-MiniApp navigation via deep links
- [ ] Event bus for cross-MiniApp notifications
- [ ] No direct MiniApp-to-MiniApp calls policy
- [ ] Router component ID

### ARCH-PLATFORM-012: Technology Stack Details

**Priority**: MEDIUM

The DESIGN SHOULD specify:

- [ ] Ktor for networking
- [ ] SQLDelight for storage
- [ ] Specific DI frameworks (Hilt/Koin)
- [ ] Version requirements

### ARCH-PLATFORM-013: Security Architecture

**Priority**: MEDIUM

The DESIGN SHOULD include:

- [ ] Authentication flow overview
- [ ] Token management approach
- [ ] Secure storage strategy
- [ ] Biometric re-auth pattern

---

## MUST NOT HAVE (Violations)

### ARCH-PLATFORM-NO-001: No MiniApp Details

**Priority**: HIGH

The DESIGN MUST NOT contain:

- [ ] MiniApp-specific module structures (belongs in DESIGN-MINIAPP)
- [ ] MiniApp navigation graphs (belongs in DESIGN-MINIAPP)
- [ ] MiniApp-specific state management (belongs in DESIGN-MINIAPP)

**Why it matters**: Platform DESIGN defines patterns, not MiniApp specifics.

### ARCH-PLATFORM-NO-002: No Implementation Code

**Priority**: HIGH

The DESIGN MUST NOT contain:

- [ ] Complete class implementations (beyond interface examples)
- [ ] Full method bodies
- [ ] Production code beyond illustrative snippets

**Why it matters**: Implementation belongs in code, not documentation.

### ARCH-PLATFORM-NO-003: No Product Requirements

**Priority**: HIGH

The DESIGN MUST NOT contain:

- [ ] Business requirements (belongs in PRD)
- [ ] User stories (belongs in PRD)
- [ ] Acceptance criteria (belongs in PRD/FEATURE)

**Why it matters**: DESIGN addresses HOW, PRD addresses WHAT.

### ARCH-PLATFORM-NO-004: No Missing Priority Markers

**Priority**: MEDIUM

The DESIGN MUST NOT have:

- [ ] Components without priority markers (`p1`, `p2`, `p3`)
- [ ] Sections without component IDs
- [ ] Undocumented decisions

**Why it matters**: Priority markers enable incremental implementation.

---

## Mobile-Specific Criteria

### MOBILE-PLATFORM-001: Native Shell Definition

**Priority**: CRITICAL

Platform DESIGN MUST define native shell:

- [ ] iOS native layer (SwiftUI)
- [ ] Android native layer (Jetpack Compose)
- [ ] Navigation implementation approach
- [ ] Platform-specific UX patterns

### MOBILE-PLATFORM-002: WebView Strategy

**Priority**: CRITICAL

Platform DESIGN MUST specify WebView:

- [ ] WebView container design
- [ ] JS bridge architecture
- [ ] Authentication token passing
- [ ] WebView → Native communication

### MOBILE-PLATFORM-003: Offline Architecture

**Priority**: HIGH

Platform DESIGN MUST address offline:

- [ ] Offline queue mechanism
- [ ] Cache management strategy
- [ ] Sync approach
- [ ] Network state handling

### MOBILE-PLATFORM-004: Push Notification Architecture

**Priority**: HIGH

Platform DESIGN MUST define:

- [ ] FCM (Android) integration
- [ ] APNS (iOS) integration
- [ ] Token registration flow
- [ ] Deep link from notification

### MOBILE-PLATFORM-005: Deep Link Architecture

**Priority**: HIGH

Platform DESIGN MUST specify:

- [ ] Deep link format (`constructor://{miniapp}/{path}`)
- [ ] Deep link routing mechanism
- [ ] Parameter handling

---

## Reporting

### Report Format

For each issue found, report:

```markdown
## Issue: {CHECKLIST-ID}

**Severity**: CRITICAL | HIGH | MEDIUM | LOW

**Why Applicable**: {Why this requirement applies to this Platform}

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
