# iOS (SwiftUI) Code Review Prompt

Review the following PR changes for iOS SwiftUI code.

## Focus Areas

### SwiftUI Best Practices
- Views are small and focused
- State management uses appropriate wrappers
- `@StateObject` for owned objects
- `@ObservedObject` for injected objects

### KMP Integration
- ViewModelWrapper pattern implemented correctly
- Combine publishers for KMP StateFlow
- Memory management (no retain cycles)
- Cancellation handled properly

### State Management
- `@Published` properties in ObservableObject
- Binding usage is correct
- State flows down, actions flow up

### Performance
- Avoid expensive operations in body
- Use `@ViewBuilder` where appropriate
- Lazy stacks for large lists
- Image caching implemented

### Navigation
- NavigationStack/NavigationLink usage
- Coordinator pattern if applicable
- Deep links handled

### Concurrency
- `@MainActor` for UI updates
- Task cancellation on disappear
- Proper async/await usage

### Resources
- Localized strings
- Asset catalogs for images
- Colors from asset catalog or extension

### Accessibility
- accessibilityLabel for non-text elements
- accessibilityHint where helpful
- VoiceOver tested

## Guidelines

Use `{checklist}` for detailed review criteria.
Refer to `{swiftui_guidelines}` for project-specific SwiftUI patterns.

## Review Output

For each issue:
1. **Location**: File:line
2. **Severity**: CRITICAL / HIGH / MEDIUM / LOW
3. **Issue**: Description
4. **Fix**: Suggested solution
