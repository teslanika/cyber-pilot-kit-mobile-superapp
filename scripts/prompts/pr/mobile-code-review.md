# Mobile Code Review Prompt

Review the following PR code changes for mobile platforms (KMP, Android, iOS).

## Focus Areas

### Architecture & Patterns
- MVI pattern implementation (State, Intent, Effect)
- Proper separation of concerns (domain, data, presentation)
- Dependency injection correctness
- Navigation patterns

### Platform-Specific
- **KMP**: Expect/actual implementations, shared logic correctness
- **Android**: Compose best practices, lifecycle handling
- **iOS**: SwiftUI patterns, KMP wrapper integration

### Quality
- Correctness, edge cases, and error handling
- Code style and idiomatic patterns
- Performance implications (memory, battery, startup)
- Test coverage

### Security
- Data handling (no PII logging, secure storage)
- Network security (certificate pinning, secure connections)
- Input validation

### Traceability
- `@cpt-impl` markers present for new code
- Markers reference valid FEATURE-MOBILE IDs
- No orphaned markers

## Guidelines

Use `{checklist}` as the structured review guide when available.
Refer to `{coding_guidelines}` for mobile-specific conventions.
Refer to `{security_guidelines}` for security requirements.

## Review Output

For each issue found:
1. **Location**: File and line number
2. **Severity**: CRITICAL / HIGH / MEDIUM / LOW
3. **Category**: Architecture / Performance / Security / Style / Test
4. **Description**: What's wrong
5. **Suggestion**: How to fix
