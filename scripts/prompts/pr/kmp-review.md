# KMP (Kotlin Multiplatform) Code Review Prompt

Review the following PR changes for Kotlin Multiplatform shared code.

## Focus Areas

### Shared Logic
- Domain models are platform-agnostic
- Use cases contain business logic only
- Repository interfaces are in common code
- No platform-specific imports in commonMain

### Expect/Actual
- All expect declarations have corresponding actual implementations
- Actual implementations are correct for each platform
- No code duplication between platforms

### MVI Pattern
- State is immutable data class with defaults
- Intent is sealed class covering all user actions
- Effect is sealed class for one-time events
- ViewModel processes Intent → State + Effects

### Coroutines
- Proper Dispatcher usage (IO for network/disk, Main for UI)
- Structured concurrency (scope management)
- Exception handling in coroutines
- Flow collection lifecycle awareness

### State Management
- StateFlow for UI state
- SharedFlow for effects
- No memory leaks from uncancelled flows

### Code Quality
- Null safety (no unnecessary `!!`)
- Extension functions used appropriately
- Sealed classes for exhaustive when expressions

## Guidelines

Use `{checklist}` for detailed review criteria.
Refer to `{kmp_conventions}` for project-specific KMP patterns.

## Review Output

For each issue:
1. **Location**: File:line
2. **Severity**: CRITICAL / HIGH / MEDIUM / LOW
3. **Issue**: Description
4. **Fix**: Suggested solution
