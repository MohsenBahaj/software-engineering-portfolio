# Jaawer App

## Table of Contents

- [Project Overview](#1-project-overview)
- [My Role](#2-my-role)
- [Key Features](#3-key-features)
- [Tech Stack](#4-tech-stack)
- [Architecture](#5-architecture)
- [Core Functional Flows](#6-core-functional-flows)
- [State Management](#7-state-management)
- [API Integration](#8-api-integration)
- [Performance Considerations](#9-performance-considerations)
- [Challenges & Solutions](#10-challenges--solutions)
- [Security Considerations](#11-security-considerations)
- [Scalability & Maintainability](#12-scalability--maintainability)
- [External Links](#13-external-links)
- [Demo](#14-demo)
- [Screenshots](#15-screenshots)
- [Disclaimer](#16-disclaimer)


# 1. Project Overview

`Jaawer` is a production-oriented Flutter mobile application focused on roommate discovery, profile matching, and direct communication between users. The app supports the full lifecycle from onboarding and phone-based account verification to profile completion, roommate browsing, advanced filtering, subscription-gated messaging, realtime chat, moderation workflows, and account management.

The `bug-fix` branch reflects a stabilized version of the product with practical improvements around authentication flow, realtime messaging, unread state handling, profile completion, subscription verification, complaint management, and platform integrations for Android and iOS.

# 2. My Role

I designed and implemented the client-side architecture of the mobile application using Flutter with a clear separation between presentation, state, repository, and model layers.

I built the feature flows end to end, including authentication, OTP verification, complete-profile onboarding, roommate discovery, profile viewing, realtime chat, subscription handling, complaint reporting, support access, and account deletion.

I integrated the application with backend REST APIs and realtime socket events, implemented secure session persistence, handled multipart profile updates with images and structured payloads, and connected Firebase services for phone verification and push messaging.

I owned state management across the app using GetX controllers and reactive observables, including loading states, navigation, unread badge synchronization, filter state, and subscription state.

I handled production-facing mobile concerns such as Firebase initialization, push notification lifecycle, in-app purchase flows, app version checks, secure token storage, Android signing configuration, iOS entitlements/permissions, and bilingual localization support.

I also worked on performance and resilience by reducing duplicate conversation entries, preserving tab state, optimizing refresh behavior, supporting pagination, and adding reconnection-aware realtime behavior for messaging.

# 3. Key Features

- Phone-based registration and login with Firebase-backed OTP verification.
- Secure session persistence using device secure storage.
- First-launch onboarding flow with localized welcome screens.
- Complete-profile workflow with demographic, lifestyle, location, and roommate-preference data.
- Map-based location selection with support for direct Google Maps URL parsing.
- Roommate discovery feed with search, filtering, ranking, and compatibility percentage display.
- Detailed roommate profiles with personal info, lifestyle, preferences, property details, images, and location preview.
- Realtime one-to-one chat with unread badges, typing indicators, edit/delete message support, and read-state updates.
- Subscription-based messaging access using in-app purchases and backend purchase verification.
- Push notification infrastructure for chat and background messaging scenarios.
- Complaint submission, complaint tracking, complaint cancellation, and user support access.
- Language switching between Arabic and English with persisted locale.
- Account logout and guided account deletion flow with reason capture and user acknowledgements.
- Store version check flow to prompt users when a newer mobile release is available.

# 4. Tech Stack

- Flutter
- Dart
- GetX for state management, navigation, and dependency access
- Dio for REST networking and multipart requests
- Firebase Core
- Firebase Auth for phone verification
- Firebase Messaging for push notifications
- Flutter Local Notifications for local notification presentation
- `socket_io_client` for realtime chat events
- `flutter_secure_storage` for token and user-session persistence
- `in_app_purchase` and StoreKit support for subscription purchases
- Google Maps Flutter for map rendering
- Geolocator and Permission Handler for location access
- Image Picker for profile and place image uploads
- Cached Network Image for remote image rendering and caching
- `new_version_plus` for app update checks
- Android Gradle + iOS native configuration for platform delivery

# 5. Architecture

The branch follows a layered Flutter architecture with strong domain separation:

- `view/`: UI screens and widgets for auth, home, chat, profile, and settings.
- `viewmodel/`: GetX controllers that own screen state, validation, user actions, async workflows, and navigation.
- `data/repository/`: API-facing services for auth, chat, settings, subscriptions, roommates, and maps.
- `data/models/`: typed request/response/domain models for users, profiles, chats, subscriptions, complaints, and roommates.
- `auth/`: secure local session and preference storage.
- Cross-cutting services: notifications, websocket lifecycle, version checking, translations, and routing.

This structure keeps the UI lightweight while concentrating business logic inside controllers and integration logic inside repositories.

# 6. Core Functional Flows

## Authentication and Onboarding

Users land in a splash bootstrap that initializes Firebase, notifications, locale, and auth state. If a session exists, the app routes directly into the authenticated experience. If not, the app distinguishes between first launch and returning logged-out users to decide between welcome onboarding and login.

Registration is a two-step flow:

- submit account data to backend
- verify phone ownership through Firebase OTP
- exchange verified identity for backend JWT
- persist token and session data locally

Password reset is handled through a dedicated OTP-based reset flow.

## Profile Completion and Editing

After authentication, users complete a rich profile including age, nationality, city, preferred city, profession, lifestyle attributes, hobbies, personality traits, preferred neighborhoods, and roommate/place preferences.

If a user has a place to offer, the flow also captures:

- occupancy details
- price per person
- property description
- place photos
- place coordinates

Profile updates are sent as multipart form data, allowing structured JSON fields and image uploads in one request.

## Roommate Discovery

Users browse a roommate feed populated from the backend. Discovery supports:

- text search
- city and preferred-city filtering
- profession filtering
- nationality filtering
- age range filtering
- room-intent matching
- result scoring and prioritization

Each result exposes a compatibility percentage and a concise summary of the roommate’s housing situation.

## Messaging and Realtime Chat

Users can open a roommate profile and attempt to start a chat. Before entering chat, the app checks subscription/conversation rules. If permitted, it either opens an existing conversation or creates one on first message.

Chat supports:

- conversation list retrieval
- message history retrieval
- send text/media messages
- edit messages
- delete messages
- mark messages as read
- typing indicators
- realtime message delivery via websocket
- unread badge synchronization in bottom navigation

## Subscription Flow

The app loads product metadata from the store, initiates a purchase, listens to purchase updates, verifies completed purchases against the backend, refreshes subscription state, and restores past purchases when needed.

## Moderation and Settings

Users can:

- change language
- access premium plans
- open payment guidance
- contact support
- view complaints
- cancel pending complaints
- log out
- submit account deletion with an explicit reason

# 7. State Management

State management is implemented with GetX using `GetxController`, `Rx` observables, and `Obx` reactive widgets.

Key patterns in this branch:

- controller-owned form state and validation
- reactive loading and error states for network calls
- shared navigation/state through Get routing
- realtime unread badge propagation from chat controllers to the main tab shell
- observable filter state for roommate discovery
- reactive subscription purchase lifecycle handling
- explicit refresh methods for conversations and messages

This approach keeps feature logic centralized and minimizes widget-level state complexity.

# 8. API Integration

The mobile client integrates with domain-specific backend endpoints through dedicated repositories:

- Auth repository: registration, verification, login, password reset, profile fetch/update
- Roommate repository: roommate listing retrieval
- Chat repository: conversation lookup, conversation list, message send/edit/delete, read-state updates, subscription/conversation eligibility checks
- Settings repository: complaint creation/cancellation/listing and account deletion
- Subscription repository: backend purchase verification
- Maps repository: location resolution and Google Maps URL parsing support

The networking layer uses request timeouts, authorization headers from secure storage, multipart form submissions for profile data, and model parsing for structured responses.

# 9. Performance Considerations

- `IndexedStack` is used for the main tab shell so tab state is preserved instead of rebuilt on every navigation change.
- Chat conversation loading includes pagination controls and duplicate-prevention logic.
- Conversation refresh replaces or updates existing entries instead of blindly appending duplicates.
- Cached image loading reduces repeated network fetches for profile/place images.
- Realtime websocket updates reduce the need for constant polling.
- Filter logic runs client-side on fetched roommate data to keep interactions responsive.
- Scroll handling and post-frame updates improve chat UX after message send/receive.
- Notification suppression in foreground avoids redundant user interruption while the active UI is already visible.

# 10. Challenges & Solutions

## Realtime unread-state consistency

I solved unread badge drift by combining API-derived unread counts, websocket event listeners, direct tab-badge synchronization, and explicit read-state updates when conversations are opened.

## Chat duplication and refresh accuracy

I prevented duplicate conversations by checking IDs before insertion and replacing stale conversation entries with fresher payloads during refresh and pagination.

## Complex profile submission

I built a multipart profile update pipeline that supports mixed primitive values, JSON-encoded preference arrays, optional place-listing metadata, image uploads, and deleted-image tracking in a single update request.

## Cross-platform subscription handling

I implemented a purchase listener pipeline that handles product loading, purchase initiation, verification, restore flows, timeout protection, platform differences, and backend activation checks.

## Location usability

I improved location capture by supporting both direct map interaction and Google Maps URL parsing, which reduces friction for users who already have a shareable maps link.

## Auth bootstrap and first-run experience

I structured startup to distinguish between first launch, returning logged-out users, and authenticated users, which keeps onboarding, login, and profile completion behavior deterministic.

# 11. Security Considerations

- Auth tokens and sensitive session data are persisted using secure device storage rather than plain local storage.
- Backend API requests use bearer-token authorization.
- Account verification relies on Firebase phone authentication before backend token issuance.
- Account deletion requires explicit user acknowledgement and a deletion reason.
- Push token registration is authenticated before being sent to the backend.
- Profile and chat capabilities are scoped to authenticated sessions.

Security hardening opportunities visible in this branch:

- move third-party API secrets and environment-specific configuration out of client source and into a safer configuration strategy
- expand automated validation around edge-case authorization failures
- add stronger automated test coverage for auth, profile submission, and purchase verification paths

# 12. Scalability & Maintainability

The codebase is structured to scale feature development without collapsing into screen-level monoliths.

Maintainability strengths:

- feature/domain separation across views, controllers, repositories, and models
- reusable repositories for backend communication
- typed models for payload parsing
- localized strings centralized in a translation layer
- platform integrations isolated into service classes
- modular controllers for auth, chat, profile, roommate discovery, and subscriptions

Scalability strengths:

- conversation pagination already exists
- realtime transport is centralized in a singleton websocket service
- subscription logic is isolated from UI rendering
- profile payload construction is encapsulated in a dedicated model
- bilingual support is built into app bootstrap and persisted per user device state

Current engineering gap:

- automated testing is minimal in this branch, so future scaling would benefit from targeted unit, widget, and integration coverage around the critical production flows.

## 13. External Links

See [External Links](./links.md)

## 14. Demo

See full demo videos: [View Demo](./demo/README.md)

## 15. Screenshots

### Home
<img src="screenshots/home.jpg" width="600"/>

### Roommate Details
<img src="screenshots/roommate-details.jpg" width="600"/>

### Chat
<img src="screenshots/chat.jpg" width="600"/>

### Subscriptions
<img src="screenshots/subscriptions.jpg" width="600"/>

### Profile
<img src="screenshots/profile.jpg" width="600"/>


For a full view of all application screens including dark mode and calling states, please visit the [Screenshots Gallery](./screenshots/README.md).

## 16. Disclaimer

> This project’s source code is private due to client confidentiality. Detailed code walkthrough can be provided upon request.
