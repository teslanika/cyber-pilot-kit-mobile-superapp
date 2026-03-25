# Mobile Codebase Implementation Rules

**Artifact**: CODEBASE  
**Kit**: mobile-superapp  
**Scope**: KMP, Android (Compose), iOS (SwiftUI)

**Dependencies**:
- `config/kits/mobile-superapp/codebase/checklist.md` — semantic quality criteria

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Requirements](#requirements)
3. [Tasks](#tasks)
4. [Validation](#validation)
5. [Mobile Implementation](#mobile-implementation)
6. [Next Steps](#next-steps)

---

## Prerequisites

### Load Dependencies

- [ ] Read project `AGENTS.md` for code conventions
- [ ] Load source artifact/description (FEATURE-MOBILE preferred)
- [ ] Load `config/kits/mobile-superapp/codebase/checklist.md` for quality guidance
- [ ] Load `{cypilot_path}/.core/requirements/code-checklist.md` for generic code quality checks
- [ ] If FEATURE source: identify all IDs with `to_code="true"` attribute
- [ ] Determine Traceability Mode (FULL vs DOCS-ONLY)
- [ ] If Traceability Mode FULL: load `{cypilot_path}/.core/architecture/specs/traceability.md`
- [ ] Load `config/kits/mobile-superapp/constraints.toml` for kit-level constraints

**Source** (one of, in priority order):
1. FEATURE-MOBILE design — registered artifact with `to_code="true"` IDs
2. Other Cypilot artifact — PRD-SUBAPP, PRD-EPIC, DESIGN-*, DECOMPOSITION-*
3. Similar content — user-provided description, feature, or requirements
4. Prompt only — direct user instructions

**ALWAYS read** the FEATURE-MOBILE artifact being implemented. It contains:
- Actor flows with CDSL steps
- Platform implementation sections (KMP, Android, iOS)
- State machines
- Definitions of Done

**ALWAYS read** the system's DESIGN artifact (DESIGN-PLATFORM, DESIGN-SUBAPP, or DESIGN-EPIC) to understand architecture, components, and constraints.

---

## Requirements

### Structural

- [ ] Code implements FEATURE-MOBILE design requirements
- [ ] Code follows project conventions from config
- [ ] Mobile modules follow kit structure (KMP/Android/iOS)

### Traceability

**Reference**: `{cypilot_path}/.core/architecture/specs/traceability.md` for full specification

- [ ] Traceability Mode determined per feature (FULL vs DOCS-ONLY)
- [ ] If Mode FULL: markers follow feature syntax (`@cpt-*`, `@cpt-begin`/`@cpt-end`)
- [ ] If Mode FULL: all `to_code="true"` IDs have markers
- [ ] If Mode FULL: every implemented CDSL instruction (`[x] ... \`inst-*\``) has a paired `@cpt-begin/.../@cpt-end` block marker in code
- [ ] If Mode FULL: no orphaned/stale markers
- [ ] If Mode FULL: design checkboxes synced with code
- [ ] If Mode OFF: use simplified `@cpt-impl` markers only

### Mobile Code Markers

**Simplified markers** (DOCS-ONLY mode):
```kotlin
// @cpt-impl cpt-kmp-{module}-{type}-{slug}
// @cpt-impl cpt-android-{module}-{type}-{slug}
```

```swift
// @cpt-impl cpt-ios-{module}-{type}-{slug}
```

**Full traceability markers** (FULL mode):
```kotlin
// @cpt-algo:cpt-{subapp}-algo-{feature}-kmp:p1
fun processData() {
    // @cpt-begin:cpt-{subapp}-algo-{feature}-kmp:p1:inst-kmp-1
    val intent = receiveIntent()
    // @cpt-end:cpt-{subapp}-algo-{feature}-kmp:p1:inst-kmp-1
    
    // @cpt-begin:cpt-{subapp}-algo-{feature}-kmp:p1:inst-kmp-2
    val result = useCase.invoke(intent.data)
    // @cpt-end:cpt-{subapp}-algo-{feature}-kmp:p1:inst-kmp-2
}
```

### Checkbox Cascade

CODE implementation triggers upstream checkbox updates through markers:

| Code Marker | FEATURE ID | Upstream Effect |
|-------------|-----------|-----------------|
| `@cpt-flow:{cpt-id}:p{N}` | kind: `flow` | When all pN markers exist → check `flow` ID in FEATURE |
| `@cpt-algo:{cpt-id}:p{N}` | kind: `algo` | When all pN markers exist → check `algo` ID in FEATURE |
| `@cpt-state:{cpt-id}:p{N}` | kind: `state` | When all pN markers exist → check `state` ID in FEATURE |
| `@cpt-dod:{cpt-id}:p{N}` | kind: `dod` | When all pN markers exist + evidence complete → check `dod` ID in FEATURE |

**Full Cascade Chain (Mobile SuperApp)**:
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
    ↓
PRD/DESIGN: referenced IDs [x] when ALL downstream refs [x]
```

**Consistency rules (MANDATORY)**:
- [ ] Never mark CDSL instruction `[x]` unless corresponding code block markers exist
- [ ] Never add code block marker pair unless corresponding CDSL instruction exists
- [ ] Parent ID checkbox state MUST be consistent with all nested task-tracked items
- [ ] If parent ID is `[x]` then ALL nested items MUST be `[x]`
- [ ] Never mark a reference as `[x]` if its definition is still `[ ]`

### Versioning

- [ ] When design ID versioned (`-v2`): update code markers to match
- [ ] Marker format with version: `@cpt-algo:{cpt-id}-v2:p{N}`
- [ ] Migration: update all markers when design version increments

### Engineering

- [ ] **TDD**: Write failing test first, implement minimal code to pass, then refactor
- [ ] **SOLID**:
  - Single Responsibility: Each module/function focused on one reason to change
  - Open/Closed: Extend behavior via composition/configuration, not editing unrelated logic
  - Liskov Substitution: Implementations honor interface contract and invariants
  - Interface Segregation: Prefer small, purpose-driven interfaces over broad ones
  - Dependency Inversion: Depend on abstractions; inject dependencies for testability
- [ ] **DRY**: Remove duplication by extracting shared logic with clear ownership
- [ ] **KISS**: Prefer simplest correct solution matching design and project conventions
- [ ] **YAGNI**: No specs/abstractions not required by current design scope
- [ ] **Refactoring discipline**: Refactor only after tests pass; keep behavior unchanged
- [ ] **Testability**: Structure code so core logic is testable without heavy integration
- [ ] **Error handling**: Fail explicitly with clear errors; never silently ignore failures
- [ ] **Observability**: Log meaningful events at integration boundaries (no secrets)

### Quality

**Reference**: `config/kits/mobile-superapp/codebase/checklist.md` for detailed criteria

- [ ] Code passes quality checklist
- [ ] Functions/methods are appropriately sized
- [ ] Error handling is consistent
- [ ] Tests cover implemented requirements

---

## Tasks

### Phase 1: Setup

**Resolve Source** (priority order):
1. FEATURE-MOBILE design (registered) — Traceability FULL possible
2. Other Cypilot artifact (PRD/DESIGN) — DOCS-ONLY
3. User-provided description — DOCS-ONLY
4. Prompt only — DOCS-ONLY
5. None — suggest `/cypilot-generate FEATURE-MOBILE` first

**Load Context**:
- [ ] Read project `AGENTS.md` for code conventions
- [ ] Load source artifact/description
- [ ] Load `config/kits/mobile-superapp/codebase/checklist.md` for quality guidance
- [ ] Determine Traceability Mode
- [ ] Plan implementation order by platform (KMP → Android → iOS)

### Phase 2: Implementation (Work Packages)

**For each work package:**

1. Identify exact design items to code (flows/algos/states/requirements/tests)
2. **KMP First**: Implement shared logic (ViewModel, UseCase, Repository)
3. **Android Second**: Implement Compose UI
4. **iOS Third**: Implement SwiftUI views with KMP wrapper
5. If Traceability Mode FULL: add `@cpt-begin`/`@cpt-end` markers per CDSL instruction
6. Run work package validation (tests, build, linters)
7. If Traceability Mode FULL: update FEATURE-MOBILE checkboxes
8. Proceed to next work package

### Phase 3: Cypilot Markers (Traceability Mode FULL only)

Apply markers per feature:
- **Scope markers**: `@cpt-{kind}:{cpt-id}:p{N}` — single-line, at function/class entry point
- **Block markers**: `@cpt-begin:{cpt-id}:p{N}:inst-{local}` / `@cpt-end:...` — paired, wrapping specific lines

**Granularity rules (MANDATORY)**:
1. Each `@cpt-begin`/`@cpt-end` pair wraps the **smallest code fragment** that implements its CDSL instruction
2. When a function implements multiple CDSL instructions, place **separate** begin/end pairs for each
3. Place markers as **close to the implementing code as possible**
4. Do NOT wrap entire function body with single begin/end pair when multiple instructions exist

**Correct example (KMP ViewModel)**:
```kotlin
// @cpt-algo:cpt-student-algo-home-kmp:p1
class HomeViewModel(private val useCase: LoadHomeUseCase) : ViewModel() {
    
    fun processIntent(intent: HomeIntent) {
        // @cpt-begin:cpt-student-algo-home-kmp:p1:inst-kmp-1
        when (intent) {
            is HomeIntent.Load -> loadData()
        }
        // @cpt-end:cpt-student-algo-home-kmp:p1:inst-kmp-1
    }
    
    private fun loadData() {
        // @cpt-begin:cpt-student-algo-home-kmp:p1:inst-kmp-2
        viewModelScope.launch {
            val result = useCase()
        // @cpt-end:cpt-student-algo-home-kmp:p1:inst-kmp-2
        
        // @cpt-begin:cpt-student-algo-home-kmp:p1:inst-kmp-3
            _state.value = when (result) {
                is Result.Success -> HomeState.Content(result.data)
                is Result.Error -> HomeState.Error(result.message)
            }
        // @cpt-end:cpt-student-algo-home-kmp:p1:inst-kmp-3
        }
    }
}
```

### Phase 4: Sync FEATURE-MOBILE (Traceability Mode FULL only)

After each work package, sync checkboxes:
1. Mark implemented CDSL steps `[x]` in FEATURE-MOBILE
2. When all steps done → mark flow/algo/state/dod `[x]` in FEATURE-MOBILE
3. When all IDs done → mark feature entry `[x]` in DECOMPOSITION-EPIC
4. Update feature status: `⏳ PLANNED` → `🔄 IN_PROGRESS` → `✅ IMPLEMENTED`

### Phase 5: Quality Check

- [ ] Self-review against `config/kits/mobile-superapp/codebase/checklist.md`
- [ ] If Traceability Mode FULL: verify all `to_code="true"` IDs have markers
- [ ] If Traceability Mode FULL: ensure no orphaned markers
- [ ] Run tests to verify implementation
- [ ] Verify engineering best practices followed

### Phase 6: Tag Verification (Traceability Mode FULL only)

- [ ] Search codebase for ALL IDs from FEATURE-MOBILE (flow/algo/state/dod)
- [ ] Confirm tags exist in files that implement corresponding logic/tests
- [ ] If any FEATURE ID has no code tag → report as gap and/or add tag

---

## Validation

### Phase 1: Implementation Coverage

- [ ] Code files exist and contain implementation
- [ ] Code is not placeholder/stub (no TODO/FIXME/unimplemented!)
- [ ] All three platforms implemented (KMP, Android, iOS)

### Phase 2: Traceability Validation (Mode FULL only)

- [ ] Marker format valid
- [ ] All begin/end pairs matched
- [ ] No empty blocks
- [ ] All `to_code="true"` IDs have markers
- [ ] No orphaned/stale markers
- [ ] Design checkboxes synced with code markers

### Phase 3: Test Scenarios Validation

- [ ] Test file exists for each test scenario from design
- [ ] Test contains scenario ID in comment for traceability
- [ ] Test is NOT ignored without justification
- [ ] Test actually validates scenario behavior

### Phase 4: Build and Lint Validation

- [ ] KMP build succeeds (`./gradlew :constructor-sdk:build`)
- [ ] Android build succeeds (`./gradlew :android-app:assembleDebug`)
- [ ] iOS build succeeds (`xcodebuild`)
- [ ] Linter passes (ktlint, detekt, swiftlint)

**Report format**:
```
Mobile Code Quality Report
══════════════════════════
Build KMP: PASS/FAIL
Build Android: PASS/FAIL
Build iOS: PASS/FAIL
Lint: PASS/FAIL
Tests: X/Y passed
Coverage: N%
Checklist: PASS/FAIL (N issues)
```

### Phase 5: Test Execution

- [ ] KMP unit tests pass
- [ ] Android unit tests pass
- [ ] Android UI tests pass
- [ ] iOS unit tests pass
- [ ] iOS UI tests pass
- [ ] Coverage meets project requirements (80%+)

### Phase 6: Code Quality Validation

- [ ] No TODO/FIXME/XXX/HACK in domain/presentation layers
- [ ] No bare `!!` (force unwrap) in Kotlin production code
- [ ] No force unwrapping in Swift production code
- [ ] TDD: New/changed behavior covered by tests
- [ ] SOLID: Responsibilities separated; dependencies injectable
- [ ] DRY: No copy-paste duplication
- [ ] KISS: No unnecessary complexity
- [ ] YAGNI: No speculative abstractions

### Phase 7: Code Logic Consistency with Design

**For each requirement marked IMPLEMENTED:**
- [ ] Read requirement specification
- [ ] Locate implementing code via @cpt-* tags
- [ ] Verify code logic matches requirement (no contradictions)
- [ ] Verify no skipped mandatory steps
- [ ] Verify error handling matches design error specifications

**For each flow marked implemented:**
- [ ] All flow steps executed in correct order
- [ ] No steps bypassed that would change behavior
- [ ] Conditional logic matches design conditions
- [ ] Error paths match design error handling

**For each algorithm marked implemented:**
- [ ] Performance characteristics match design
- [ ] Edge cases handled as designed
- [ ] No logic shortcuts that violate design constraints

### Phase 8: Semantic Expert Review

Run expert panel review after producing validation output.

**Review Scope Selection**:

| Change Size | Review Mode | Experts |
|-------------|-------------|--------|
| <50 LOC, single concern | Abbreviated | Developer + 1 relevant expert |
| 50-200 LOC, multiple concerns | Standard | Developer, QA, Mobile Architect |
| >200 LOC or architectural | Full | All experts |

**Mobile Expert Panel**: Developer, QA Engineer, Mobile Architect, Security Expert, Performance Engineer, Accessibility Expert

**For EACH expert:**
1. Adopt role (write: `Role assumed: {expert}`)
2. Review actual code and tests in validation scope
3. If design artifact available: evaluate design-to-code alignment
4. Identify issues
5. Provide concrete proposals
6. Propose corrective workflow: `feature`, `design`, or `code`

**PASS only if:**
- Build/lint/tests pass per project config
- Coverage meets project requirements
- No CRITICAL divergences between code and design
- If Traceability Mode FULL: required tags present and properly paired

---

## Mobile Implementation

### KMP Implementation

**Directory Structure**:
```
constructor-sdk/feature/{module}/
├── src/
│   ├── commonMain/kotlin/com/constructor/sdk/feature/{module}/
│   │   ├── domain/
│   │   │   ├── model/           # Domain entities
│   │   │   └── usecase/         # Use cases
│   │   ├── data/
│   │   │   ├── repository/      # Repository implementations
│   │   │   ├── remote/          # API clients, DTOs
│   │   │   └── local/           # Local data sources
│   │   └── presentation/
│   │       ├── {Feature}ViewModel.kt
│   │       ├── {Feature}State.kt
│   │       ├── {Feature}Intent.kt
│   │       └── {Feature}Effect.kt
│   ├── androidMain/             # Android-specific expect/actual
│   └── iosMain/                 # iOS-specific expect/actual
└── build.gradle.kts
```

**MVI Pattern Rules**:

**State Class**:
- [ ] MUST be immutable `data class`
- [ ] MUST have default values for all properties
- [ ] MUST NOT contain mutable collections

**Intent Class**:
- [ ] MUST be `sealed class`
- [ ] Each intent represents a user action

**Effect Class**:
- [ ] MUST be `sealed class`
- [ ] Effects are one-time actions (navigation, toast, etc.)

**ViewModel**:
- [ ] MUST process Intent → State + Effects
- [ ] MUST expose `state: StateFlow<State>`
- [ ] MUST expose `effects: SharedFlow<Effect>`

### Android Implementation

**Directory Structure**:
```
android-app/feature/{module}/
├── src/main/kotlin/com/constructor/android/feature/{module}/
│   ├── ui/
│   │   ├── {Feature}Screen.kt           # Main screen
│   │   └── components/                   # Reusable components
│   ├── navigation/
│   │   └── {Feature}NavGraph.kt
│   └── di/
│       └── {Feature}Module.kt           # Hilt module
└── build.gradle.kts
```

**Compose Screen Rules**:
- [ ] MUST use `collectAsStateWithLifecycle()` for state
- [ ] MUST handle all screen states (Loading, Content, Error, Empty)
- [ ] MUST pass events via lambda or Intent

### iOS Implementation

**Directory Structure**:
```
ios-app/Features/{Module}/
├── Views/
│   ├── {Feature}View.swift              # Main SwiftUI view
│   └── Components/                       # Reusable components
├── Navigation/
│   └── {Feature}Coordinator.swift
├── ViewModels/
│   └── {Feature}ViewModelWrapper.swift  # KMP ViewModel bridge
└── Resources/
```

**SwiftUI View Rules**:
- [ ] MUST use `@StateObject` for ViewModel wrapper
- [ ] MUST handle all view states
- [ ] MUST use Combine for KMP state observation

**KMP Bridge Pattern**:
```swift
class {Feature}ViewModelWrapper: ObservableObject {
    private let kmpViewModel: {Feature}ViewModel
    @Published var state: {Feature}State
    
    func send(_ intent: {Feature}Intent) {
        kmpViewModel.processIntent(intent)
    }
}
```

### IMPL.md Files

Each feature module MUST have an IMPL.md file:
- `constructor-sdk/feature/{module}/IMPL.md`
- `android-app/feature/{module}/IMPL.md`
- `ios-app/Features/{Module}/IMPL.md`

---

## Next Steps

### After Success

- [ ] Feature complete → update feature status to IMPLEMENTED in DECOMPOSITION-EPIC
- [ ] All features done → `/cypilot-analyze DESIGN-EPIC` — validate epic completion
- [ ] New feature needed → `/cypilot-generate FEATURE-MOBILE` — design next feature
- [ ] Want expert review only → `/cypilot-analyze semantic` — semantic validation

### After Issues

- [ ] Design mismatch → `/cypilot-generate FEATURE-MOBILE` — update feature design
- [ ] Missing tests → continue `/cypilot-generate CODE` — add tests
- [ ] Code quality issues → continue `/cypilot-generate CODE` — refactor
- [ ] Platform-specific bug → fix in respective platform module

### No Design

- [ ] Implementing new feature → `/cypilot-generate FEATURE-MOBILE` first
- [ ] Implementing from PRD → `/cypilot-generate DESIGN-EPIC` then DECOMPOSITION-EPIC
- [ ] Quick prototype → proceed without traceability, suggest FEATURE-MOBILE later
