# GlassBoard

Cross-Department Dependency & Handoff Tracker

A mobile application that gives large organizations transparent visibility into
cross-module workflows via a verifiable digital handshake protocol.

## Tech Stack

- **Frontend**: React Native (TypeScript, Expo)
- **Auth**: Firebase Authentication with Custom Claims
- **Database**: Cloud Firestore
- **Realtime**: Firebase Realtime Database
- **Storage**: Firebase Storage
- **Push**: Firebase Cloud Messaging (FCM)
- **Functions**: Firebase Cloud Functions (Node.js)

## Project Structure

glassboard/
├── src/                    # React Native app source
│   ├── config/             # Firebase initialisation
│   ├── contexts/           # React context providers
│   ├── hooks/              # Custom React hooks
│   ├── navigation/         # React Navigation stack
│   ├── screens/            # Screen components
│   │   ├── auth/           # Login, register, onboarding
│   │   ├── modules/        # Phase 2+
│   │   ├── tasks/          # Phase 2+
│   │   ├── handshakes/     # Phase 4+
│   │   ├── files/          # Phase 7+
│   │   └── admin/          # Phase 6+
│   ├── types/              # Shared TypeScript types
│   └── utils/              # Helpers
├── functions/              # Firebase Cloud Functions
│   └── src/
│       ├── auth/           # onNewUser trigger
│       ├── handshakes/     # Phase 4+
│       ├── modules/        # Phase 3+
│       └── index.ts        # Function exports
└── firestore.rules         # Security rules

## Getting Started

### Prerequisites

- Node.js 18+
- Expo CLI: `npm install -g expo-cli`
- Firebase CLI: `npm install -g firebase-tools`

### 1. Clone and install

```bash
git clone https://github.com/your-org/glassboard.git
cd glassboard
npm install
```

### 2. Firebase setup

1. Create a project at [Firebase Console](https://console.firebase.google.com)
2. Enable Authentication (Email/Password)
3. Enable Cloud Firestore
4. Enable Realtime Database
5. Enable Storage
6. Enable Cloud Functions (Blaze plan required)
7. Copy `.env.example` to `.env` and fill in your Firebase config values

### 3. Deploy Firestore rules

```bash
firebase deploy --only firestore:rules
```

### 4. Deploy Cloud Functions

```bash
cd functions && npm install
cd .. && firebase deploy --only functions
```

### 5. Run the app

```bash
npx expo start
```

## Build Phases

| Phase | Status | Description |
|-------|--------|-------------|
| 1 | ✅ Complete | Auth + Org Setup |
| 2 | 🔲 Pending | Module & Task CRUD |
| 3 | 🔲 Pending | Realtime Progress |
| 4 | 🔲 Pending | Handshake System |
| 5 | 🔲 Pending | FCM Notifications |
| 6 | 🔲 Pending | Admin Dashboard |
| 7 | 🔲 Pending | File Versioning |
| 8 | 🔲 Pending | Polish & Security |

## RBAC Roles

| Role | Permissions |
|------|-------------|
| `member` | View own module, manage own tasks, participate in handshakes |
| `manager` | All member permissions + initiate handshakes, update progress |
| `admin` | Unrestricted read across all modules, create/delete modules |

## Security

- All handshake writes go through Cloud Functions (never direct client writes)
- Firestore Security Rules enforce RBAC at the database level
- Custom Claims carry `{ role, orgId, moduleId }` — no round-trips for role checks
- Token refresh required after any role change

## Contributing

See [CONTRIBUTING.md](./CONTRIBUTING.md). All PRs must pass the Firebase Emulator
security rules test suite before merge.
