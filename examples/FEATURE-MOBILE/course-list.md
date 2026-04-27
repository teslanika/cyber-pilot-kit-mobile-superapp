# FEATURE-MOBILE: Course List

## Meta

| Field | Value |
|-------|-------|
| Feature ID | `cpt-learn-course-catalog-feature-course-list` |
| Epic | Course Catalog (`cpt-learn-epic-course-catalog`) |
| MiniApp | Learn (`cpt-platform-miniapp-learn`) |
| Status | `DESIGNED` |
| Version | 1.0 |

## Overview

Display a paginated list of available courses with search and filtering capabilities.

## Traceability

### Cascading Requirements

| Level | ID | Description |
|-------|-----|-------------|
| Platform FR | `cpt-platform-fr-course-discovery` | Users can discover available courses |
| Platform FR | `cpt-platform-fr-offline-support` | Core features work offline |
| MiniApp FR | `cpt-learn-fr-browse-courses` | Students can browse course catalog |
| MiniApp FR | `cpt-learn-fr-offline-courses` | Cached courses available offline |
| Epic Story | `cpt-learn-course-catalog-story-view-courses` | As a student, I want to view available courses |
| Epic AC | `cpt-learn-course-catalog-ac-list-pagination` | List supports infinite scroll pagination |

### Design References

| Kind | ID | Description |
|------|-----|-------------|
| Component | `cpt-learn-component-course-repository` | Course data access |
| Component | `cpt-learn-course-catalog-component-list-viewmodel` | List ViewModel |
| Sequence | `cpt-learn-course-catalog-seq-load-courses` | Load courses flow |

## MVI Definition

### State

```kotlin
// cpt-learn-course-list-state
data class CourseListState(
    val isLoading: Boolean = false,
    val isLoadingMore: Boolean = false,
    val courses: List<CourseItem> = emptyList(),
    val hasMorePages: Boolean = true,
    val error: CourseListError? = null,
    val searchQuery: String = "",
    val selectedCategory: Category? = null
)

data class CourseItem(
    val id: String,
    val title: String,
    val description: String,
    val thumbnailUrl: String?,
    val instructorName: String,
    val duration: Duration,
    val enrollmentCount: Int,
    val rating: Float?
)

sealed class CourseListError {
    object NetworkError : CourseListError()
    object ServerError : CourseListError()
    data class Unknown(val message: String) : CourseListError()
}
```

### Intent

```kotlin
// cpt-learn-course-list-intent
sealed class CourseListIntent {
    object LoadInitial : CourseListIntent()
    object LoadMore : CourseListIntent()
    object Refresh : CourseListIntent()
    data class Search(val query: String) : CourseListIntent()
    data class SelectCategory(val category: Category?) : CourseListIntent()
    data class SelectCourse(val courseId: String) : CourseListIntent()
    object RetryAfterError : CourseListIntent()
}
```

### Effect

```kotlin
// cpt-learn-course-list-effect
sealed class CourseListEffect {
    data class NavigateToCourseDetail(val courseId: String) : CourseListEffect()
    data class ShowErrorToast(val message: String) : CourseListEffect()
    object ScrollToTop : CourseListEffect()
}
```

## Actor Flows

### Flow: Load Courses `cpt-learn-flow-course-list-load` `to_code="true"`

**Actor**: Student  
**Precondition**: User opens Learn MiniApp  
**Postcondition**: Course list displayed or error shown

```cdsl
flow cpt-learn-flow-course-list-load {
  actor: Student
  
  p1: [x] User opens course catalog screen `inst-open`
  p2: [x] System shows loading indicator `inst-loading`
  p3: [x] System fetches courses from repository `inst-fetch`
  p4: [x] System receives course list `inst-receive`
  p5: [x] System hides loading indicator `inst-hide-loading`
  p6: [x] System displays courses in list `inst-display`
  
  error-network: [ ] If network error → show cached courses if available, else show error `inst-error-network`
  error-empty: [ ] If no courses → show empty state `inst-error-empty`
}
```

### Flow: Load More (Pagination) `cpt-learn-flow-course-list-load-more` `to_code="true"`

**Actor**: Student  
**Precondition**: Course list displayed, more pages available  
**Postcondition**: Additional courses appended

```cdsl
flow cpt-learn-flow-course-list-load-more {
  actor: Student
  
  p1: [ ] User scrolls to bottom of list `inst-scroll`
  p2: [ ] System shows loading more indicator `inst-loading-more`
  p3: [ ] System fetches next page `inst-fetch-next`
  p4: [ ] System appends courses to existing list `inst-append`
  p5: [ ] System hides loading indicator `inst-hide-loading`
  p6: [ ] System updates hasMorePages flag `inst-update-flag`
  
  error: [ ] If error → show toast, keep existing list `inst-error`
}
```

### Flow: Search Courses `cpt-learn-flow-course-list-search` `to_code="true"`

**Actor**: Student  
**Precondition**: Course list displayed  
**Postcondition**: Filtered courses displayed

```cdsl
flow cpt-learn-flow-course-list-search {
  actor: Student
  
  p1: [ ] User enters search query `inst-enter-query`
  p2: [ ] System debounces input (300ms) `inst-debounce`
  p3: [ ] System shows loading indicator `inst-loading`
  p4: [ ] System fetches filtered courses `inst-fetch-filtered`
  p5: [ ] System replaces list with results `inst-replace`
  p6: [ ] System scrolls to top `inst-scroll-top`
  
  empty: [ ] If no results → show "no results" state `inst-empty`
}
```

### Flow: Pull to Refresh `cpt-learn-flow-course-list-refresh` `to_code="true"`

**Actor**: Student  
**Precondition**: Course list displayed  
**Postcondition**: List refreshed with latest data

```cdsl
flow cpt-learn-flow-course-list-refresh {
  actor: Student
  
  p1: [ ] User pulls down on list `inst-pull`
  p2: [ ] System shows refresh indicator `inst-refresh-indicator`
  p3: [ ] System fetches fresh data `inst-fetch-fresh`
  p4: [ ] System replaces list with new data `inst-replace`
  p5: [ ] System hides refresh indicator `inst-hide-indicator`
  
  error: [ ] If error → show toast, keep existing list `inst-error`
}
```

## Algorithms

### Algorithm: Course Caching `cpt-learn-algo-course-list-cache` `to_code="true"`

```cdsl
algo cpt-learn-algo-course-list-cache {
  input: List<CourseDTO>
  output: Unit
  
  p1: [ ] Map DTOs to domain models `inst-map`
  p2: [ ] Store in local database `inst-store`
  p3: [ ] Update cache timestamp `inst-timestamp`
  p4: [ ] Prune old entries (>7 days) `inst-prune`
}
```

### Algorithm: Search Debounce `cpt-learn-algo-course-list-debounce` `to_code="true"`

```cdsl
algo cpt-learn-algo-course-list-debounce {
  input: String (query)
  output: Flow<String>
  
  p1: [ ] Receive query input `inst-receive`
  p2: [ ] Cancel previous debounce job `inst-cancel`
  p3: [ ] Start 300ms delay `inst-delay`
  p4: [ ] Emit query if not cancelled `inst-emit`
}
```

## State Machine

### State: Course List Screen `cpt-learn-state-course-list-screen` `to_code="true"`

```
stateDiagram-v2
    [*] --> Loading: LoadInitial
    Loading --> Content: Success
    Loading --> Error: Failure
    Loading --> Empty: EmptyResult
    
    Content --> LoadingMore: LoadMore
    Content --> Refreshing: Refresh
    Content --> Searching: Search
    
    LoadingMore --> Content: Success/Failure
    Refreshing --> Content: Success/Failure
    Searching --> Content: Success
    Searching --> Empty: EmptyResult
    
    Error --> Loading: Retry
    Empty --> Searching: Search
```

## Platform Implementation

### KMP Implementation

**Module**: `constructor-sdk/feature/learn/`

```
src/commonMain/kotlin/com/constructor/sdk/feature/learn/courselist/
├── domain/
│   └── model/
│       ├── Course.kt
│       └── CourseListError.kt
├── data/
│   └── repository/
│       └── CourseRepositoryImpl.kt
└── presentation/
    ├── CourseListViewModel.kt
    ├── CourseListState.kt
    ├── CourseListIntent.kt
    └── CourseListEffect.kt
```

**ViewModel Implementation**:
```kotlin
// @cpt-impl cpt-learn-course-list-viewmodel-kmp
class CourseListViewModel(
    private val loadCoursesUseCase: LoadCoursesUseCase,
    private val searchCoursesUseCase: SearchCoursesUseCase
) : ViewModel() {
    
    private val _state = MutableStateFlow(CourseListState())
    val state: StateFlow<CourseListState> = _state.asStateFlow()
    
    private val _effects = MutableSharedFlow<CourseListEffect>()
    val effects: SharedFlow<CourseListEffect> = _effects.asSharedFlow()
    
    fun processIntent(intent: CourseListIntent) {
        when (intent) {
            is CourseListIntent.LoadInitial -> loadInitial()
            is CourseListIntent.LoadMore -> loadMore()
            is CourseListIntent.Refresh -> refresh()
            is CourseListIntent.Search -> search(intent.query)
            is CourseListIntent.SelectCourse -> selectCourse(intent.courseId)
            is CourseListIntent.RetryAfterError -> loadInitial()
            is CourseListIntent.SelectCategory -> filterByCategory(intent.category)
        }
    }
}
```

### Android Implementation

**Module**: `android-app/feature/learn/`

```
src/main/kotlin/com/constructor/android/feature/learn/courselist/
├── ui/
│   ├── CourseListScreen.kt
│   └── components/
│       ├── CourseCard.kt
│       ├── CourseListContent.kt
│       ├── CourseListEmpty.kt
│       └── CourseListError.kt
└── navigation/
    └── CourseListNavigation.kt
```

**Compose Screen**:
```kotlin
// @cpt-impl cpt-learn-course-list-screen-android
@Composable
fun CourseListScreen(
    viewModel: CourseListViewModel = hiltViewModel(),
    onNavigateToCourse: (String) -> Unit
) {
    val state by viewModel.state.collectAsStateWithLifecycle()
    
    LaunchedEffect(Unit) {
        viewModel.effects.collect { effect ->
            when (effect) {
                is CourseListEffect.NavigateToCourseDetail -> 
                    onNavigateToCourse(effect.courseId)
                is CourseListEffect.ShowErrorToast -> 
                    // Show toast
                is CourseListEffect.ScrollToTop -> 
                    // Scroll to top
            }
        }
    }
    
    CourseListContent(
        state = state,
        onIntent = viewModel::processIntent
    )
}
```

### iOS Implementation

**Module**: `ios-app/Features/Learn/`

```
CourseList/
├── Views/
│   ├── CourseListView.swift
│   └── Components/
│       ├── CourseCardView.swift
│       ├── CourseListContentView.swift
│       ├── CourseListEmptyView.swift
│       └── CourseListErrorView.swift
├── ViewModels/
│   └── CourseListViewModelWrapper.swift
└── Navigation/
    └── CourseListCoordinator.swift
```

**SwiftUI View**:
```swift
// @cpt-impl cpt-learn-course-list-view-ios
struct CourseListView: View {
    @StateObject private var viewModel = CourseListViewModelWrapper()
    let onNavigateToCourse: (String) -> Void
    
    var body: some View {
        CourseListContentView(
            state: viewModel.state,
            onIntent: viewModel.processIntent
        )
        .onAppear {
            viewModel.processIntent(.LoadInitial())
        }
        .onReceive(viewModel.effects) { effect in
            switch effect {
            case let .NavigateToCourseDetail(courseId):
                onNavigateToCourse(courseId)
            case let .ShowErrorToast(message):
                // Show toast
            case .ScrollToTop:
                // Scroll to top
            }
        }
    }
}
```

## Acceptance Criteria

### Functional

| ID | Criterion | Platforms |
|----|-----------|-----------|
| AC-1 | Course list displays with thumbnail, title, instructor, duration | All |
| AC-2 | Pull-to-refresh updates course list | All |
| AC-3 | Infinite scroll loads next page | All |
| AC-4 | Search filters courses by title/description | All |
| AC-5 | Category filter narrows results | All |
| AC-6 | Tapping course navigates to detail | All |
| AC-7 | Cached courses show when offline | All |
| AC-8 | Error state shows retry option | All |
| AC-9 | Empty state shows when no courses match | All |

### Performance

| ID | Criterion | Threshold |
|----|-----------|-----------|
| PERF-1 | Initial load time | < 2s on 3G |
| PERF-2 | Scroll frame rate | 60fps |
| PERF-3 | Search response time | < 500ms after debounce |
| PERF-4 | Memory usage | < 50MB for 100 items |

### Accessibility

| ID | Criterion | Platforms |
|----|-----------|-----------|
| A11Y-1 | Course cards have accessibility labels | All |
| A11Y-2 | Loading states announced | All |
| A11Y-3 | Error messages accessible | All |
| A11Y-4 | Minimum touch target 48x48dp/44x44pt | Android/iOS |

## Definition of Done

### Development

- [ ] `cpt-learn-dod-course-list-kmp` KMP ViewModel, State, Intent, Effect implemented
- [ ] `cpt-learn-dod-course-list-android` Android Compose screen implemented
- [ ] `cpt-learn-dod-course-list-ios` iOS SwiftUI view implemented
- [ ] `cpt-learn-dod-course-list-tests` Unit tests for ViewModel (>80% coverage)
- [ ] `cpt-learn-dod-course-list-ui-tests` UI tests for critical flows

### Documentation

- [ ] IMPL.md updated with code mappings
- [ ] API documentation updated
- [ ] Accessibility audit passed

### Review

- [ ] Code review approved
- [ ] Design review approved
- [ ] QA sign-off received
