# 1. Project Overview

**Oron Wallet** is a Flutter-based mobile wallet application built for secure digital asset management across multiple blockchain networks. The current codebase supports wallet creation and import, password-based authentication, dashboard portfolio views, transaction history, token and NFT management, send/receive flows, token swap flows, wallet switching, a built-in Web3 browser, and notification infrastructure.

This is a production-style mobile wallet codebase with real financial workflows, API integrations, local persistence, and security-sensitive user journeys.

# 2. My Role

I worked on the product as part of a shared engineering effort, with clear ownership over the wallet transaction experience and key user-facing flows.

I designed and implemented the **send and receive experience**, including the supporting transaction screens, token/network selection flow, confirmation steps, and the integration points required to move assets through the app.

I designed and implemented the **full swap flow**, including:
- swap page UI and UX
- token selection experience
- quote flow
- slippage and confirmation flow
- swap execution journey from one currency/token to another
- related screen design and interaction behavior

I also contributed to **dashboard UI enhancements**, improving the presentation and usability of wallet data and core actions.

I integrated the app’s swap and transfer flows with the relevant backend and transaction services, ensuring the mobile experience connected correctly to quote, execution, and confirmation logic.

I did **not** build every part of the application. Core areas such as **login, settings, and some authentication/account-management flows** were implemented by other contributors. My contribution was centered on **transactional product flows, swap UX, send/receive UX, and dashboard-facing UI improvements**.

# 3. Key Features

- Multi-network wallet experience
- Portfolio dashboard with wallet and asset visibility
- Send token flow with network/token selection and confirmation
- Receive flow for wallet funding
- Token swap flow with quote and confirmation
- Multi-wallet support and wallet switching
- Transaction history
- Custom token and NFT management
- Embedded Web3 browser
- Biometric and security-related app protections
- Push notification infrastructure

# 4. Tech Stack

- **Framework:** Flutter
- **Language:** Dart
- **State Management:** `provider`, `ChangeNotifier`
- **Networking:** `http`
- **Secure Storage / Local Storage:** `flutter_secure_storage`, `shared_preferences`, `sqflite`
- **Authentication / Device Security:** `local_auth`, `safe_device`, `flutter_windowmanager_plus`
- **Blockchain / Web3 Libraries:** `web3dart`, `flutter_ethers`, `uniswap`, `bip39`, `bip32`, `bitcoin_base`, `tron`
- **Notifications:** Firebase Core, Firebase Messaging, local notifications
- **UI Utilities:** `flutter_svg`, `cached_network_image`, `dropdown_search`, `lottie`

# 5. Architecture

The application follows a modular Flutter structure with separation between screens, services, models, local state, and shared widgets.

- `lib/pages/`: feature screens and user journeys
- `lib/api_services/`: backend and network integrations
- `lib/models/`: typed API models
- `lib/domain/`: local app state and persisted wallet context
- `lib/routes/`: centralized navigation
- `lib/common_widgets/`: reusable UI and helper components
- `lib/dbhelper/`: local browser/history storage

From my contribution area, the most important architectural layer was the connection between:
- swap/send/receive UI
- chain/token selection state
- API/service integration
- transaction confirmation and result handling

# 6. Core Functional Flows

**Send / Receive**
- User selects a network and asset
- Chooses the recipient or receive screen
- Confirms transaction details
- Completes the transfer through integrated transaction services

**Token Swap**
- User selects source token and target token
- Enters amount
- Reviews quote, rate, and slippage
- Confirms the transaction
- Executes the swap flow from one currency/token to another

**Dashboard Interaction**
- User views wallet balances and assets
- Navigates into transactional actions such as send, receive, and swap
- Uses improved UI pathways to move through wallet operations more efficiently

# 7. State Management

The app uses lightweight Flutter-native state management built around `Provider` and `ChangeNotifier`, with persistence through `SharedPreferences` and `FlutterSecureStorage`.

For the flows I worked on, state management was especially important for:
- selected wallet
- selected chain/network
- selected token
- transfer and swap context
- confirmation-stage data
- wallet/session continuity between transactional screens

# 8. API Integration

The application integrates with backend wallet services for:
- dashboard data
- token and NFT data
- transaction history
- wallet/account operations
- protected wallet actions

In my scope, I focused on integration for:
- send/receive transaction handling
- swap quote and execution flow
- chain-specific transfer behavior
- transaction confirmation and user feedback

# 9. Security Considerations (CRITICAL)

Because this is a wallet product, security is a core concern throughout the application.

High-level protections visible in the codebase include:
- authenticated API access using access tokens
- secure local storage for sensitive data
- biometric re-entry support
- screenshot blocking on sensitive screens
- password-gated access to private key / recovery operations
- device-integrity checks at startup
- controlled permission requests for camera and notifications

Within my areas of contribution, I worked inside these security-sensitive transaction flows and ensured the send/receive and swap journeys respected protected confirmation steps and secure handoff patterns already established in the application.

# 10. Performance Considerations

- Async loading for API-driven screens
- local persistence for faster session continuity
- reusable widgets for transactional UI consistency
- cached remote assets for token visuals
- focused state updates around wallet, network, and token selection
- dashboard refresh patterns for updated wallet views

# 11. Challenges & Solutions

**Designing a usable swap flow in a wallet context**
- I built the swap journey to make token-to-token exchange understandable, with clear selection, quote review, slippage handling, and confirmation steps.

**Balancing transaction complexity with mobile UX**
- I simplified send/receive and swap interactions into guided screens so the user could move through high-risk actions with clarity.

**Working in an existing shared codebase**
- I integrated my work into an application where some core account/auth/settings areas already existed, so my focus was extending the transaction layer and improving UI/UX without disrupting other modules.

**Improving dashboard usability**
- I enhanced parts of the dashboard experience to better surface wallet actions and make transactional entry points more intuitive.

# 12. Scalability & Maintainability

The project is maintainable because it already separates pages, services, routes, models, and shared widgets.

From my contribution area, maintainability came from:
- keeping swap flow UI separated from service logic
- structuring transactional screens as step-based flows
- reusing existing app state and route patterns
- extending the current architecture instead of bypassing it

A clear next step for long-term scale would be stronger test coverage and more formalized abstractions for chain-specific transaction execution.

# 13. Screenshots

### Wallet Dashboard
<img src="screenshots/Wallet Dashboard – Account Overview & Token Balances.png" width="600"/>

### Token Swap Flow
<img src="screenshots/Swap Screen – Token Selection & Amount Input.png" width="600"/>

### Swap Confirmation
<img src="screenshots/Swap Quote Screen – Price, Fees & Confirmation.png" width="600"/>

### Asset Selection
<img src="screenshots/Token Selection Modal – Search & Asset List.png" width="600"/>

For a full view of all application screens including dark mode and calling states, please visit the [Screenshots Gallery](./screenshots/README.md).


# 14. Disclaimer

This documentation reflects the **current codebase only** and is intentionally limited to what is implemented in this repository. It avoids exposing source code, secrets, credentials, or sensitive operational details.

Contribution ownership is described honestly: I was primarily responsible for the **send/receive flows, swap flow, swap page design/UI, and dashboard UI enhancements**, while **login, settings, and some authentication/account-management areas were implemented by other contributors**.

