# Decomposition: {MiniApp Name} MiniApp

## Table of Contents

<!-- toc -->

<!-- /toc -->

## 1. Overview

This document decomposes the {MiniApp} MiniApp DESIGN into Epics. Each Epic represents a screen, capability, or user flow that can be developed and tested independently.

**Parent Documents:**
- MiniApp PRD: [PRD.md](./PRD.md)
- MiniApp DESIGN: [DESIGN.md](./DESIGN.md)
- Platform DECOMPOSITION: [../DECOMPOSITION.md](../DECOMPOSITION.md)

## 2. Epic Entries

**Overall implementation status:**

- [ ] `p1` - **ID**: `cpt-{miniapp}-status-overall`

---

### 2.1 Screens

#### [{Screen Name 1}](screens/{screen1}/) - HIGH

- [ ] `p1` - **ID**: `cpt-{miniapp}-epic-{screen1}`

- **Category**: Screen

- **Purpose**: {Few sentences describing what this screen provides and why it matters}

- **Actors**: `cpt-{platform}-actor-{slug}`

- **Depends On**: None (entry point) / `cpt-{miniapp}-epic-{slug}` (if dependent)

- **Scope**:
  - {widget/feature 1}
  - {widget/feature 2}

- **Out of scope**:
  - {out-of-scope item}

- **Requirements Covered**:
  - [ ] `p1` - `cpt-{miniapp}-fr-{slug}` — {requirement summary}

- **Design Components**:
  - [ ] `p1` - `cpt-{miniapp}-component-{slug}` — {component from MiniApp DESIGN}

- **KMP Modules**:
  - `cpt-{miniapp}-component-kmp-{slug}`

- **Target Release**: Q{X} 202{Y}

---

#### [{Screen Name 2}](screens/{screen2}/) - MEDIUM

- [ ] `p2` - **ID**: `cpt-{miniapp}-epic-{screen2}`

- **Category**: Screen

- **Purpose**: {Description}

- **Actors**: `cpt-{platform}-actor-{slug}`

- **Depends On**: `cpt-{miniapp}-epic-{screen1}`

- **Scope**:
  - {scope item}

- **Out of scope**:
  - {out-of-scope item}

- **Requirements Covered**:
  - [ ] `p2` - `cpt-{miniapp}-fr-{slug}` — {requirement summary}

- **Design Components**:
  - [ ] `p2` - `cpt-{miniapp}-component-{slug}` — {component}

---

### 2.2 Capabilities

#### [{Capability Name}](capabilities/{capability}/) - HIGH

- [ ] `p1` - **ID**: `cpt-{miniapp}-epic-{capability}`

- **Category**: Capability (cross-cutting)

- **Purpose**: {Few sentences describing this cross-cutting capability}

- **Actors**: `cpt-{platform}-actor-{slug}`

- **Depends On**: Kernel services

- **Scope**:
  - {capability scope 1}
  - {capability scope 2}

- **Out of scope**:
  - {out-of-scope item}

- **Requirements Covered**:
  - [ ] `p1` - `cpt-{miniapp}-fr-{slug}` — {requirement}
  - [ ] `p1` - `cpt-{miniapp}-nfr-{slug}` — {NFR if applicable}

- **Design Components**:
  - [ ] `p1` - `cpt-{miniapp}-component-{slug}` — {component}

- **Kernel Integration**:
  - `cpt-{platform}-component-{kernel-slug}` — {how it uses kernel}

---

### 2.3 Flows

#### [{Flow Name}](flows/{flow}/) - MEDIUM

- [ ] `p2` - **ID**: `cpt-{miniapp}-epic-{flow}`

- **Category**: Flow (multi-screen journey)

- **Purpose**: {Few sentences describing this user flow}

- **Actors**: `cpt-{platform}-actor-{slug}`

- **Depends On**: 
  - `cpt-{miniapp}-epic-{screen1}` — starting point
  - `cpt-{miniapp}-epic-{screen2}` — intermediate step

- **Screens Involved**:
  - {Screen 1} → {Screen 2} → {Screen 3}

- **Scope**:
  - {flow scope}

- **Out of scope**:
  - {out-of-scope}

- **Requirements Covered**:
  - [ ] `p2` - `cpt-{miniapp}-fr-{slug}` — {requirement}

- **Design Sequences**:
  - [ ] `p2` - `cpt-{miniapp}-seq-{slug}` — {sequence from DESIGN}

---

## 3. Epic Dependencies

```text
cpt-{miniapp}-epic-{foundation}
    │
    ├─→ cpt-{miniapp}-epic-{dependent1}
    │       │
    │       └─→ cpt-{miniapp}-epic-{sub-dependent}
    │
    └─→ cpt-{miniapp}-epic-{dependent2}

cpt-{miniapp}-epic-{capability} (cross-cutting, used by multiple screens)
```

**Dependency Rationale**:

- `cpt-{miniapp}-epic-{dependent1}` requires `cpt-{miniapp}-epic-{foundation}`: {explain why}
- `cpt-{miniapp}-epic-{capability}` is used across screens: {list screens}

## 4. Coverage Matrix

### 4.1 Requirements Coverage

| Requirement ID | Epic | Status |
|----------------|------|--------|
| `cpt-{miniapp}-fr-{slug1}` | `cpt-{miniapp}-epic-{epic1}` | ☐ |
| `cpt-{miniapp}-fr-{slug2}` | `cpt-{miniapp}-epic-{epic2}` | ☐ |

### 4.2 Design Component Coverage

| Component ID | Epic | Status |
|--------------|------|--------|
| `cpt-{miniapp}-component-{slug1}` | `cpt-{miniapp}-epic-{epic1}` | ☐ |
| `cpt-{miniapp}-component-{slug2}` | `cpt-{miniapp}-epic-{epic2}` | ☐ |

## 5. Implementation Order

| Phase | Epics | Rationale |
|-------|-------|-----------|
| 1 | `cpt-{miniapp}-epic-{foundation}` | Foundation, no dependencies |
| 2 | `cpt-{miniapp}-epic-{capability}` | Cross-cutting, enables other epics |
| 3 | `cpt-{miniapp}-epic-{dependent1}`, `cpt-{miniapp}-epic-{dependent2}` | Can be parallel |
| 4 | `cpt-{miniapp}-epic-{flow}` | Requires screens to be ready |
