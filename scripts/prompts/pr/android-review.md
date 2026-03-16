# Android (Jetpack Compose) Code Review Prompt

Review the following PR changes for Android Compose UI code.

## Focus Areas

### Compose Best Practices
- Composable functions are stateless where possible
- State hoisting applied correctly
- `remember` and `rememberSaveable` used appropriately
- No side effects in composition

### State Collection
- `collectAsStateWithLifecycle()` for StateFlow
- Proper lifecycle handling for effects
- LaunchedEffect scoped correctly

### Performance
- Avoid unnecessary recompositions
- Use `key()` for list items
- Derivation with `derivedStateOf` where applicable
- Large lists use LazyColumn/LazyRow

### Hilt/DI
- `@HiltViewModel` annotation present
- `hiltViewModel()` used in Composables
- Module bindings are correct

### Navigation
- NavController used correctly
- Deep links configured if needed
- Back stack handled properly

### Resources
- Strings in resources (no hardcoded text)
- Dimensions in resources
- Theme/colors from MaterialTheme

### Accessibility
- ContentDescription for images
- Semantic properties set
- Touch targets adequate (48dp minimum)

## Guidelines

Use `{checklist}` for detailed review criteria.
Refer to `{compose_guidelines}` for project-specific Compose patterns.

## Review Output

For each issue:
1. **Location**: File:line
2. **Severity**: CRITICAL / HIGH / MEDIUM / LOW
3. **Issue**: Description
4. **Fix**: Suggested solution
