# Greenfield Guide — Mobile SuperApp

Use this guide when starting a new mobile app from scratch.

All prompts work through the `cypilot` skill — enable it with `cypilot on` and use natural language prompts.

## Goal

Create a validated 4-level architecture baseline before writing mobile code.

## What You Will Produce

Cypilot artifacts registered in `{cypilot_path}/config/artifacts.toml`:

| Level | Artifacts | Default Location |
|-------|-----------|------------------|
| L0: Platform | PRD-PLATFORM, DESIGN-PLATFORM, DECOMPOSITION-PLATFORM | `architecture/platform/` |
| L1: SubApp | PRD-SUBAPP, DESIGN-SUBAPP, DECOMPOSITION-SUBAPP | `architecture/subapps/{slug}/` |
| L2: Epic | PRD-EPIC, DESIGN-EPIC, DECOMPOSITION-EPIC | `architecture/subapps/{subapp}/epics/{slug}/` |
| L3: Feature | FEATURE-MOBILE | `architecture/subapps/{subapp}/epics/{epic}/features/{slug}.md` |

---

## Workflow Sequence

### Phase 1: Platform Level (L0)

#### 1.1 PRD-PLATFORM

**Create**

| Prompt | What happens |
|--------|--------------|
| `cypilot make PRD-PLATFORM` | Creates platform PRD interactively |
| `cypilot make PRD-PLATFORM for Constructor SuperApp` | Creates PRD with context |
| `cypilot draft PRD-PLATFORM from README` | Extracts from existing docs |

**Provide context:**
```
cypilot make PRD-PLATFORM for Constructor SuperApp
Context:
- Product: Educational mobile platform
- Users: students, instructors, admins
- SubApps: Learn, Assess, Communicate
- Platforms: iOS (SwiftUI), Android (Compose), shared KMP
- Key NFRs: offline-first, <3s launch, 60fps animations
```

**Validate**

| Prompt | What happens |
|--------|--------------|
| `cypilot validate PRD-PLATFORM` | Full validation |
| `cypilot validate PRD-PLATFORM semantic` | Semantic only |
| `cypilot validate PRD-PLATFORM structural` | Structural only |

#### 1.2 DESIGN-PLATFORM

**Create**

| Prompt | What happens |
|--------|--------------|
| `cypilot make DESIGN-PLATFORM` | Creates platform architecture |
| `cypilot make DESIGN-PLATFORM from PRD-PLATFORM` | Transforms PRD into architecture |

**Provide context:**
```
cypilot make DESIGN-PLATFORM
Context:
- Architecture: KMP shared + native UI
- Shared modules: constructor-sdk (domain, data, presentation)
- Native apps: android-app (Compose), ios-app (SwiftUI)
- DI: Koin (KMP), Hilt (Android)
- Navigation: Decompose (KMP) + platform coordinators
- Offline: Room (Android), Core Data (iOS), shared cache strategy
```

**Validate**

| Prompt | What happens |
|--------|--------------|
| `cypilot validate DESIGN-PLATFORM` | Full validation |
| `cypilot validate DESIGN-PLATFORM refs` | Cross-references to PRD |

#### 1.3 DECOMPOSITION-PLATFORM

**Create**

| Prompt | What happens |
|--------|--------------|
| `cypilot make DECOMPOSITION-PLATFORM` | Creates SubApp breakdown |
| `cypilot decompose platform into subapps` | Alternative phrasing |

**Provide context:**
```
cypilot make DECOMPOSITION-PLATFORM
Context:
- SubApps:
  - learn (course catalog, progress, certificates)
  - assess (exams, proctoring, results)
  - communicate (chat, notifications, announcements)
- Shared: auth, settings, profile
```

**Validate**

| Prompt | What happens |
|--------|--------------|
| `cypilot validate DECOMPOSITION-PLATFORM` | Full validation |
| `cypilot validate DECOMPOSITION-PLATFORM refs` | Cross-references |

---

### Phase 2: SubApp Level (L1)

For each SubApp from DECOMPOSITION-PLATFORM:

#### 2.1 PRD-SUBAPP

**Create**

| Prompt | What happens |
|--------|--------------|
| `cypilot make PRD-SUBAPP for learn` | Creates Learn SubApp PRD |
| `cypilot make PRD-SUBAPP for assess` | Creates Assess SubApp PRD |

**Provide context:**
```
cypilot make PRD-SUBAPP for learn
Context:
- SubApp: Learn
- Parent: cpt-platform (references platform FRs)
- Capabilities: course browsing, enrollment, progress tracking, certificates
- Actors: student, instructor
- Offline requirements: course content, progress sync
```

**Validate**

| Prompt | What happens |
|--------|--------------|
| `cypilot validate PRD-SUBAPP for learn` | Full validation |
| `cypilot validate PRD-SUBAPP for learn refs` | References to platform |

#### 2.2 DESIGN-SUBAPP

**Create**

| Prompt | What happens |
|--------|--------------|
| `cypilot make DESIGN-SUBAPP for learn` | Creates SubApp architecture |
| `cypilot make DESIGN-SUBAPP for learn from PRD-SUBAPP` | From SubApp PRD |

**Provide context:**
```
cypilot make DESIGN-SUBAPP for learn
Context:
- SubApp: Learn
- KMP modules: learn-domain, learn-data, learn-presentation
- Features: course-catalog, course-player, progress-tracker
- Data: CourseRepository, ProgressRepository
- Navigation: LearnNavGraph, LearnCoordinator
```

**Validate**

| Prompt | What happens |
|--------|--------------|
| `cypilot validate DESIGN-SUBAPP for learn` | Full validation |
| `cypilot validate DESIGN-SUBAPP for learn refs` | References |

#### 2.3 DECOMPOSITION-SUBAPP

**Create**

| Prompt | What happens |
|--------|--------------|
| `cypilot make DECOMPOSITION-SUBAPP for learn` | Creates Epic breakdown |
| `cypilot decompose subapp learn into epics` | Alternative phrasing |

**Provide context:**
```
cypilot make DECOMPOSITION-SUBAPP for learn
Context:
- Epics:
  - course-catalog (browse, search, filter, enroll)
  - course-player (video, content, quizzes)
  - progress-tracker (completion, achievements, certificates)
```

---

### Phase 3: Epic Level (L2)

For each Epic from DECOMPOSITION-SUBAPP:

#### 3.1 PRD-EPIC

| Prompt | What happens |
|--------|--------------|
| `cypilot make PRD-EPIC for course-catalog` | Creates Epic requirements |
| `cypilot validate PRD-EPIC for course-catalog` | Validates Epic PRD |

**Provide context:**
```
cypilot make PRD-EPIC for course-catalog
Context:
- Epic: Course Catalog
- SubApp: Learn
- User stories: browse courses, search, filter by category, view details, enroll
- Acceptance criteria per story
```

#### 3.2 DESIGN-EPIC

| Prompt | What happens |
|--------|--------------|
| `cypilot make DESIGN-EPIC for course-catalog` | Creates Epic architecture |
| `cypilot validate DESIGN-EPIC for course-catalog` | Validates Epic design |

**Provide context:**
```
cypilot make DESIGN-EPIC for course-catalog
Context:
- Components: CourseListViewModel, CourseDetailViewModel, CourseRepository
- Data flow: API → Repository → ViewModel → UI
- States: Loading, Content, Empty, Error
- Navigation: CourseList → CourseDetail → Enrollment
```

#### 3.3 DECOMPOSITION-EPIC

| Prompt | What happens |
|--------|--------------|
| `cypilot make DECOMPOSITION-EPIC for course-catalog` | Creates Feature breakdown |
| `cypilot decompose epic course-catalog into features` | Alternative phrasing |

**Provide context:**
```
cypilot make DECOMPOSITION-EPIC for course-catalog
Context:
- Features:
  - course-list (browse, pagination, pull-to-refresh)
  - course-search (search, filters, suggestions)
  - course-detail (info, syllabus, reviews, enrollment)
```

---

### Phase 4: Feature Level (L3)

For each Feature from DECOMPOSITION-EPIC:

#### 4.1 FEATURE-MOBILE

| Prompt | What happens |
|--------|--------------|
| `cypilot make FEATURE-MOBILE for course-list` | Creates feature design |
| `cypilot validate FEATURE-MOBILE for course-list` | Validates feature |

**Provide context:**
```
cypilot make FEATURE-MOBILE for course-list
Context:
- Feature: Course List
- Epic: Course Catalog
- Actor flows: browse courses, pull to refresh, load more
- States: Loading, Content(courses), Empty, Error(message)
- Intents: Load, Refresh, LoadMore, SelectCourse
- Effects: NavigateToCourse, ShowError
- Edge cases: empty list, network error, pagination end
```

#### 4.2 CODE Implementation

**Implement all platforms**

| Prompt | What happens |
|--------|--------------|
| `cypilot implement course-list` | Generates KMP + Android + iOS |
| `cypilot implement course-list step by step` | With confirmation |
| `cypilot implement course-list tests first` | TDD approach |

**Implement specific platform**

| Prompt | What happens |
|--------|--------------|
| `cypilot implement course-list kmp` | KMP ViewModel, UseCase, Repository |
| `cypilot implement course-list android` | Compose UI |
| `cypilot implement course-list ios` | SwiftUI + KMP wrapper |

**Validate code**

| Prompt | What happens |
|--------|--------------|
| `cypilot validate code for course-list` | Validates markers and coverage |
| `cypilot validate code coverage for course-list` | Coverage report |
| `cypilot validate code orphans` | Finds orphaned markers |

---

## Iteration Rules

1. **Design flows down**: Platform → SubApp → Epic → Feature
2. **Changes propagate up**: If feature needs platform change, update platform first
3. **Validate before implementing**: Always validate artifact before using it
4. **Code matches design**: If code contradicts design, fix design at appropriate level

---

## Quick Reference

### Full Pipeline

| Step | Generate | Validate |
|------|----------|----------|
| 1 | `cypilot make PRD-PLATFORM` | `cypilot validate PRD-PLATFORM` |
| 2 | `cypilot make DESIGN-PLATFORM` | `cypilot validate DESIGN-PLATFORM` |
| 3 | `cypilot make DECOMPOSITION-PLATFORM` | `cypilot validate DECOMPOSITION-PLATFORM` |
| 4 | `cypilot make PRD-SUBAPP for {subapp}` | `cypilot validate PRD-SUBAPP for {subapp}` |
| 5 | `cypilot make DESIGN-SUBAPP for {subapp}` | `cypilot validate DESIGN-SUBAPP for {subapp}` |
| 6 | `cypilot make DECOMPOSITION-SUBAPP for {subapp}` | `cypilot validate DECOMPOSITION-SUBAPP for {subapp}` |
| 7 | `cypilot make PRD-EPIC for {epic}` | `cypilot validate PRD-EPIC for {epic}` |
| 8 | `cypilot make DESIGN-EPIC for {epic}` | `cypilot validate DESIGN-EPIC for {epic}` |
| 9 | `cypilot make DECOMPOSITION-EPIC for {epic}` | `cypilot validate DECOMPOSITION-EPIC for {epic}` |
| 10 | `cypilot make FEATURE-MOBILE for {feature}` | `cypilot validate FEATURE-MOBILE for {feature}` |
| 11 | `cypilot implement {feature}` | `cypilot validate code for {feature}` |

### Validation Modes

Append to any `validate` command:
- `semantic` — content quality, completeness, mobile patterns
- `structural` — format, IDs, template compliance
- `refs` — cross-references across levels
- `quick` — critical issues only (fast)
