# IMPL-ANDROID Rules

**Artifact**: IMPL-ANDROID  
**Kit**: mobile-superapp  
**Level**: Implementation (Android UI)

**Dependencies**:
- `{impl_android_template}` — structural reference
- `{impl_android_checklist}` — semantic quality criteria
- `{feature_mobile_template}` — parent FEATURE reference
- `{design_epic_template}` — Epic DESIGN reference
- `{impl_kmp_template}` — KMP shared logic reference

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Requirements](#requirements)
3. [Tasks](#tasks)
4. [Validation](#validation)
5. [Error Handling](#error-handling)
6. [Next Steps](#next-steps)

---

## Prerequisites

### Load Dependencies

- [ ] Load `{impl_android_template}` for structure
- [ ] Load `{impl_android_checklist}` for semantic guidance
- [ ] Read parent FEATURE-MOBILE for CDSL specifications
- [ ] Read Epic DESIGN for component definitions
- [ ] Read IMPL-KMP for shared logic reference
- [ ] Load `{constraints}` for kit-level constraints
- [ ] Load `{cypilot_path}/.core/architecture/specs/traceability.md` for ID formats

---

## Requirements

### Structural

- [ ] IMPL-ANDROID follows `{impl_android_template}` structure
- [ ] All required sections present and non-empty:
  - Overview (module path)
  - References (Feature, Epic DESIGN, SubApp DESIGN)
  - Scope (what Android module implements)
  - Implementation Notes
  - Traceability Table
  - Directory Structure
  - Code Markers
  - Dependencies
  - Validation
- [ ] Module path is correct: `android-app/feature/{module}/`
- [ ] All references have valid paths and IDs
- [ ] No placeholder content (TODO, TBD, FIXME)

### Code Traceability

- [ ] Traceability Table maps:
  - Design Component ID → Code File → Implementation ID
- [ ] Implementation IDs follow format: `@cpt-impl cpt-android-{module}-{kind}-{slug}`
- [ ] All FEATURE CDSL steps (Section 3.2) have corresponding code markers
- [ ] All Epic DESIGN Android components (screens, widgets) have markers
- [ ] Code markers are in `@cpt-impl` comment format (Kotlin)

### Mobile-Specific (Android)

- [ ] Directory structure follows Android conventions:
  - `src/main/kotlin/com/constructor/android/feature/{module}/`
  - `ui/` — Compose screens and components
  - `ui/components/` — Reusable UI components
  - `navigation/` — Navigation graph
  - `di/` — Hilt dependency injection module
- [ ] Compose components documented:
  - `{Feature}Screen.kt` — Main screen composable
  - Widget components in `components/`
  - Navigation graph in `navigation/`
- [ ] Dependencies section includes:
  - KMP shared logic module reference
  - Common UI module reference
  - Common navigation module reference
- [ ] Kotlin/Compose code markers are valid comment syntax

### Versioning

- [ ] When editing existing IMPL: update traceability table
- [ ] When adding new components: add to traceability table
- [ ] When code moves: update file paths in table

---

## Tasks

### Phase 1: Setup

- [ ] Load `{impl_android_template}` for structure
- [ ] Load `{impl_android_checklist}` for semantic guidance
- [ ] Read FEATURE-MOBILE Section 3.2 (Android UI)
- [ ] Read Epic DESIGN for Android component definitions
- [ ] Read IMPL-KMP for shared ViewModel reference
- [ ] Identify all Android components to implement

### Phase 2: Content Creation

Apply checklist semantics during creation:

| Checklist Category | Generation Task |
|-------------------|-----------------|
| Overview | Document module path |
| References | Link to FEATURE, Epic DESIGN, SubApp DESIGN |
| Scope | Describe what this Android module implements |
| Implementation Notes | Document Compose patterns, navigation setup |
| Traceability Table | Map design IDs → code files → impl IDs |
| Directory Structure | Document module file organization |
| Code Markers | Show `@cpt-impl` marker examples |
| Dependencies | List KMP and common module dependencies |

**Traceability Table Format**:

| Design Component ID | Code File | Implementation ID |
|---------------------|-----------|-------------------|
| `cpt-{subapp}-{epic}-screen-{slug}` | `ui/{feature}/{Feature}Screen.kt` | `@cpt-impl cpt-android-{module}-screen-{slug}` |
| `cpt-{subapp}-{epic}-widget-{slug}` | `ui/{feature}/components/{Widget}.kt` | `@cpt-impl cpt-android-{module}-widget-{slug}` |
| `cpt-{subapp}-{epic}-nav` | `navigation/{Feature}NavGraph.kt` | `@cpt-impl cpt-android-{module}-nav-{slug}` |

**Partial Completion Handling**:

If IMPL-ANDROID cannot be completed in a single session:
1. Checkpoint progress with documented components
2. Mark incomplete mappings with `PENDING: {reason}`
3. Document resumption point

### Phase 3: IDs and References

- [ ] Link to FEATURE ID: `cpt-{subapp}-feature-{slug}`
- [ ] Link to Epic DESIGN ID: `cpt-{subapp}-epic-{epic}`
- [ ] Link to SubApp DESIGN ID: `cpt-{subapp}-design`
- [ ] Generate implementation IDs:
  - Screens: `@cpt-impl cpt-android-{module}-screen-{slug}`
  - Widgets: `@cpt-impl cpt-android-{module}-widget-{slug}`
  - Navigation: `@cpt-impl cpt-android-{module}-nav-{slug}`
  - UI logic: `@cpt-impl cpt-android-{module}-ui-{slug}`
- [ ] Verify implementation IDs match FEATURE CDSL `inst-android-` markers

### Phase 4: Quality Check

- [ ] Self-review against `{impl_android_checklist}` MUST HAVE items
- [ ] Ensure no MUST NOT HAVE violations
- [ ] Verify all FEATURE Section 3.2 steps have impl markers
- [ ] Verify all Epic DESIGN Android components are mapped
- [ ] Verify directory structure matches actual code
- [ ] Verify KMP dependency is correctly referenced

### Phase 5: Validation Commands

- [ ] Document `cypilot validate` command for this module
- [ ] Verify validation checks are appropriate

---

## Validation

### Phase 1: Structural Validation

- [ ] Run `cypilot validate --artifact android-app/feature/{module}/` for:
  - Template structure compliance
  - ID format validation
  - Cross-reference validity

### Phase 2: Code Marker Validation

- [ ] All design components have `@cpt-impl` markers in code
- [ ] All code markers reference valid design IDs
- [ ] No orphan markers (markers without design IDs)
- [ ] No missing markers (design IDs without code markers)

### Phase 3: Coverage Validation

- [ ] All FEATURE CDSL steps (Section 3.2) are implemented
- [ ] All Epic DESIGN Android components have implementations
- [ ] Coverage meets minimum threshold (e.g., 100% for P1 items)

### Phase 4: Android-Specific Validation

- [ ] Compose screens collect state with `collectAsStateWithLifecycle`
- [ ] Side effects are handled properly (LaunchedEffect, etc.)
- [ ] Navigation uses compose-navigation patterns
- [ ] Hilt injection is properly configured

### Validation Report Format

```
IMPL-ANDROID Validation Report
══════════════════════════════

Module: android-app/feature/{module}/

Structural: PASS/FAIL
Code Markers: PASS/FAIL (N markers found)
Coverage: X/Y components (Z%)

Issues:
- [SEVERITY] Description
```

---

## Error Handling

### Missing FEATURE-MOBILE

- [ ] If parent FEATURE-MOBILE not found:
  - Option 1: Run `/cypilot-generate FEATURE-MOBILE` first (recommended)
  - Option 2: Continue without FEATURE (traceability will be incomplete)
  - Document "FEATURE pending" in IMPL header

### Missing IMPL-KMP

- [ ] If IMPL-KMP not found:
  - Option 1: Run `/cypilot-generate IMPL-KMP` first (recommended)
  - Option 2: Continue without KMP reference
  - Document KMP dependency assumptions

### Code Marker Mismatches

- [ ] If code markers don't match design IDs:
  - Review FEATURE CDSL `inst-android-` markers
  - Update code markers to match
  - Or update IMPL traceability table to reflect actual code

### Escalation

- [ ] Ask user when Compose patterns deviate from FEATURE spec
- [ ] Ask user when code organization differs from template
- [ ] Ask user when Android-specific constraints arise

---

## Next Steps

### Options

- [ ] IMPL-ANDROID complete → Implement actual Kotlin/Compose code with `@cpt-impl` markers
- [ ] IMPL-ANDROID complete → `/cypilot-generate IMPL-IOS` — create iOS implementation reference
- [ ] IMPL-KMP missing → `/cypilot-generate IMPL-KMP` — create KMP reference first
- [ ] FEATURE missing → `/cypilot-generate FEATURE-MOBILE` — create FEATURE first
- [ ] IMPL needs revision → continue editing IMPL-ANDROID
- [ ] Ready for code review → validate markers with `cypilot validate`
