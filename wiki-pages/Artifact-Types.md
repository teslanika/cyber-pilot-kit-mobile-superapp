# Artifact Types

The Mobile SuperApp Kit provides 13 artifact types organized across 4 hierarchy levels.

## Summary Table

| Level | Artifact | Purpose | ID Pattern |
|-------|----------|---------|------------|
| **L0: Platform** | `PRD-PLATFORM` | Platform-wide requirements | `cpt-platform-fr-{slug}` |
| | `DESIGN-PLATFORM` | Platform architecture | `cpt-platform-component-{slug}` |
| | `DECOMPOSITION-PLATFORM` | MiniApp breakdown | `cpt-platform-miniapp-{slug}` |
| **L1: MiniApp** | `PRD-MINIAPP` | MiniApp requirements | `cpt-{miniapp}-fr-{slug}` |
| | `DESIGN-MINIAPP` | MiniApp architecture | `cpt-{miniapp}-component-{slug}` |
| | `DECOMPOSITION-MINIAPP` | Epic breakdown | `cpt-{miniapp}-epic-{slug}` |
| **L2: Epic** | `PRD-EPIC` | User stories | `cpt-{miniapp}-{epic}-story-{slug}` |
| | `DESIGN-EPIC` | Epic architecture | `cpt-{miniapp}-{epic}-component-{slug}` |
| | `DECOMPOSITION-EPIC` | Feature breakdown | `cpt-{miniapp}-{epic}-feature-{slug}` |
| **L3: Feature** | `FEATURE-MOBILE` | MVI feature design | `cpt-{miniapp}-flow-{feature}-{slug}` |
| | `IMPL-KMP` | KMP implementation | `@cpt-impl cpt-kmp-...` |
| | `IMPL-ANDROID` | Android implementation | `@cpt-impl cpt-android-...` |
| | `IMPL-IOS` | iOS implementation | `@cpt-impl cpt-ios-...` |

## Artifact Structure

Each artifact type includes three files:

```
artifacts/{ARTIFACT-TYPE}/
├── template.md    # Document structure
├── rules.md       # Generation and validation rules
└── checklist.md   # Review criteria
```

---

## PRD Artifacts

### PRD-PLATFORM

Platform-wide product requirements document.

**Contains:**
- Actors (Student, Instructor, Admin)
- Functional Requirements (FR)
- Non-Functional Requirements (NFR)
- Use Cases
- Constraints

**Example IDs:**
- `cpt-platform-actor-student`
- `cpt-platform-fr-offline-support`
- `cpt-platform-nfr-launch-time`

### PRD-MINIAPP

MiniApp-level requirements that refine platform requirements.

**Contains:**
- MiniApp-specific actors
- Domain requirements
- References to Platform FRs

**Example IDs:**
- `cpt-learn-fr-browse-courses`
- `cpt-learn-fr-offline-courses`

### PRD-EPIC

Epic-level user stories and acceptance criteria.

**Contains:**
- User stories
- Acceptance criteria
- References to MiniApp FRs

**Example IDs:**
- `cpt-learn-course-catalog-story-view-courses`
- `cpt-learn-course-catalog-ac-pagination`

---

## DESIGN Artifacts

### DESIGN-PLATFORM

Platform architecture defining shared infrastructure.

**Contains:**
- KMP module structure
- Shared components (Auth, Push, Navigation)
- Data architecture
- API contracts

**Example IDs:**
- `cpt-platform-component-auth-service`
- `cpt-platform-module-constructor-sdk`

### DESIGN-MINIAPP

MiniApp architecture within platform constraints.

**Contains:**
- ViewModels
- Repositories
- Navigation graph
- Data models

**Example IDs:**
- `cpt-learn-component-course-repository`
- `cpt-learn-viewmodel-course-list`

### DESIGN-EPIC

Epic-level component design.

**Contains:**
- Screen components
- Sequences
- State machines

**Example IDs:**
- `cpt-learn-course-catalog-component-list-screen`
- `cpt-learn-course-catalog-seq-load-courses`

---

## DECOMPOSITION Artifacts

### DECOMPOSITION-PLATFORM

Breaks platform into MiniApps.

**Contains:**
- MiniApp list with descriptions
- Dependencies between MiniApps
- Priority/order

### DECOMPOSITION-MINIAPP

Breaks MiniApp into Epics.

**Contains:**
- Epic list with descriptions
- Dependencies between Epics
- Implementation order

### DECOMPOSITION-EPIC

Breaks Epic into Features.

**Contains:**
- Feature list with descriptions
- Dependencies between Features
- Implementation order

---

## FEATURE-MOBILE

The core artifact for implementing mobile features.

**Contains:**
- MVI definitions (State, Intent, Effect)
- CDSL flows with instructions
- Algorithms
- State machines
- Platform-specific implementation sections (KMP, Android, iOS)
- Acceptance criteria per platform
- Definition of Done

See [MVI Pattern](MVI-Pattern) for details.

---

## IMPL Artifacts

Implementation tracking documents for each platform.

### IMPL-KMP

Tracks KMP shared code implementation.

### IMPL-ANDROID

Tracks Android/Compose implementation.

### IMPL-IOS

Tracks iOS/SwiftUI implementation.

See [Code Markers](Code-Markers) for traceability.
