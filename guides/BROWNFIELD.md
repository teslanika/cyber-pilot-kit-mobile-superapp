# Brownfield Guide — Mobile SuperApp

Use this guide when you already have a mobile codebase and want to adopt Cypilot.

All prompts work through the `cypilot` skill — enable it with `cypilot on` and use natural language prompts.

## Goal

Adopt Cypilot incrementally — start with what makes sense for your mobile project, not a fixed sequence.

## Key Principle: Start Anywhere

Unlike greenfield projects, **brownfield has no required order**. You can:

- Start with **any level** — Platform, MiniApp, Epic, or Feature
- Work **top-down** (Platform → Feature → CODE) or **bottom-up** (CODE → Feature → Platform)
- Adopt **incrementally** — use only what you need, add more later
- Use **code-only mode** — just Cypilot's code generation with MVI pattern guidance

**Even with zero artifacts**, Cypilot's mobile code generation uses the `codebase-checklist` internally for quality guidance.

---

## Adoption Scenarios

### Scenario A: Code-Only

You just want better mobile code generation. No artifacts needed.

| Prompt | What happens |
|--------|--------------|
| `cypilot implement feature auth` | Generates KMP/Android/iOS code with MVI |
| `cypilot add markers to shared/src/` | Adds traceability markers to existing KMP |
| `cypilot add markers to android-app/` | Adds markers to Android code |
| `cypilot validate code` | Validates code quality and markers |

**Benefits**: MVI pattern guidance, consistent architecture, code traceability.

### Scenario B: Feature-First (Bottom-Up)

You want to document existing mobile features, then build up.

```
1. cypilot reverse FEATURE-MOBILE from shared/feature/auth/
   → Creates FEATURE-MOBILE from existing KMP code

2. cypilot reverse FEATURE-MOBILE from shared/feature/courses/
   → Creates another FEATURE from code

3. cypilot make DECOMPOSITION-EPIC from features
   → Creates DECOMPOSITION-EPIC from FEATUREs

4. cypilot make DESIGN-EPIC from DECOMPOSITION-EPIC
   → Creates DESIGN-EPIC from structure

5. (optional) Continue up to MiniApp and Platform levels
```

**When to use**: You want to document what exists without changing code.

### Scenario C: MiniApp-First (Middle-Out)

You want to capture MiniApp architecture, then decompose into features.

```
1. cypilot reverse DESIGN-MINIAPP for learn from codebase
   → Extracts Learn MiniApp architecture from code

2. cypilot make DECOMPOSITION-MINIAPP for learn
   → Creates Epic breakdown

3. cypilot make FEATURE-MOBILE for {slug}
   → Creates detailed features

4. cypilot implement {slug}
   → Implements with traceability markers
```

**When to use**: You want architectural control over a specific MiniApp.

### Scenario D: Full Top-Down

You want complete 4-level documentation from platform to code.

```
1. cypilot reverse PRD-PLATFORM from codebase
   → Extracts platform requirements

2. cypilot reverse DESIGN-PLATFORM from codebase
   → Documents current architecture

3. Continue through all levels...

4. cypilot implement {feature}
   → Implements with full traceability
```

**When to use**: New team members, compliance requirements, or major refactoring.

### Scenario E: Gradual Adoption

Start minimal, add artifacts as needed.

```
Week 1: cypilot implement {feature}        → Code-only, with MVI checklist
Week 2: cypilot make FEATURE-MOBILE        → Add features for complex work
Week 3: cypilot make DECOMPOSITION-EPIC    → Organize features into epics
Later:  cypilot make DESIGN-MINIAPP         → Document MiniApp architecture
```

**When to use**: You want low-friction adoption with growing benefits.

---

## Reverse Engineering Prompts

### From Existing KMP Code

| Prompt | What happens |
|--------|--------------|
| `cypilot reverse FEATURE-MOBILE from shared/feature/auth/` | Creates FEATURE from KMP module |
| `cypilot reverse DESIGN-MINIAPP from shared/feature/learn/` | Creates MiniApp design from module |
| `cypilot reverse DESIGN-PLATFORM from shared/` | Documents platform architecture |

### From Existing Android Code

| Prompt | What happens |
|--------|--------------|
| `cypilot reverse FEATURE-MOBILE from android-app/feature/auth/` | Creates FEATURE from Android module |
| `cypilot analyze android-app/feature/auth/` | Systematic code analysis |

### From Existing iOS Code

| Prompt | What happens |
|--------|--------------|
| `cypilot reverse FEATURE-MOBILE from ios-app/Features/Auth/` | Creates FEATURE from iOS module |
| `cypilot analyze ios-app/Features/Auth/` | Systematic code analysis |

### From Existing Docs

| Prompt | What happens |
|--------|--------------|
| `cypilot make PRD-PLATFORM from README` | Creates PRD from README |
| `cypilot make DESIGN-MINIAPP from docs/architecture.md` | Creates design from existing docs |
| `cypilot import OpenAPI as DESIGN-MINIAPP` | Converts API spec into design |

---

## Adding Features to Existing Code

### 1. Add to Appropriate Level

| Prompt | What happens |
|--------|--------------|
| `cypilot add miniapp notifications to platform` | Adds MiniApp to platform decomposition |
| `cypilot add epic push-notifications to miniapp notifications` | Adds Epic to MiniApp |
| `cypilot add feature notification-list to epic push-notifications` | Adds Feature to Epic |

### 2. Create FEATURE-MOBILE

| Prompt | What happens |
|--------|--------------|
| `cypilot make FEATURE-MOBILE for notification-list` | Creates feature design |
| `cypilot reverse FEATURE-MOBILE from shared/feature/notifications/` | From existing code |

**Provide context:**
```
cypilot make FEATURE-MOBILE for notification-list
Context:
- Feature: Notification List
- Epic: Push Notifications
- MiniApp: Notifications
- Existing code: shared/feature/notifications/
- States: Loading, Content(notifications), Empty
- Intents: Load, MarkRead, Delete
```

### 3. Validate and Implement

| Prompt | What happens |
|--------|--------------|
| `cypilot validate FEATURE-MOBILE for notification-list` | Validates feature |
| `cypilot implement notification-list` | Generates code |
| `cypilot implement notification-list remaining` | Only unimplemented parts |

---

## Sync and Compare

When code and design drift apart:

| Prompt | What happens |
|--------|--------------|
| `cypilot compare DESIGN-MINIAPP for learn to code` | Shows drift |
| `cypilot compare FEATURE-MOBILE for course-list to code` | Shows feature drift |
| `cypilot sync DESIGN-MINIAPP for learn from code` | Updates design from code |
| `cypilot sync FEATURE-MOBILE for course-list from code` | Updates feature from code |
| `cypilot sync code with FEATURE-MOBILE for course-list` | Updates code from feature |

---

## Adding Markers to Existing Code

### KMP Shared Code

```kotlin
// Before: no markers
class CourseListViewModel(
    private val loadCoursesUseCase: LoadCoursesUseCase
) : ViewModel() {
    fun loadCourses() { ... }
}

// After: with markers
// @cpt-impl cpt-learn-course-list-viewmodel-kmp
class CourseListViewModel(
    private val loadCoursesUseCase: LoadCoursesUseCase
) : ViewModel() {
    // @cpt-begin:cpt-learn-flow-course-list-load:p1:inst-kmp-1
    fun loadCourses() { ... }
    // @cpt-end:cpt-learn-flow-course-list-load:p1:inst-kmp-1
}
```

### Android Compose

```kotlin
// @cpt-impl cpt-learn-course-list-screen-android
@Composable
fun CourseListScreen(
    viewModel: CourseListViewModel = hiltViewModel()
) {
    // @cpt-begin:cpt-learn-flow-course-list-load:p1:inst-android-1
    val state by viewModel.state.collectAsStateWithLifecycle()
    // @cpt-end:cpt-learn-flow-course-list-load:p1:inst-android-1
}
```

### iOS SwiftUI

```swift
// @cpt-impl cpt-learn-course-list-view-ios
struct CourseListView: View {
    // @cpt-begin:cpt-learn-flow-course-list-load:p1:inst-ios-1
    @StateObject private var viewModel = CourseListViewModelWrapper()
    // @cpt-end:cpt-learn-flow-course-list-load:p1:inst-ios-1
}
```

### Prompts for Adding Markers

| Prompt | What happens |
|--------|--------------|
| `cypilot add markers to shared/feature/courses/` | Adds markers to KMP module |
| `cypilot add markers for course-list` | Adds markers matching FEATURE |
| `cypilot fix markers in android-app/feature/` | Fixes incorrect markers |

---

## Common Scenarios

### Requirements Changed at Platform Level

```
cypilot update PRD-PLATFORM
cypilot validate PRD-PLATFORM
cypilot propagate PRD-PLATFORM changes to DESIGN-PLATFORM
cypilot validate DESIGN-PLATFORM
# Continue down through affected MiniApps/Epics/Features
```

### MiniApp Design Changed

```
cypilot update DESIGN-MINIAPP for learn
cypilot validate DESIGN-MINIAPP for learn
cypilot propagate DESIGN-MINIAPP changes to affected epics
# Continue down through affected Epics/Features
```

### Feature Design Changed

```
cypilot update FEATURE-MOBILE for course-list
cypilot validate FEATURE-MOBILE for course-list
cypilot sync code with FEATURE-MOBILE for course-list
cypilot validate code for course-list
```

### Code Changed Without Design Update

```
cypilot compare FEATURE-MOBILE for course-list to code
cypilot sync FEATURE-MOBILE for course-list from code
cypilot validate FEATURE-MOBILE for course-list
```

---

## Quick Reference

### By Adoption Level

| Level | What you do | Benefits |
|-------|-------------|----------|
| **Code-only** | `cypilot implement {slug}` | MVI checklist, consistent patterns |
| **+ FEATURE** | Add `cypilot make FEATURE-MOBILE` | Flows, states, edge cases documented |
| **+ DECOMPOSITION** | Add `cypilot make DECOMPOSITION-EPIC` | Feature organization, dependencies |
| **+ DESIGN** | Add `cypilot make DESIGN-{LEVEL}` | Architecture, components, data model |
| **+ PRD** | Add `cypilot make PRD-{LEVEL}` | Requirements, full 4-level traceability |

### Top-Down (Full)

| Step | Generate | Validate |
|------|----------|----------|
| 1 | `cypilot reverse PRD-PLATFORM` | `cypilot validate PRD-PLATFORM` |
| 2 | `cypilot reverse DESIGN-PLATFORM` | `cypilot validate DESIGN-PLATFORM` |
| 3 | `cypilot make DECOMPOSITION-PLATFORM` | `cypilot validate DECOMPOSITION-PLATFORM` |
| ... | Continue through all levels | ... |
| N | `cypilot implement {feature}` | `cypilot validate code for {feature}` |

### Bottom-Up (Feature-First)

| Step | Generate | Validate |
|------|----------|----------|
| 1 | `cypilot reverse FEATURE-MOBILE from {path}` | `cypilot validate FEATURE-MOBILE` |
| 2 | `cypilot make DECOMPOSITION-EPIC from features` | `cypilot validate DECOMPOSITION-EPIC` |
| 3 | `cypilot make DESIGN-EPIC` | `cypilot validate DESIGN-EPIC` |
| ... | Continue up as needed | ... |

### Code-Only

| Prompt | What happens |
|--------|--------------|
| `cypilot implement {slug}` | Generates code with MVI guidance |
| `cypilot add markers to {path}` | Adds traceability to existing code |
| `cypilot validate code` | Validates code quality |

**Validation modes** (append to any `validate` command):
- `semantic` — content quality, completeness, mobile patterns
- `structural` — format, IDs, template compliance
- `refs` — cross-references across levels
- `quick` — critical issues only (fast)

## Iteration Rules

- Start with what you need — add more artifacts as value becomes clear
- If code changes affect feature behavior, update FEATURE-MOBILE first
- Re-validate the FEATURE design
- Run `cypilot validate code` to ensure design and code remain consistent
- If code contradicts design, decide: update design OR update code
