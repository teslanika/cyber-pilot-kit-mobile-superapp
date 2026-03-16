# Mobile SuperApp Kit

> A [Cyber Pilot](https://github.com/cyberfabric/cyber-pilot) kit for mobile SuperApp development with multi-level documentation hierarchy and cascading requirement traceability.

## Installation

```bash
# Install (--version is optional, defaults to latest)
cpt kit install teslanika/cyber-pilot-kit-mobile-superapp

# Update
cpt kit update mobile-superapp

# Validate
cpt validate-kits .
```

## Overview

**Mobile SuperApp Kit** provides a 4-level documentation hierarchy designed specifically for large-scale mobile applications that combine multiple "mini-apps" (SubApps) into a single host application.

### Key Features

- **4-Level Documentation Hierarchy**: Platform → SubApp → Epic → Feature
- **Cascading Requirement Traceability**: Every requirement traces from high-level platform goals down to code
- **Mobile-Specific Templates**: KMP, Android (Compose), iOS (SwiftUI) implementation patterns
- **MVI State Management**: Consistent state management across all SubApps

### Documentation Hierarchy

```
L0: Platform PRD (architecture/PRD.md)
    └── Shared kernel: Auth, Push, Deep Links, SubApp Container, NFRs

L1: SubApp PRD (subapps/{subapp}/PRD.md)
    └── Domain requirements: Student, Proctor, Groups

L2: Epic PRD (subapps/{subapp}/capabilities/{epic}/PRD.md)
    └── Screen-level: Notification History, Course Catalog, etc.

L3: Feature (subapps/{subapp}/capabilities/{epic}/features/{feature}/FEATURE.md)
    └── CDSL specifications with platform-specific implementation
```

### Traceability Chain

```
Platform FR: cpt-superapp-fr-inapp-notifications
    │ refined-by
    ▼
SubApp FR: cpt-student-fr-notifications
    │ detailed-by
    ▼
Epic FR: cpt-student-epic-notification-history-fr-badge
    │ specified-by
    ▼
Feature: cpt-student-feature-notification-badge
    │ implemented-by
    ▼
Code: @cpt-impl:cpt-student-feature-notification-badge
```

## What the Kit Provides

| Category | Artifacts |
|----------|-----------|
| **PRD** | PRD-SUBAPP, PRD-EPIC |
| **DESIGN** | DESIGN-PLATFORM, DESIGN-SUBAPP, DESIGN-EPIC |
| **DECOMPOSITION** | DECOMPOSITION-PLATFORM, DECOMPOSITION-SUBAPP, DECOMPOSITION-EPIC |
| **FEATURE** | FEATURE-MOBILE (with CDSL flows) |
| **IMPL** | IMPL-KMP, IMPL-ANDROID, IMPL-IOS |

Each artifact type includes:
- `template.md` — Document structure
- `rules.md` — Generation and validation rules
- `checklist.md` — Review criteria

## Quick Start

### 1. Create Platform PRD

```bash
# Use standard SDLC PRD for platform level
cypilot generate PRD --path architecture/PRD.md
```

### 2. Create Platform DESIGN

```bash
cypilot generate DESIGN-PLATFORM --path architecture/DESIGN.md
```

### 3. Create SubApp

```bash
# PRD for SubApp
cypilot generate PRD-SUBAPP --path subapps/student/PRD.md

# DESIGN for SubApp
cypilot generate DESIGN-SUBAPP --path subapps/student/DESIGN.md
```

### 4. Create Epic

```bash
# PRD for Epic
cypilot generate PRD-EPIC --path subapps/student/capabilities/notification-history/PRD.md

# DESIGN for Epic
cypilot generate DESIGN-EPIC --path subapps/student/capabilities/notification-history/DESIGN.md
```

### 5. Create Feature

```bash
cypilot generate FEATURE-MOBILE --path subapps/student/capabilities/notification-history/features/badge/FEATURE.md
```

## Project Structure

```
my-superapp/
├── architecture/
│   ├── PRD.md                    # Platform PRD (L0)
│   ├── DESIGN.md                 # Platform DESIGN
│   └── DECOMPOSITION.md          # Platform → SubApps
│
└── subapps/
    └── student/
        ├── PRD.md                # SubApp PRD (L1)
        ├── DESIGN.md             # SubApp DESIGN
        ├── DECOMPOSITION.md      # SubApp → Epics
        │
        └── capabilities/
            └── notification-history/
                ├── PRD.md        # Epic PRD (L2)
                ├── DESIGN.md     # Epic DESIGN
                ├── DECOMPOSITION.md
                │
                └── features/
                    └── badge/
                        └── FEATURE.md  # Feature (L3)
```

## ID Naming Conventions

| Level | Pattern | Example |
|-------|---------|---------|
| Platform FR | `cpt-{platform}-fr-{slug}` | `cpt-superapp-fr-offline` |
| Platform Component | `cpt-{platform}-component-{slug}` | `cpt-superapp-component-auth` |
| SubApp FR | `cpt-{subapp}-fr-{slug}` | `cpt-student-fr-courses` |
| SubApp Epic | `cpt-{subapp}-epic-{slug}` | `cpt-student-epic-home` |
| Epic FR | `cpt-{subapp}-epic-{epic}-fr-{slug}` | `cpt-student-epic-home-fr-streak` |
| Feature | `cpt-{subapp}-feature-{slug}` | `cpt-student-feature-daily-goal` |
| KMP Impl | `cpt-kmp-{module}-{type}-{slug}` | `cpt-kmp-home-usecase-load` |
| Android Impl | `cpt-android-{module}-{type}-{slug}` | `cpt-android-home-screen-main` |
| iOS Impl | `cpt-ios-{module}-{type}-{slug}` | `cpt-ios-home-view-main` |

## Validation

```bash
# Validate single artifact
cypilot validate --artifact subapps/student/PRD.md

# Validate FR traceability cascade
cypilot validate --check=fr-cascade

# Check Platform FR → SubApp FR coverage
cypilot validate --check=platform-fr-coverage

# Check Feature implementation coverage
cypilot validate --check=feature-impl-coverage
```

## Technology Stack (Target)

| Layer | Technology |
|-------|------------|
| **KMP Shared** | Kotlin Multiplatform, Ktor, SQLDelight |
| **Android UI** | Jetpack Compose, Hilt, Navigation Compose |
| **iOS UI** | SwiftUI, Combine, Swift Concurrency |
| **State Management** | MVI (Model-View-Intent) |
| **Architecture** | Clean Architecture, Modular |

## References

- [Cyber Pilot](https://github.com/cyberfabric/cyber-pilot) — Core framework
- [SDLC Kit](https://github.com/cyberfabric/cyber-pilot-kit-sdlc) — Base SDLC artifacts

## License

MIT License — see [LICENSE](LICENSE)
