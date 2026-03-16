---
name: mobile-superapp
description: "Mobile SuperApp documentation kit with 4-level hierarchy: Platform → SubApp → Epic → Feature, with cascading requirement traceability"
---

# Cypilot Skill — Kit `mobile-superapp`

## Overview

This kit provides specialized templates for mobile SuperApp development with:
- **4-Level PRD hierarchy** (Platform → SubApp → Epic → Feature)
- **Level-specific DESIGN templates** (Platform, SubApp, Epic)
- **Cascading DECOMPOSITION** (Platform → SubApps, SubApp → Epics, Epic → Features)
- **Mobile-specific FEATURE template** with KMP/Android/iOS sections
- **Platform-specific IMPL templates** (KMP, Android, iOS)

## Artifact Types

### PRD-SUBAPP
SubApp-level PRD that refines Platform requirements.

**Use when**: Creating requirements for a self-contained feature module (e.g., Student SubApp, Proctor SubApp).

**Contains**:
- Traces to Platform PRD
- SubApp-specific functional requirements
- SubApp-level NFRs (extending Platform NFRs)
- Use cases
- Platform dependencies

### PRD-EPIC
Epic-level PRD that details SubApp requirements for a specific screen/flow/capability.

**Use when**: Creating requirements for a screen, user flow, or cross-cutting capability.

**Contains**:
- Traces to SubApp PRD
- Screen states and error handling
- UI/UX requirements
- Data requirements
- API contracts

### DESIGN-PLATFORM
Platform-level architecture design for the entire SuperApp.

**Use when**: Defining overall platform architecture, shared kernel, SubApp container model.

**Contains**:
- Platform layers (Presentation, Application, Domain, Infrastructure)
- Cross-platform strategy (Native vs WebView)
- KMP SDK scope
- SubApp container model
- Shared kernel components (Auth, Storage, Network, Notifications)
- External integrations

### DESIGN-SUBAPP
SubApp-level architecture design.

**Use when**: Designing a specific SubApp's module structure and internal architecture.

**Contains**:
- Module structure (KMP, Android, iOS)
- Navigation architecture
- State management (MVI)
- Domain model
- API layer
- Kernel integration

### DESIGN-EPIC
Epic-level (screen/flow/capability) technical design.

**Use when**: Designing a specific screen or feature within a SubApp.

**Contains**:
- Component architecture
- Screen/widget components
- State management
- Data flow (UseCase, Repository)
- Platform-specific considerations
- Error handling

### DECOMPOSITION-PLATFORM
Decomposes Platform DESIGN into SubApps.

**Use when**: Breaking down the platform into deployable SubApp modules.

### DECOMPOSITION-SUBAPP
Decomposes SubApp DESIGN into Epics (screens, capabilities, flows).

**Use when**: Breaking down a SubApp into implementable epics.

### DECOMPOSITION-EPIC
Decomposes Epic DESIGN into Features.

**Use when**: Breaking down an epic into discrete, implementable features.

### FEATURE-MOBILE
Mobile-specific feature design with CDSL flows.

**Use when**: Specifying a discrete piece of functionality ready for implementation.

**Contains**:
- Actor flows (CDSL)
- Platform implementation sections (KMP, Android, iOS, WebView)
- State machines (CDSL)
- Definitions of Done
- Platform-specific acceptance criteria

### IMPL-KMP / IMPL-ANDROID / IMPL-IOS
Implementation reference documents linking code to product docs.

**Use when**: Creating traceability from code back to documentation.

## Commands

### Validation
```bash
cypilot validate --artifact <path>
cypilot validate --check=fr-cascade
cypilot validate --check=platform-fr-coverage
cypilot validate --check=feature-impl-coverage
```

### ID Operations
```bash
cypilot list-ids --kind feature
cypilot where-defined --id <id>
cypilot where-used --id <id>
```

## Workflows

### Generate Platform Architecture
1. Create/update `architecture/PRD.md` (use SDLC PRD)
2. Create `architecture/DESIGN.md` using DESIGN-PLATFORM template
3. Create `architecture/DECOMPOSITION.md` listing SubApps
4. Create `architecture/adr/` for platform decisions

### Generate SubApp
1. Create `subapps/{subapp}/PRD.md` using PRD-SUBAPP template
2. Create `subapps/{subapp}/DESIGN.md` using DESIGN-SUBAPP template
3. Create `subapps/{subapp}/DECOMPOSITION.md` listing Epics
4. Create epics in `screens/`, `capabilities/`, `flows/`

### Generate Epic
1. Create `subapps/{subapp}/{category}/{epic}/PRD.md` using PRD-EPIC template
2. Create `DESIGN.md` using DESIGN-EPIC template
3. Create `DECOMPOSITION.md` listing Features
4. Create features in `features/`

### Generate Feature
1. Create `features/{feature}/FEATURE.md` using FEATURE-MOBILE template
2. Create IMPL.md files in code folders:
   - `constructor-sdk/feature/{module}/IMPL.md`
   - `android-app/feature/{module}/IMPL.md`
   - `ios-app/Features/{Module}/IMPL.md`

## Level Detection

| Path Pattern | Level |
|--------------|-------|
| `architecture/` | L0: Platform |
| `subapps/{subapp}/` (direct children) | L1: SubApp |
| `subapps/{subapp}/screens/{screen}/` | L2: Epic (screen) |
| `subapps/{subapp}/capabilities/{capability}/` | L2: Epic (capability) |
| `subapps/{subapp}/flows/{flow}/` | L2: Epic (flow) |
| `subapps/{subapp}/*/{epic}/features/{feature}/` | L3: Feature |

## Traceability Chain

```
Platform PRD
    ↓ refined-by
Platform DESIGN + ADR
    ↓ decomposed-by
Platform DECOMPOSITION (SubApps)
    ↓ detailed-by
SubApp PRD
    ↓ designed-by
SubApp DESIGN + ADR
    ↓ decomposed-by
SubApp DECOMPOSITION (Epics)
    ↓ detailed-by
Epic PRD
    ↓ designed-by
Epic DESIGN + ADR
    ↓ decomposed-by
Epic DECOMPOSITION (Features)
    ↓ specified-by
FEATURE (CDSL)
    ↓ implemented-by
IMPL-KMP + IMPL-ANDROID + IMPL-IOS
    ↓ traces-to
Code (@cpt-impl markers)
```
