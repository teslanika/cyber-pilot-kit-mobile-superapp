# Traceability

Cascading FR traceability ensures every requirement flows from platform to code.

## The Problem

In mobile development, requirements often get "lost":

```
Product Manager: "The app should work offline"
Developer: "Which screens? What data? How fresh?"
```

## The Solution

**Cascading FR traceability** requires explicit links at each level:

```
Platform FR: cpt-platform-fr-offline-support
    ↓ "refined by"
SubApp FR: cpt-learn-fr-offline-courses
    ↓ "detailed by"
Epic Story: cpt-learn-course-catalog-story-cache-courses
    ↓ "specified by"
Feature Flow: cpt-learn-flow-course-list-load-cached
    ↓ "implemented by"
Code: @cpt-flow:cpt-learn-flow-course-list-load-cached:p1
```

## Benefits

| Benefit | Description |
|---------|-------------|
| **Impact Analysis** | Change platform FR → see all affected SubApps/Features |
| **Coverage Check** | Ensure every platform requirement reaches code |
| **Audit Trail** | For compliance and security reviews |
| **Gap Detection** | Find requirements without implementation |

## How to Link

### In PRD-SUBAPP

Reference Platform FRs:

```markdown
## Traceability

### Platform Requirements
| Platform FR | SubApp FR |
|-------------|-----------|
| `cpt-platform-fr-offline-support` | `cpt-learn-fr-offline-courses` |
| `cpt-platform-fr-push-notifications` | `cpt-learn-fr-course-reminders` |
```

### In PRD-EPIC

Reference SubApp FRs:

```markdown
## Traceability

### SubApp Requirements
| SubApp FR | Epic Story |
|-----------|------------|
| `cpt-learn-fr-offline-courses` | `cpt-learn-course-catalog-story-cache-courses` |
```

### In FEATURE-MOBILE

Reference Epic and higher levels:

```markdown
## Traceability

### Cascading Requirements
| Level | ID | Description |
|-------|-----|-------------|
| Platform FR | `cpt-platform-fr-offline-support` | App works offline |
| SubApp FR | `cpt-learn-fr-offline-courses` | Cached courses available |
| Epic Story | `cpt-learn-course-catalog-story-cache-courses` | User can browse cached |
```

### In Code

Reference Feature IDs:

```kotlin
// @cpt-flow:cpt-learn-flow-course-list-load-cached:p1
fun loadCachedCourses() {
    // Implementation
}
```

## Validation Commands

```bash
# Check all traceability
cypilot validate all refs

# Check Platform FR coverage
cypilot validate --check=platform-fr-coverage

# Check Feature implementation
cypilot validate --check=feature-impl-coverage

# Trace specific ID
cypilot trace cpt-platform-fr-offline-support

# Find orphans (IDs with no downstream refs)
cypilot find orphans
```

## Traceability Report

```bash
cypilot coverage report
```

Output:

```
Platform FR Coverage
═══════════════════════════════════════
cpt-platform-fr-offline-support
  └── cpt-learn-fr-offline-courses
      └── cpt-learn-course-catalog-story-cache-courses
          └── cpt-learn-flow-course-list-load-cached
              └── @cpt-flow:...:p1 ✅

cpt-platform-fr-push-notifications
  └── cpt-learn-fr-course-reminders
      └── (no epic story) ⚠️

Coverage: 1/2 (50%)
```

## Checkbox Cascade

When code is implemented, checkboxes cascade upward:

```
CODE markers exist
    ↓
FEATURE-MOBILE: flow/algo/state/dod IDs → [x]
    ↓
DECOMPOSITION-EPIC: feature entry [x]
    ↓
DECOMPOSITION-SUBAPP: epic entry [x]
    ↓
DECOMPOSITION-PLATFORM: subapp entry [x]
```

## Consistency Rules

1. **Never mark parent `[x]` if child is `[ ]`**
2. **Never add code marker without CDSL instruction**
3. **Never mark reference `[x]` if definition is `[ ]`**
4. **Update design first, then code** (design is source of truth)
