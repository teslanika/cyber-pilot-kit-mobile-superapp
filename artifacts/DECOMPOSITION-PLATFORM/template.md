# Decomposition: {Platform Name}

## Table of Contents

<!-- toc -->

<!-- /toc -->

## 1. Overview

This document decomposes the Platform DESIGN into MiniApps. Each MiniApp is a self-contained module within the SuperApp that can be developed, deployed, and activated independently.

**Parent Documents:**
- PRD: [PRD.md](./PRD.md)
- DESIGN: [DESIGN.md](./DESIGN.md)

## 2. MiniApp Entries

**Overall implementation status:**

- [ ] `p1` - **ID**: `cpt-{platform}-status-overall`

---

### 2.1 [{MiniApp Name 1}](miniapps/{miniapp1}/) - HIGH

- [ ] `p1` - **ID**: `cpt-{platform}-miniapp-{miniapp1}`

- **Purpose**: {Few sentences describing what this MiniApp provides and why it exists}

- **Target Users**: `cpt-{platform}-actor-{slug}`

- **Depends On**: Kernel (Auth, Storage, Network)

- **Scope**:
  - {in-scope capability 1}
  - {in-scope capability 2}

- **Out of scope**:
  - {out-of-scope item 1}

- **Requirements Covered**:
  - [ ] `p1` - `cpt-{platform}-fr-{slug}` — {requirement summary}
  - [ ] `p1` - `cpt-{platform}-fr-{slug}` — {requirement summary}

- **Platform Components**:
  - [ ] `p1` - `cpt-{platform}-component-{slug}` — {component from Platform DESIGN}

- **Integration Points**:
  - `cpt-{platform}-integration-{slug}` — {external integration}

- **Target Release**: Q{X} 202{Y}

---

### 2.2 [{MiniApp Name 2}](miniapps/{miniapp2}/) - MEDIUM

- [ ] `p2` - **ID**: `cpt-{platform}-miniapp-{miniapp2}`

- **Purpose**: {Few sentences describing what this MiniApp provides}

- **Target Users**: `cpt-{platform}-actor-{slug}`

- **Depends On**: 
  - Kernel (Auth, Storage, Network)
  - `cpt-{platform}-miniapp-{miniapp1}` (if dependent on another MiniApp)

- **Scope**:
  - {in-scope capability 1}

- **Out of scope**:
  - {out-of-scope item 1}

- **Requirements Covered**:
  - [ ] `p2` - `cpt-{platform}-fr-{slug}` — {requirement summary}

- **Platform Components**:
  - [ ] `p2` - `cpt-{platform}-component-{slug}` — {component from Platform DESIGN}

- **Integration Points**:
  - `cpt-{platform}-integration-{slug}` — {external integration}

- **Target Release**: Q{X} 202{Y}

---

### 2.3 [{MiniApp Name 3}](miniapps/{miniapp3}/) - LOW

- [ ] `p3` - **ID**: `cpt-{platform}-miniapp-{miniapp3}`

- **Purpose**: {Few sentences describing what this MiniApp provides}

- **Target Users**: `cpt-{platform}-actor-{slug}`

- **Depends On**: Kernel

- **Scope**:
  - {in-scope capability}

- **Out of scope**:
  - {out-of-scope item}

- **Requirements Covered**:
  - [ ] `p3` - `cpt-{platform}-fr-{slug}` — {requirement summary}

- **Platform Components**:
  - [ ] `p3` - `cpt-{platform}-component-{slug}` — {component from Platform DESIGN}

- **Target Release**: Q{X} 202{Y}

---

## 3. Shared Kernel Components

Components from Platform DESIGN that are shared across all MiniApps:

| Component ID | Component | MiniApps Using |
|--------------|-----------|---------------|
| `cpt-{platform}-component-auth-kernel` | Authentication Module | All |
| `cpt-{platform}-component-storage-kernel` | Storage Module | All |
| `cpt-{platform}-component-network-kernel` | Networking Module | All |
| `cpt-{platform}-component-notifications-kernel` | Notifications Module | Student, Proctor |

## 4. MiniApp Dependencies

```text
Kernel (Auth, Storage, Network, Notifications)
    │
    ├─→ cpt-{platform}-miniapp-student (independent)
    │
    ├─→ cpt-{platform}-miniapp-proctor (independent)
    │       │
    │       └─→ uses: Student MiniApp deep links for exam navigation
    │
    └─→ cpt-{platform}-miniapp-groups (independent)
```

**Dependency Rationale**:

- All MiniApps depend on **Kernel** for shared services (auth, storage, network)
- MiniApps are **loosely coupled** — communicate via deep links and events, not direct calls
- **Proctor → Student**: Proctor needs to navigate to exam content in Student MiniApp

## 5. Release Roadmap

| Quarter | MiniApps | Milestone |
|---------|---------|-----------|
| Q1 2026 | Student (MVP) | Core learning experience |
| Q2 2026 | Proctor, Groups (WebView) | Full proctoring, video calls |
| Q3 2026 | Groups (Native), Practice | Native video, virtual labs |
| Q4 2026 | Role-based features | Instructor, Admin capabilities |
