# PRD — {Epic Name}

> **Level**: L2 (Epic)  
> **Parent MiniApp**: [{MiniApp Name} PRD](../../PRD.md) `cpt-{miniapp}-prd`  
> **Parent Platform**: [Platform PRD](../../../../architecture/PRD.md) `cpt-superapp-prd`  
> **Version**: 1.0  
> **Status**: Draft

---

## 1. Overview

### 1.1 Purpose

This PRD defines requirements for the **{Epic Name}** epic within the {MiniApp Name} MiniApp.

**Epic Type:** Screen | Capability | Flow | Widget

### 1.2 Scope

**In Scope:**
- {screen/feature 1}
- {screen/feature 2}

**Out of Scope:**
- {explicitly excluded}

### 1.3 Traces To Parent Requirements

| MiniApp Requirement | Relation | Description |
|-------------------|----------|-------------|
| `cpt-{miniapp}-fr-{slug}` | details | {How this Epic details MiniApp FR} |
| `cpt-{miniapp}-fr-{slug-2}` | details | {Another MiniApp FR this Epic covers} |

**Indirect Platform Trace:**
- `cpt-{miniapp}-fr-{slug}` → `cpt-superapp-fr-{platform-slug}`

---

## 2. Actors & Context

### 2.1 Primary Actors

| Actor ID | Role in this Epic |
|----------|------------------|
| `cpt-superapp-actor-student` | {Specific role in this epic} |

### 2.2 Entry Points

| Entry Point | Source | Trigger |
|-------------|--------|---------|
| Deep link | External | `constructor://student/{epic}` |
| Navigation | Tab bar | Tap on {icon} |
| Push notification | System | {notification type} |

---

## 3. Functional Requirements

### 3.1 Core Requirements

#### FR-01: {Requirement Name}

**ID**: `cpt-{miniapp}-epic-{epic}-fr-{slug}`

**Traces To:** `cpt-{miniapp}-fr-{parent-slug}` (details)

| Attribute | Value |
|-----------|-------|
| Priority | P1 |
| Actor | `cpt-superapp-actor-{actor}` |
| Description | {Specific behavior in this screen/flow} |
| UI Element | {Widget/component involved} |
| Acceptance | {Specific acceptance criteria} |

---

#### FR-02: {Epic-Specific Requirement}

**ID**: `cpt-{miniapp}-epic-{epic}-fr-{slug}`

**Tags**: `epic-specific`

**Traces To:** — (Epic-specific requirement)

| Attribute | Value |
|-----------|-------|
| Priority | P2 |
| Description | {Behavior specific to this Epic only} |
| Rationale | {Why this is needed at Epic level only} |

---

### 3.2 State Requirements

#### Screen States

**ID**: `cpt-{miniapp}-epic-{epic}-state`

| State | Condition | UI Behavior |
|-------|-----------|-------------|
| Loading | Initial load | Show skeleton |
| Content | Data loaded | Show main content |
| Empty | No data | Show empty state with CTA |
| Error | API failed | Show error with retry |
| Offline | No network | Show cached data with offline banner |

---

### 3.3 Error Handling

| Error Type | User Message | Recovery Action |
|------------|--------------|-----------------|
| Network timeout | "Check your connection" | Retry button |
| Invalid data | "Something went wrong" | Contact support link |
| Auth expired | "Session expired" | Redirect to login |

---

## 4. UI/UX Requirements

### 4.1 Screen Layout

```
┌────────────────────────────────┐
│ Navigation Bar                 │
├────────────────────────────────┤
│                                │
│ {Main Content Area}            │
│                                │
├────────────────────────────────┤
│ {Bottom Action Area}           │
└────────────────────────────────┘
```

### 4.2 Components

| Component | ID | Description |
|-----------|-----|-------------|
| {Widget Name} | `cpt-{miniapp}-{epic}-widget-{slug}` | {Purpose} |
| {Widget Name 2} | `cpt-{miniapp}-{epic}-widget-{slug-2}` | {Purpose} |

### 4.3 Interactions

| Interaction | Trigger | Result |
|-------------|---------|--------|
| Pull to refresh | Swipe down | Reload data |
| Tap item | Touch | Navigate to detail |
| Long press | Touch + hold | Show context menu |

---

## 5. Data Requirements

### 5.1 Required Data

| Data | Source | Caching |
|------|--------|---------|
| {Entity} | API: `GET /api/v1/{resource}` | 5 min TTL |
| {Entity 2} | Local DB | Persist |

### 5.2 API Contracts

| Endpoint | Method | Request | Response |
|----------|--------|---------|----------|
| `/api/v1/{resource}` | GET | `{ filters }` | `{ data[] }` |

---

## 6. Traceability Matrix

### 6.1 MiniApp FR → Epic FR Coverage

| MiniApp FR | Epic FRs | Coverage |
|-----------|---------|----------|
| `cpt-{miniapp}-fr-{slug-1}` | `cpt-{miniapp}-epic-{epic}-fr-{a}` | Full |
| `cpt-{miniapp}-fr-{slug-2}` | `cpt-{miniapp}-epic-{epic}-fr-{b}`, `cpt-{miniapp}-epic-{epic}-fr-{c}` | Full |

### 6.2 Epic FR → Feature Mapping

| Epic FR | Target Feature | Status |
|---------|---------------|--------|
| `cpt-{miniapp}-epic-{epic}-fr-{slug}` | `cpt-{miniapp}-feature-{feature}` | Planned |

### 6.3 Full Traceability Chain

```
Platform FR                    MiniApp FR                      Epic FR
─────────────                  ─────────                      ───────
cpt-superapp-fr-{slug}    →    cpt-{miniapp}-fr-{slug}    →    cpt-{miniapp}-epic-{epic}-fr-{slug}
     ↓                              ↓                              ↓
DESIGN-PLATFORM             DESIGN-MINIAPP               DESIGN-EPIC
     ↓                              ↓                              ↓
                                                           FEATURE
```

---

## 7. Acceptance Criteria

- [ ] All MiniApp FRs in scope are detailed
- [ ] All Epic FRs have feature specifications
- [ ] All states defined and designed
- [ ] All error scenarios handled
- [ ] Traceability chain verified

---

## Appendix: ID Reference

| ID Pattern | Example | Purpose |
|------------|---------|---------|
| `cpt-{miniapp}-epic-{epic}-prd` | `cpt-student-epic-home-prd` | Epic PRD anchor |
| `cpt-{miniapp}-epic-{epic}-fr-{slug}` | `cpt-student-epic-home-fr-streak` | Functional requirement |
| `cpt-{miniapp}-epic-{epic}-state` | `cpt-student-epic-home-state` | State machine |
| `cpt-{miniapp}-{epic}-widget-{slug}` | `cpt-student-home-widget-progress` | UI component |
