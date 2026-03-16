# Design Review Prompt (Platform / SubApp / Epic)

Review the following PR changes for Design Document.

## Focus Areas

### Architecture
- Correct hierarchy level (Platform, SubApp, or Epic)
- Components clearly defined with responsibilities
- Interfaces specified
- Data flow documented

### Mobile Architecture
- KMP shared module structure
- Platform-specific implementations justified
- MVI pattern applied consistently
- Navigation architecture defined

### Technical Quality
- No contradictions with parent design
- Component boundaries clear
- Dependencies documented
- Scalability considered

### Traceability
- References PRD FR/NFR IDs
- References parent design IDs (if SubApp/Epic)
- Design IDs follow kit conventions

### Mobile-Specific Concerns
- Offline architecture
- State persistence strategy
- Deep linking architecture
- Push notification handling

### Performance Design
- Caching strategy
- Lazy loading approach
- Background task handling
- Memory management approach

## Guidelines

Use `{checklist}` for detailed validation criteria.
Compare against `{template}` for structural compliance.
Reference `{architecture}` for existing architecture documentation.

## Review Output

For each issue:
1. **Section**: Which section has the issue
2. **Severity**: CRITICAL / HIGH / MEDIUM / LOW
3. **Issue**: What's wrong or inconsistent
4. **Fix**: How to address it
