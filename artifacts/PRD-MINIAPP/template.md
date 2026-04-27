# PRD — {MiniApp Name} MiniApp

> **Level**: L1 (MiniApp)  
> **Parent**: [Platform PRD](../../architecture/PRD.md) `cpt-superapp-prd`  
> **Version**: 1.0  
> **Status**: Draft

---

## 1. Overview

### 1.1 Purpose

This PRD defines requirements for the **{MiniApp Name}** MiniApp within the Constructor Mobile SuperApp.

### 1.2 Scope

**In Scope:**
- {capability 1}
- {capability 2}

**Out of Scope:**
- {explicitly excluded capability}

### 1.3 Traces To Platform

| Platform Requirement | Relation | Description |
|---------------------|----------|-------------|
| `cpt-superapp-fr-{slug}` | refines | {How this MiniApp refines Platform FR} |
| `cpt-superapp-nfr-{slug}` | inherits | {Which Platform NFRs apply} |

---

## 2. Actors

### 2.1 Primary Actors

| Actor ID | Role | MiniApp-Specific Context |
|----------|------|------------------------|
| `cpt-superapp-actor-student` | Primary | {How student uses this MiniApp} |
| `cpt-superapp-actor-instructor` | Secondary | {How instructor uses this MiniApp} |

---

## 3. Functional Requirements

### 3.1 Core Capabilities

#### FR-01: {Feature Name}

**ID**: `cpt-{miniapp}-fr-{slug}`

**Traces To:** `cpt-superapp-fr-{parent-slug}` (refines)

| Attribute | Value |
|-----------|-------|
| Priority | P1 |
| Actor | `cpt-superapp-actor-{actor}` |
| Description | {What the system must do} |
| Acceptance | {Measurable acceptance criteria} |

---

#### FR-02: {MiniApp-Specific Feature}

**ID**: `cpt-{miniapp}-fr-{slug}`

**Tags**: `miniapp-specific`

**Traces To:** — (MiniApp-specific requirement)

| Attribute | Value |
|-----------|-------|
| Priority | P2 |
| Actor | `cpt-superapp-actor-{actor}` |
| Description | {MiniApp-specific capability not from Platform} |
| Rationale | {Why this is needed at MiniApp level only} |

---

### 3.2 MiniApp-Level NFRs

#### NFR-01: {Quality Attribute}

**ID**: `cpt-{miniapp}-nfr-{slug}`

**Traces To:** `cpt-superapp-nfr-{parent-slug}` (extends)

| Attribute | Value |
|-----------|-------|
| Category | Performance / Security / Usability |
| Metric | {Measurable metric} |
| Target | {Specific target value} |
| Rationale | {Why MiniApp needs stricter/different requirement} |

---

## 4. Use Cases

### UC-01: {Use Case Name}

**ID**: `cpt-{miniapp}-usecase-{slug}`

**Traces To:** `cpt-{miniapp}-fr-{slug}`

| Attribute | Value |
|-----------|-------|
| Primary Actor | `cpt-superapp-actor-{actor}` |
| Precondition | {Starting state} |
| Main Flow | 1. {Step 1}<br/>2. {Step 2}<br/>3. {Step 3} |
| Postcondition | {End state} |
| Exceptions | {Error scenarios} |

---

## 5. Dependencies

### 5.1 Platform Dependencies

| Dependency | Type | Description |
|------------|------|-------------|
| Auth Kernel | Required | `cpt-superapp-component-auth-kernel` |
| Storage Kernel | Required | `cpt-superapp-component-storage-kernel` |

### 5.2 External Dependencies

| System | Integration Type | Description |
|--------|-----------------|-------------|
| {Backend Service} | API | {What data/operations} |

---

## 6. Traceability Matrix

### 6.1 Platform FR → MiniApp FR Coverage

| Platform FR | MiniApp FRs | Coverage Status |
|-------------|-----------|-----------------|
| `cpt-superapp-fr-{slug-1}` | `cpt-{miniapp}-fr-{a}`, `cpt-{miniapp}-fr-{b}` | Full |
| `cpt-superapp-fr-{slug-2}` | `cpt-{miniapp}-fr-{c}` | Partial |
| `cpt-superapp-fr-{slug-3}` | — | Not in scope |

### 6.2 MiniApp FR → Epic Coverage

| MiniApp FR | Target Epics | Status |
|-----------|--------------|--------|
| `cpt-{miniapp}-fr-{slug}` | Home, Settings | Planned |

---

## 7. Acceptance Criteria

- [ ] All Platform FRs in scope are refined
- [ ] All MiniApp FRs have epic-level detailing
- [ ] All use cases have corresponding features
- [ ] Traceability matrix complete

---

## Appendix: ID Reference

| ID Pattern | Example | Purpose |
|------------|---------|---------|
| `cpt-{miniapp}-prd` | `cpt-student-prd` | MiniApp PRD anchor |
| `cpt-{miniapp}-fr-{slug}` | `cpt-student-fr-course-list` | Functional requirement |
| `cpt-{miniapp}-nfr-{slug}` | `cpt-student-nfr-offline` | Non-functional requirement |
| `cpt-{miniapp}-usecase-{slug}` | `cpt-student-usecase-browse` | Use case |
