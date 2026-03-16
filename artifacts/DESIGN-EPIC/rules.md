# DESIGN-EPIC Rules

**Artifact**: DESIGN-EPIC  
**Kit**: mobile-superapp  
**Level**: L2 (Epic)

**Dependencies**:
- `{design_epic_template}` — structural reference
- `{design_epic_checklist}` — semantic quality criteria
- `{prd_epic_template}` — parent Epic PRD reference
- `{design_subapp_template}` — parent SubApp DESIGN reference

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

- [ ] Load `{design_epic_template}` for structure
- [ ] Load `{design_epic_checklist}` for semantic guidance
- [ ] Read parent Epic PRD for requirements
- [ ] Read parent SubApp DESIGN for architectural context
- [ ] Load `{constraints}` for kit-level constraints
- [ ] Load `{cypilot_path}/.core/architecture/specs/traceability.md` for ID formats

---

## Requirements

### Structural

- [ ] DESIGN-EPIC follows `{design_epic_template}` structure
- [ ] All required sections present and non-empty:
  - Epic Overview (purpose, requirements coverage, drivers)
  - Component Architecture (diagram, screens, widgets)
  - State Management (state, intents, effects)
  - Data Flow (use cases, repositories, API contracts)
  - Navigation (entry/exit points, parameters)
  - Platform-Specific Considerations (Android, iOS, WebView)
  - Error Handling (error states, offline behavior)
  - Traceability
- [ ] All IDs follow `cpt-{subapp}-{epic}-{kind}-{slug}` convention
- [ ] References to Epic PRD are valid
- [ ] References to SubApp DESIGN are valid
- [ ] Component diagram present (Mermaid flowchart)
- [ ] No placeholder content (TODO, TBD, FIXME)
- [ ] No duplicate IDs within document

### Mobile-Specific

- [ ] Platform implementation table for each component:
  - KMP module location
  - Android component location
  - iOS component location
- [ ] MVI pattern documented with State, Intent, Effect classes
- [ ] Use cases have Input/Output types and step documentation
- [ ] Repository operations specify caching strategy
- [ ] Navigation includes deep link format
- [ ] Platform-specific sections for Android (Compose) and iOS (SwiftUI)
- [ ] WebView integration documented (if applicable)

### Traceability

- [ ] Requirements coverage table maps Epic PRD FRs to design responses
- [ ] ADR references provided for key decisions
- [ ] Screen/widget IDs link to Epic PRD components
- [ ] Use case IDs link to Epic PRD requirements
- [ ] Links to parent documents (Epic PRD, SubApp DESIGN)

### Versioning

- [ ] When editing existing DESIGN: increment version in document header
- [ ] When changing component definition: add `-v{N}` suffix to ID or increment

---

## Tasks

### Phase 1: Setup

- [ ] Load `{design_epic_template}` for structure
- [ ] Load `{design_epic_checklist}` for semantic guidance
- [ ] Read Epic PRD for requirements
- [ ] Read SubApp DESIGN for architectural patterns
- [ ] Identify which Epic FRs this DESIGN addresses

### Phase 2: Content Creation

Apply checklist semantics during creation:

| Checklist Category | Generation Task |
|-------------------|-----------------|
| Epic Overview | Document purpose, requirements coverage, ADRs |
| Component Architecture | Create component diagram, document screens/widgets |
| State Management | Define MVI State/Intent/Effect classes |
| Data Flow | Document use cases, repositories, API contracts |
| Navigation | Define entry/exit points, deep links, parameters |
| Platform-Specific | Document Android Compose, iOS SwiftUI specifics |
| Error Handling | Define error states, offline behavior |

**Partial Completion Handling**:

If DESIGN-EPIC cannot be completed in a single session:
1. Checkpoint progress with completed sections
2. Add `status: DRAFT` to document header
3. Mark incomplete sections with `INCOMPLETE: {reason}`
4. Document resumption point

### Phase 3: IDs and References

- [ ] Generate component overview ID: `cpt-{subapp}-epic-{epic}-component-overview`
- [ ] Generate screen IDs: `cpt-{subapp}-{epic}-screen-{slug}`
- [ ] Generate widget IDs: `cpt-{subapp}-{epic}-widget-{slug}`
- [ ] Generate state ID: `cpt-{subapp}-{epic}-state`
- [ ] Generate use case IDs: `cpt-{subapp}-{epic}-usecase-{slug}`
- [ ] Generate repo IDs: `cpt-{subapp}-{epic}-repo-{slug}`
- [ ] Generate API IDs: `cpt-{subapp}-{epic}-api-{slug}`
- [ ] Generate nav ID: `cpt-{subapp}-{epic}-nav`
- [ ] Generate platform IDs: `cpt-{subapp}-{epic}-android`, `cpt-{subapp}-{epic}-ios`
- [ ] Generate offline ID: `cpt-{subapp}-{epic}-offline`
- [ ] Link to Epic PRD requirements
- [ ] Reference SubApp DESIGN patterns
- [ ] Verify uniqueness with `cypilot list-ids`

### Phase 4: Quality Check

- [ ] Self-review against `{design_epic_checklist}` MUST HAVE items
- [ ] Ensure no MUST NOT HAVE violations
- [ ] Verify Epic PRD traceability
- [ ] Verify SubApp DESIGN alignment
- [ ] Verify MVI pattern is consistent

### Phase 5: Table of Contents

- [ ] Run `cypilot toc <path>` to generate/update Table of Contents
- [ ] Verify TOC is present and complete

---

## Validation

### Phase 1: Structural Validation

- [ ] Run `cypilot validate --artifact <path>` for:
  - Template structure compliance
  - ID format validation
  - Cross-reference validity
  - No placeholders

### Phase 2: Semantic Validation

- [ ] Read `{design_epic_checklist}` in full
- [ ] For each MUST HAVE item: check if requirement is met
- [ ] For each MUST NOT HAVE item: scan document for violations

### Phase 3: Epic-Specific Validation

- [ ] Component diagram accurately represents architecture
- [ ] All screens have platform implementation table
- [ ] All widgets have states and props documented
- [ ] MVI State/Intent/Effect are complete
- [ ] All use cases have steps documented
- [ ] Navigation includes deep link handling
- [ ] Error handling covers all error types
- [ ] Offline behavior is defined (if applicable)

### Validation Report Format

```
DESIGN-EPIC Validation Report
═════════════════════════════

Structural: PASS/FAIL
Semantic: PASS/FAIL (N issues)
Epic-Specific: PASS/FAIL (N issues)

Issues:
- [SEVERITY] CHECKLIST-ID: Description
```

---

## Error Handling

### Missing Epic PRD

- [ ] If parent Epic PRD not found:
  - Option 1: Run `/cypilot-generate PRD-EPIC` first (recommended)
  - Option 2: Continue without PRD (DESIGN will lack traceability)
  - Document "PRD pending" in DESIGN header

### Missing SubApp DESIGN

- [ ] If parent SubApp DESIGN not found:
  - Option 1: Run `/cypilot-generate DESIGN-SUBAPP` first
  - Option 2: Continue with assumptions documented
  - Document architectural assumptions made

### Escalation

- [ ] Ask user when uncertain about component boundaries
- [ ] Ask user when API contracts are unavailable
- [ ] Ask user when platform-specific behavior needs clarification

---

## Next Steps

### Options

- [ ] DESIGN-EPIC complete → `/cypilot-generate DECOMPOSITION-EPIC` — create features manifest
- [ ] Need architecture decision → `/cypilot-generate ADR` — document key decision
- [ ] PRD missing/incomplete → `/cypilot-generate PRD-EPIC` — create/update PRD first
- [ ] DESIGN needs revision → continue editing DESIGN-EPIC
- [ ] Ready for Feature → `/cypilot-generate FEATURE-MOBILE` — create feature specification
- [ ] SubApp DESIGN missing → `/cypilot-generate DESIGN-SUBAPP` — create SubApp DESIGN first
