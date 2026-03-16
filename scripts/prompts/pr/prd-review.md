# PRD Review Prompt (Platform / SubApp / Epic)

Review the following PR changes for Product Requirements Document.

## Focus Areas

### Structure
- Correct hierarchy level (Platform, SubApp, or Epic)
- All required sections present per template
- IDs follow kit conventions

### Requirements Quality
- Requirements are testable and measurable
- No ambiguous language ("should", "may", "might")
- Clear acceptance criteria
- Edge cases documented

### Mobile-Specific
- Platform considerations (iOS, Android, KMP)
- Offline requirements defined
- Performance requirements specified
- Accessibility requirements included

### Traceability
- References to parent level (if SubApp/Epic)
- FR/NFR IDs are unique and follow pattern
- Cascading requirements properly linked

### Completeness
- All actors defined
- Use cases cover happy path and errors
- Non-functional requirements comprehensive
- Constraints clearly stated

## Guidelines

Use `{checklist}` for detailed validation criteria.
Compare against `{template}` for structural compliance.

## Review Output

For each issue:
1. **Section**: Which section has the issue
2. **Severity**: CRITICAL / HIGH / MEDIUM / LOW
3. **Issue**: What's wrong or missing
4. **Fix**: How to address it
