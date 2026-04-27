# Decomposition: {Epic Name}

## Table of Contents

<!-- toc -->

<!-- /toc -->

## 1. Overview

This document decomposes the {Epic} DESIGN into Features. Each Feature is a discrete piece of functionality that can be implemented, tested, and delivered independently.

**Parent Documents:**
- Epic PRD: [PRD.md](./PRD.md)
- Epic DESIGN: [DESIGN.md](./DESIGN.md)
- MiniApp DECOMPOSITION: [../DECOMPOSITION.md](../DECOMPOSITION.md)

## 2. Feature Entries

**Overall implementation status:**

- [ ] `p1` - **ID**: `cpt-{miniapp}-{epic}-status-overall`

---

### 2.1 [{Feature Name 1}](features/{feature1}/) - HIGH

- [ ] `p1` - **ID**: `cpt-{miniapp}-feature-{feature1}`

- **Purpose**: {Few sentences describing what this feature accomplishes and why it matters}

- **Depends On**: None

- **Scope**:
  - {in-scope item 1}
  - {in-scope item 2}

- **Out of scope**:
  - {out-of-scope item}

- **Requirements Covered**:
  - [ ] `p1` - `cpt-{miniapp}-epic-{epic}-fr-{slug}` — {requirement summary}

- **Design Components**:
  - [ ] `p1` - `cpt-{miniapp}-{epic}-component-{slug}` — {component from Epic DESIGN}

- **Screen/Widget**:
  - [ ] `p1` - `cpt-{miniapp}-{epic}-screen-{slug}` — {screen component}
  - [ ] `p1` - `cpt-{miniapp}-{epic}-widget-{slug}` — {widget component}

- **Use Cases**:
  - [ ] `p1` - `cpt-{miniapp}-{epic}-usecase-{slug}` — {use case}

- **API Endpoints**:
  - `GET /api/v1/mobile/{miniapp}/{resource}`
  - `POST /api/v1/mobile/{miniapp}/{resource}`

- **Platform Implementation**:

| Platform | Module | Location |
|----------|--------|----------|
| KMP | `{Feature}ViewModel`, `{Feature}UseCase` | `constructor-sdk/feature/{miniapp}/` |
| Android | `{Feature}Screen` | `android-app/feature/{miniapp}/ui/` |
| iOS | `{Feature}View` | `ios-app/Features/{MiniApp}/Views/` |

---

### 2.2 [{Feature Name 2}](features/{feature2}/) - MEDIUM

- [ ] `p2` - **ID**: `cpt-{miniapp}-feature-{feature2}`

- **Purpose**: {Description}

- **Depends On**: `cpt-{miniapp}-feature-{feature1}`

- **Scope**:
  - {scope item}

- **Out of scope**:
  - {out-of-scope}

- **Requirements Covered**:
  - [ ] `p2` - `cpt-{miniapp}-epic-{epic}-fr-{slug}` — {requirement}

- **Design Components**:
  - [ ] `p2` - `cpt-{miniapp}-{epic}-component-{slug}` — {component}

- **State Management**:
  - [ ] `p2` - `cpt-{miniapp}-{epic}-state` — {state from DESIGN}

- **Platform Implementation**:

| Platform | Module | Location |
|----------|--------|----------|
| KMP | `{Module}` | `constructor-sdk/feature/{miniapp}/` |
| Android | `{Component}` | `android-app/feature/{miniapp}/` |
| iOS | `{Component}` | `ios-app/Features/{MiniApp}/` |

---

### 2.3 [{Feature Name 3}](features/{feature3}/) - LOW

- [ ] `p3` - **ID**: `cpt-{miniapp}-feature-{feature3}`

- **Purpose**: {Description}

- **Depends On**: `cpt-{miniapp}-feature-{feature1}`, `cpt-{miniapp}-feature-{feature2}`

- **Scope**:
  - {scope item}

- **Out of scope**:
  - {out-of-scope}

- **Requirements Covered**:
  - [ ] `p3` - `cpt-{miniapp}-epic-{epic}-fr-{slug}` — {requirement}

- **Design Components**:
  - [ ] `p3` - `cpt-{miniapp}-{epic}-component-{slug}` — {component}

---

## 3. Feature Dependencies

```text
cpt-{miniapp}-feature-{feature1}
    │
    ├─→ cpt-{miniapp}-feature-{feature2}
    │       │
    │       └─→ cpt-{miniapp}-feature-{feature3}
    │
    └─→ cpt-{miniapp}-feature-{feature4}
```

**Dependency Rationale**:

- `cpt-{miniapp}-feature-{feature2}` requires `cpt-{miniapp}-feature-{feature1}`: {explain why}
- `cpt-{miniapp}-feature-{feature3}` requires both: {explain why}

## 4. Coverage Matrix

### 4.1 Requirements → Features

| Requirement ID | Feature | Priority | Status |
|----------------|---------|----------|--------|
| `cpt-{miniapp}-epic-{epic}-fr-{slug1}` | `cpt-{miniapp}-feature-{feature1}` | p1 | ☐ |
| `cpt-{miniapp}-epic-{epic}-fr-{slug2}` | `cpt-{miniapp}-feature-{feature2}` | p2 | ☐ |

### 4.2 Design Components → Features

| Component ID | Feature | Status |
|--------------|---------|--------|
| `cpt-{miniapp}-{epic}-screen-{slug}` | `cpt-{miniapp}-feature-{feature1}` | ☐ |
| `cpt-{miniapp}-{epic}-widget-{slug}` | `cpt-{miniapp}-feature-{feature2}` | ☐ |
| `cpt-{miniapp}-{epic}-usecase-{slug}` | `cpt-{miniapp}-feature-{feature1}` | ☐ |

### 4.3 Platform Implementation Matrix

| Feature | KMP | Android | iOS |
|---------|-----|---------|-----|
| `cpt-{miniapp}-feature-{feature1}` | ☐ | ☐ | ☐ |
| `cpt-{miniapp}-feature-{feature2}` | ☐ | ☐ | ☐ |
| `cpt-{miniapp}-feature-{feature3}` | ☐ | ☐ | ☐ |

## 5. Implementation Order

| Phase | Features | Rationale |
|-------|----------|-----------|
| 1 | `cpt-{miniapp}-feature-{feature1}` | Foundation, no dependencies |
| 2 | `cpt-{miniapp}-feature-{feature2}` | Depends on phase 1 |
| 3 | `cpt-{miniapp}-feature-{feature3}`, `cpt-{miniapp}-feature-{feature4}` | Can be parallel after phase 2 |

## 6. Acceptance Criteria Summary

| Feature | Key Acceptance Criteria |
|---------|------------------------|
| `cpt-{miniapp}-feature-{feature1}` | {1-2 key criteria} |
| `cpt-{miniapp}-feature-{feature2}` | {1-2 key criteria} |
