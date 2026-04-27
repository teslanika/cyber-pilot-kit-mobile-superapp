# Technical Design — {Platform Name}

## Table of Contents

<!-- toc -->

<!-- /toc -->

## 1. Platform Architecture Overview

### 1.1 Architectural Vision

{2-3 paragraphs: Technical approach, key architectural decisions, design philosophy. How does this platform architecture satisfy the business goals from PRD?}

**ADRs**: `cpt-{platform}-adr-{slug}`

### 1.2 Architecture Drivers

Requirements that significantly influence platform architecture decisions.

#### Functional Drivers

| Requirement | Design Response |
|-------------|------------------|
| `cpt-{platform}-fr-{slug}` | {How platform architecture addresses this requirement} |

#### NFR Allocation

| NFR ID | NFR Summary | Allocated To | Design Response | Verification Approach |
|--------|-------------|--------------|-----------------|----------------------|
| `cpt-{platform}-nfr-{slug}` | {Brief NFR description} | {Layer/module/mechanism} | {How this design element realizes the NFR} | {How compliance is verified} |

### 1.3 Platform Layers

```
┌─────────────────────────────────────────────────────────────┐
│                    PRESENTATION LAYER                        │
│  ┌─────────────────┐  ┌─────────────────┐                   │
│  │   iOS Native    │  │  Android Native │    Native Shell   │
│  │    (SwiftUI)    │  │   (Compose)     │                   │
│  └────────┬────────┘  └────────┬────────┘                   │
│           │                    │                             │
│  ┌────────┴────────────────────┴────────┐                   │
│  │            WebView Container          │    Hybrid Layer  │
│  └───────────────────┬──────────────────┘                   │
└──────────────────────┼──────────────────────────────────────┘
                       │
┌──────────────────────┼──────────────────────────────────────┐
│                 APPLICATION LAYER                            │
│  ┌───────────────────┴──────────────────┐                   │
│  │              KMP SDK                  │    Shared Logic  │
│  │  ┌──────────┐  ┌──────────┐          │                   │
│  │  │ ViewModels│  │ Use Cases │         │                   │
│  │  └──────────┘  └──────────┘          │                   │
│  └──────────────────────────────────────┘                   │
└─────────────────────────────────────────────────────────────┘
                       │
┌──────────────────────┼──────────────────────────────────────┐
│                   DOMAIN LAYER                               │
│  ┌──────────────────────────────────────┐                   │
│  │           Domain Entities             │    Business Model │
│  │  ┌──────┐  ┌──────┐  ┌──────┐        │                   │
│  │  │Course│  │ User │  │ Task │        │                   │
│  │  └──────┘  └──────┘  └──────┘        │                   │
│  └──────────────────────────────────────┘                   │
└─────────────────────────────────────────────────────────────┘
                       │
┌──────────────────────┼──────────────────────────────────────┐
│               INFRASTRUCTURE LAYER                           │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐                   │
│  │ Network  │  │ Storage  │  │  Auth    │    Platform APIs  │
│  │  (Ktor)  │  │(SQLDelight)│ │(Keychain)│                   │
│  └──────────┘  └──────────┘  └──────────┘                   │
└─────────────────────────────────────────────────────────────┘
```

- [ ] `p1` - **ID**: `cpt-{platform}-layer-presentation`

| Layer | Responsibility | Technology | Location |
|-------|---------------|------------|----------|
| Presentation | Native UI shell, navigation, platform-specific UX | SwiftUI (iOS), Jetpack Compose (Android) | `ios-app/`, `android-app/` |
| Application | Business logic, state management, use cases | Kotlin Multiplatform (KMP) | `constructor-sdk/` |
| Domain | Core entities, business rules | Kotlin (shared) | `constructor-sdk/common/domain/` |
| Infrastructure | Network, storage, platform APIs | Ktor, SQLDelight, platform-specific | `constructor-sdk/common/data/` |

## 2. Cross-Platform Strategy

### 2.1 Native vs WebView Decision Matrix

- [ ] `p1` - **ID**: `cpt-{platform}-principle-hybrid`

| Content Type | Implementation | Rationale |
|--------------|----------------|-----------|
| Navigation shell | Native | Platform-native UX, gestures, animations |
| Authentication | Native | Security, biometrics, Keychain/KeyStore |
| Course content | WebView | Rapid updates, Learn 1.7 UI reuse |
| Assignments | WebView | Complex forms, Learn UI consistency |
| Calendar | Native | Platform integration, offline |
| Notifications | Native | Push, badges, system integration |
| Video calls (Groups) | WebView → Native | WebView MVP, native for reliability |
| Proctoring | Native | Camera, ML, device control |

**ADRs**: `cpt-{platform}-adr-hybrid-approach`

### 2.2 KMP SDK Scope

- [ ] `p1` - **ID**: `cpt-{platform}-principle-kmp-scope`

**Included in KMP SDK:**
- Domain entities and business logic
- Use cases and ViewModels (MVI)
- Repository interfaces and implementations
- Network clients (Ktor)
- Local storage (SQLDelight)
- Authentication state management

**NOT in KMP SDK (Platform-specific):**
- UI components (SwiftUI/Compose)
- Navigation implementation
- Platform permissions
- Push notification handling
- Biometric authentication
- WebView bridge

### 2.3 Code Sharing Matrix

| Module | Android | iOS | KMP Shared |
|--------|---------|-----|------------|
| Domain entities | ✗ | ✗ | ✓ |
| Business logic | ✗ | ✗ | ✓ |
| Network layer | ✗ | ✗ | ✓ |
| Storage layer | ✗ | ✗ | ✓ |
| ViewModels | ✗ | ✗ | ✓ |
| UI components | ✓ | ✓ | ✗ |
| Navigation | ✓ | ✓ | ✗ |
| Platform APIs | ✓ | ✓ | ✗ |

## 3. MiniApp Architecture

### 3.1 MiniApp Container Model

- [ ] `p1` - **ID**: `cpt-{platform}-component-miniapp-container`

```
┌─────────────────────────────────────────────────────────────┐
│                      HOST APPLICATION                        │
│  ┌──────────────────────────────────────────────────────┐   │
│  │                    KERNEL                             │   │
│  │  ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐        │   │
│  │  │  Auth  │ │Storage │ │Network │ │Notif.  │        │   │
│  │  └────────┘ └────────┘ └────────┘ └────────┘        │   │
│  └──────────────────────────────────────────────────────┘   │
│                           │                                  │
│  ┌────────────────────────┴─────────────────────────────┐   │
│  │                  MINIAPP REGISTRY                      │   │
│  └────────────────────────┬─────────────────────────────┘   │
│                           │                                  │
│  ┌─────────┬─────────┬────┴────┬─────────┬─────────┐       │
│  │ Student │ Proctor │ Groups  │Practice │  ...    │       │
│  │ MiniApp  │ MiniApp  │ MiniApp  │ MiniApp  │         │       │
│  └─────────┴─────────┴─────────┴─────────┴─────────┘       │
└─────────────────────────────────────────────────────────────┘
```

**MiniApp Interface Contract:**

```kotlin
interface MiniApp {
    val id: String
    val name: String
    val version: String
    
    fun initialize(kernel: Kernel)
    fun start(): MiniAppScreen
    fun handleDeepLink(uri: Uri): Boolean
    fun onBackground()
    fun onForeground()
    fun dispose()
}
```

### 3.2 MiniApp Lifecycle

- [ ] `p2` - **ID**: `cpt-{platform}-state-miniapp-lifecycle`

**States**: REGISTERED, INITIALIZING, READY, ACTIVE, BACKGROUND, DISPOSED

**Initial State**: REGISTERED

**Transitions**:
1. **FROM** REGISTERED **TO** INITIALIZING **WHEN** user selects MiniApp
2. **FROM** INITIALIZING **TO** READY **WHEN** initialization complete
3. **FROM** READY **TO** ACTIVE **WHEN** MiniApp screen displayed
4. **FROM** ACTIVE **TO** BACKGROUND **WHEN** app backgrounded or MiniApp switched
5. **FROM** BACKGROUND **TO** ACTIVE **WHEN** app foregrounded
6. **FROM** any **TO** DISPOSED **WHEN** MiniApp unloaded

### 3.3 MiniApp Communication

- [ ] `p2` - **ID**: `cpt-{platform}-component-miniapp-router`

**Inter-MiniApp Navigation:**
- Deep links: `constructor://miniapp/{miniapp-id}/path`
- Event bus for cross-MiniApp notifications
- Shared Kernel services (no direct MiniApp-to-MiniApp calls)

## 4. Shared Kernel

### 4.1 Authentication Module

- [ ] `p1` - **ID**: `cpt-{platform}-component-auth-kernel`

**Responsibilities:**
- SSO integration (SAML 2.0, OAuth 2.0, LDAP)
- Apple Sign In, Google Sign In
- E-Devlet authorization (Turkey)
- Token management (JWT, refresh)
- Biometric re-authentication
- Session state

**Technology**: KMP shared logic + platform-specific secure storage

**Location**: `constructor-sdk/common/auth/`

### 4.2 Storage Module

- [ ] `p1` - **ID**: `cpt-{platform}-component-storage-kernel`

**Responsibilities:**
- Local database (SQLDelight)
- Secure credential storage (Keychain/KeyStore)
- File storage (downloaded content)
- Cache management

**Technology**: SQLDelight (KMP), platform-specific secure storage

**Location**: `constructor-sdk/common/data/storage/`

### 4.3 Networking Module

- [ ] `p1` - **ID**: `cpt-{platform}-component-network-kernel`

**Responsibilities:**
- HTTP client (Ktor)
- API request/response handling
- Authentication header injection
- Retry logic and error handling
- Offline queue

**Technology**: Ktor (KMP)

**Location**: `constructor-sdk/common/data/network/`

### 4.4 Notifications Module

- [ ] `p2` - **ID**: `cpt-{platform}-component-notifications-kernel`

**Responsibilities:**
- Push token registration (FCM/APNS)
- In-app notification center
- Deep link handling from notifications
- Badge management

**Technology**: Platform-specific (FCM/APNS) + KMP shared logic

**Location**: `constructor-sdk/common/notifications/`, `ios-app/Notifications/`, `android-app/notifications/`

## 5. External Integrations

### 5.1 Learn Backend

- [ ] `p1` - **ID**: `cpt-{platform}-integration-learn`

**Direction**: Required from Learn backend

**Protocol**: REST API, JSON

**Endpoints**: `/api/v1/mobile/learn/*`

**Authentication**: JWT Bearer token

**Key Contracts:**
- Course catalog
- Assignment list and submission
- Grades
- Calendar events

### 5.2 Proctor Service

- [ ] `p2` - **ID**: `cpt-{platform}-integration-proctor`

**Direction**: Required from Proctor backend

**Protocol**: REST API + WebSocket (real-time)

**Key Contracts:**
- Session management
- Face recognition events
- Recording upload
- Violation reporting

### 5.3 Groups Service

- [ ] `p2` - **ID**: `cpt-{platform}-integration-groups`

**Direction**: Required from Groups (mediasoup) backend

**Protocol**: WebSocket (signaling) + WebRTC (media)

**Key Contracts:**
- Room join/leave
- Media stream management
- Screen sharing
- Participant management

### 5.4 Notification Service

- [ ] `p2` - **ID**: `cpt-{platform}-integration-notifications`

**Direction**: Required from Platform Notification Engine

**Protocol**: FCM (Android), APNS (iOS)

**Key Contracts:**
- Push token registration
- Notification payload format
- Deep link format

## 6. Traceability

- **PRD**: [PRD.md](./PRD.md)
- **ADRs**: [adr/](./adr/)
- **DECOMPOSITION**: [DECOMPOSITION.md](./DECOMPOSITION.md)
- **MiniApps**: [miniapps/](../miniapps/)
