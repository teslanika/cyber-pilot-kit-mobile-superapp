# Feature Review Prompt (FEATURE-MOBILE)

Review the following PR changes for Mobile Feature Document.

## Focus Areas

### MVI Definition
- State is complete and immutable
- All user actions have corresponding Intents
- Effects cover all one-time events
- Initial state is valid

### CDSL Flows
- Actor flows are complete
- Steps are atomic and testable
- Error paths documented
- Edge cases covered

### Platform Sections
- KMP implementation section complete
- Android implementation section complete
- iOS implementation section complete
- Platform-specific edge cases documented

### Traceability
- References Epic design IDs
- References PRD story/AC IDs
- Cascading FR references present
- Flow/Algo/State/DoD IDs follow pattern

### Acceptance Criteria
- Per-platform criteria defined
- Testable and measurable
- Include performance criteria
- Include accessibility criteria

### Definition of Done
- All platforms covered
- Test requirements specified
- Documentation requirements listed

## Guidelines

Use `{checklist}` for detailed validation criteria.
Compare against `{template}` for structural compliance.

## Review Output

For each issue:
1. **Section**: Which section has the issue
2. **Severity**: CRITICAL / HIGH / MEDIUM / LOW
3. **Issue**: What's wrong or missing
4. **Fix**: How to address it
