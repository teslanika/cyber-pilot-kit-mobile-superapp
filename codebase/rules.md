# Mobile Codebase Implementation Rules

**Kit**: mobile-superapp  
**Scope**: KMP, Android (Compose), iOS (SwiftUI)

This document defines implementation rules for mobile SuperApp codebases using the mobile-superapp kit.

---

## Table of Contents

1. [Code Markers](#code-markers)
2. [KMP Implementation](#kmp-implementation)
3. [Android Implementation](#android-implementation)
4. [iOS Implementation](#ios-implementation)
5. [Traceability](#traceability)
6. [Validation](#validation)

---

## Code Markers

### @cpt-impl Marker Format

All implementations MUST include `@cpt-impl` markers linking code to documentation:

```kotlin
// @cpt-impl cpt-kmp-{module}-{type}-{slug}
```

```kotlin
// @cpt-impl cpt-android-{module}-{type}-{slug}
```

```swift
// @cpt-impl cpt-ios-{module}-{type}-{slug}
```

### Marker Placement

- [ ] Place marker immediately before class/function declaration
- [ ] One marker per implementation unit
- [ ] Multiple markers allowed if code implements multiple design components

### Marker Types

| Type | Description | Example |
|------|-------------|---------|
| `usecase` | Use case implementation | `cpt-kmp-home-usecase-load` |
| `vm` | ViewModel implementation | `cpt-kmp-home-vm-main` |
| `repo` | Repository implementation | `cpt-kmp-home-repo-courses` |
| `entity` | Domain entity | `cpt-kmp-home-entity-course` |
| `screen` | Screen composable/view | `cpt-android-home-screen-main` |
| `widget` | Reusable UI component | `cpt-android-home-widget-streak` |
| `nav` | Navigation component | `cpt-android-home-nav-graph` |
| `view` | SwiftUI view | `cpt-ios-home-view-main` |

---

## KMP Implementation

### Directory Structure

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

### MVI Pattern Rules

**State Class**:
- [ ] MUST be immutable `data class`
- [ ] MUST have default values for all properties
- [ ] MUST NOT contain mutable collections

```kotlin
// @cpt-impl cpt-kmp-{module}-state-{slug}
data class {Feature}State(
    val isLoading: Boolean = false,
    val data: List<{Entity}> = emptyList(),
    val error: String? = null
)
```

**Intent Class**:
- [ ] MUST be `sealed class`
- [ ] Each intent represents a user action

```kotlin
// @cpt-impl cpt-kmp-{module}-intent-{slug}
sealed class {Feature}Intent {
    object Load : {Feature}Intent()
    data class Select(val id: String) : {Feature}Intent()
}
```

**Effect Class**:
- [ ] MUST be `sealed class`
- [ ] Effects are one-time actions (navigation, toast, etc.)

```kotlin
// @cpt-impl cpt-kmp-{module}-effect-{slug}
sealed class {Feature}Effect {
    data class Navigate(val route: String) : {Feature}Effect()
    data class ShowError(val message: String) : {Feature}Effect()
}
```

**ViewModel**:
- [ ] MUST process Intent → State + Effects
- [ ] MUST expose `state: StateFlow<State>`
- [ ] MUST expose `effects: SharedFlow<Effect>`

### Repository Rules

- [ ] Interface defined in `domain/`
- [ ] Implementation in `data/repository/`
- [ ] Return `Result<T>` for operations that can fail
- [ ] Cache strategy documented in DESIGN

### Use Case Rules

- [ ] Single responsibility
- [ ] `operator fun invoke(input: Input): Result<Output>`
- [ ] Input validation at beginning
- [ ] Error mapping to domain errors

---

## Android Implementation

### Directory Structure

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
├── src/main/res/
│   ├── values/strings.xml
│   └── drawable/
└── build.gradle.kts
```

### Compose Screen Rules

- [ ] MUST use `collectAsStateWithLifecycle()` for state
- [ ] MUST handle all screen states (Loading, Content, Error, Empty)
- [ ] MUST pass events via lambda or Intent

```kotlin
// @cpt-impl cpt-android-{module}-screen-{slug}
@Composable
fun {Feature}Screen(
    viewModel: {Feature}ViewModel = hiltViewModel(),
    onNavigate: (String) -> Unit
) {
    val state by viewModel.state.collectAsStateWithLifecycle()
    
    LaunchedEffect(Unit) {
        viewModel.effects.collect { effect ->
            when (effect) {
                is {Feature}Effect.Navigate -> onNavigate(effect.route)
                is {Feature}Effect.ShowError -> { /* show snackbar */ }
            }
        }
    }
    
    // Render based on state
}
```

### Navigation Rules

- [ ] Use Navigation Compose
- [ ] Define routes as constants
- [ ] Support deep links where specified in DESIGN

---

## iOS Implementation

### Directory Structure

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
    ├── Localizable.strings
    └── Assets.xcassets/
```

### SwiftUI View Rules

- [ ] MUST use `@StateObject` for ViewModel wrapper
- [ ] MUST handle all view states
- [ ] MUST use Combine for KMP state observation

```swift
// @cpt-impl cpt-ios-{module}-view-{slug}
struct {Feature}View: View {
    @StateObject private var viewModel: {Feature}ViewModelWrapper
    
    var body: some View {
        content
            .onAppear { viewModel.send(.load) }
    }
    
    @ViewBuilder
    private var content: some View {
        switch viewModel.state.screenState {
        case .loading: ProgressView()
        case .content(let data): ContentView(data: data)
        case .error(let message): ErrorView(message: message)
        }
    }
}
```

### KMP Bridge Rules

- [ ] Use `ObservableObject` wrapper
- [ ] Subscribe to KMP StateFlow
- [ ] Forward intents to KMP ViewModel

```swift
// @cpt-impl cpt-ios-{module}-wrapper-{slug}
class {Feature}ViewModelWrapper: ObservableObject {
    private let kmpViewModel: {Feature}ViewModel
    
    @Published var state: {Feature}State
    
    init() {
        self.kmpViewModel = {Feature}ViewModel()
        // Observe KMP StateFlow
    }
    
    func send(_ intent: {Feature}Intent) {
        kmpViewModel.processIntent(intent)
    }
}
```

---

## Traceability

### IMPL.md Files

Each feature module MUST have an IMPL.md file:
- `constructor-sdk/feature/{module}/IMPL.md`
- `android-app/feature/{module}/IMPL.md`
- `ios-app/Features/{Module}/IMPL.md`

### Traceability Table Format

```markdown
| Design Component ID | Code File | Implementation ID |
|---------------------|-----------|-------------------|
| `cpt-{subapp}-{epic}-usecase-{slug}` | `usecase/{UseCase}.kt` | `@cpt-impl cpt-kmp-{module}-usecase-{slug}` |
```

---

## Validation

### Run Validation

```bash
# Validate KMP module
cypilot validate --artifact constructor-sdk/feature/{module}/

# Validate Android module
cypilot validate --artifact android-app/feature/{module}/

# Validate iOS module
cypilot validate --artifact ios-app/Features/{Module}/
```

### Validation Checks

- [ ] All design components have `@cpt-impl` markers
- [ ] All markers reference valid design IDs
- [ ] Coverage meets minimum threshold (80%)
- [ ] IMPL.md files are up to date
