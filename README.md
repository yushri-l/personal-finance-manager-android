<div align="center">

# Personal Finance Manager

### A multi-source income & expense tracker built for irregular earners

[![Kotlin](https://img.shields.io/badge/Kotlin-100%25-7F52FF?logo=kotlin&logoColor=white)](https://kotlinlang.org/)
[![Jetpack Compose](https://img.shields.io/badge/Jetpack%20Compose-Material%203-4285F4?logo=jetpackcompose&logoColor=white)](https://developer.android.com/jetpack/compose)
[![Architecture](https://img.shields.io/badge/Architecture-MVVM-blue)](https://developer.android.com/topic/architecture)
[![Firebase](https://img.shields.io/badge/Firebase-Auth%20%2B%20Firestore-FFCA28?logo=firebase&logoColor=black)](https://firebase.google.com/)
[![Min SDK](https://img.shields.io/badge/Min%20SDK-26-3DDC84?logo=android&logoColor=white)](https://developer.android.com/about/versions/oreo)
[![Status](https://img.shields.io/badge/Status-In%20Development-orange)]()

**SE3092 — Platform Based Development · SLIIT 2026 Semester 1**

</div>

---

## Overview

A personal finance management Android application designed for users with **irregular, multi-source income** — primarily junior software engineers in Sri Lanka who earn from a fixed salary, freelance projects, online ad revenue paid in USD, and cryptocurrency trading.

The app is built around a documented user persona, **Kavindu Silva** — a 25-year-old junior software engineer who has earned over LKR 1.6M in 12 months but saved only LKR 11,200. Existing tools have failed him because they assume a single income source, a fixed monthly budget, and a single currency. Our solution is designed specifically for his reality.

> **The challenge:** build a finance app Kavindu would actually open every day — and still be using six months from now.

---

## The Problem

Kavindu has tried four different tools to track his finances. All four failed within two weeks:

| Tool | Why it failed |
|---|---|
| Google Sheets | Manual entry overhead; formulas broke after row inserts |
| Play Store budgeting app | USD only, no cloud sync, assumed single income source |
| Notes app + bank exports | Became unreadable after four days |
| Bank's spending summary | Missed cash and secondary accounts; miscategorised transactions |

A solution must handle: **irregular multi-source income**, **multi-currency entries**, **frictionless daily input**, **goal tracking**, and **discretionary-vs-committed spending visibility**.

---

## Key Features

- Multi-source income tracking — Salary · Freelance · AdSense · Crypto
- Multi-currency support with FX rate snapshots — LKR · USD · USDT · ETH
- Frictionless expense entry — under two taps after opening the app
- Smart category memory and vendor-to-category auto-suggestions
- Real-time dashboard with live goal progress
- Discretionary vs Committed spending breakdown
- Subscription tracker and freelance invoice status
- Offline-first with cloud sync via Firebase

---

## Tech Stack

| Layer | Technology |
|---|---|
| Language | Kotlin (100%) |
| UI Framework | Jetpack Compose · Material 3 |
| Architecture | MVVM (UI → ViewModel → Repository → Model) |
| Navigation | Navigation Compose (single-activity) |
| State Management | StateFlow |
| Async / Concurrency | Kotlin Coroutines |
| Authentication | Firebase Authentication |
| Database | Cloud Firestore |
| Local Cache | Room |
| Dependency Injection | Hilt |
| Build System | Gradle (Kotlin DSL) |
| Min SDK | 26 (Android 8.0 Oreo) |
| Target SDK | 34+ |

---

## Architecture

The application strictly follows the **MVVM** pattern with a unidirectional data flow:

```
       UI Layer (Composable)
                │
        observes StateFlow
                │
              ViewModel
                │
       suspend function calls
                │
            Repository
                │
        ┌───────┴───────┐
        ▼               ▼
    Firestore         Room
   (remote)         (local cache)
```

**Architectural principles**

- No business logic in Composable functions
- ViewModels never reference Android UI classes
- All async work is launched in `viewModelScope` using Coroutines
- The UI reads from Room as the single source of truth; Firestore listeners hydrate it
- Firestore Security Rules enforce per-user data scoping

A detailed architecture diagram is available in [`docs/architecture.md`](docs/architecture.md).

---

## Project Structure

```
personal-finance-manager-android/
├── app/
│   ├── src/main/java/com/sliit/pfm/
│   │   ├── data/                # Models, repositories, Firestore + Room sources
│   │   ├── di/                  # Hilt modules
│   │   ├── ui/
│   │   │   ├── auth/            # Sign-up, sign-in
│   │   │   ├── dashboard/       # Home screen, charts
│   │   │   ├── income/          # Income features
│   │   │   ├── expense/         # Expense features
│   │   │   ├── goal/            # Goal tracking
│   │   │   ├── components/      # Reusable composables
│   │   │   └── theme/           # Material 3 theme tokens
│   │   └── PfmApplication.kt
│   └── src/main/res/            # Icons and string resources (no XML layouts)
├── docs/                        # Design documents, diagrams, wireframes
│   ├── requirements.md
│   ├── firestore-schema.md
│   ├── architecture.md
│   └── wireframes/
├── firestore.rules              # Submitted Firestore Security Rules
├── build.gradle.kts
└── README.md
```

---

## Getting Started

### Prerequisites

- Android Studio Hedgehog (2023.1.1) or newer
- JDK 17
- An Android device or emulator running Android 8.0 (API 26) or higher
- A Firebase project with Authentication and Firestore enabled

### Setup

**1. Clone the repository**

```bash
git clone <repo-url>
cd personal-finance-manager-android
```

**2. Configure Firebase**

- Create a project at [console.firebase.google.com](https://console.firebase.google.com)
- Enable **Authentication** → Email/Password sign-in method
- Enable **Cloud Firestore** in production mode
- Register an Android app with package name `com.sliit.pfm`
- Download the generated `google-services.json` and place it in the `app/` directory
- Deploy the security rules from [`firestore.rules`](firestore.rules):

  ```bash
  firebase deploy --only firestore:rules
  ```

**3. Build and run**

```bash
./gradlew assembleDebug
```

Or open the project in Android Studio and click **Run**.

### Building a release APK

```bash
./gradlew assembleRelease
```

The signed APK is generated at `app/build/outputs/apk/release/app-release.apk`.

---

## Documentation

| Document | Location |
|---|---|
| Requirements Analysis | [`docs/requirements.md`](docs/requirements.md) |
| Firestore Schema & Indexing | [`docs/firestore-schema.md`](docs/firestore-schema.md) |
| MVVM Architecture Diagram | [`docs/architecture.md`](docs/architecture.md) |
| Annotated Wireframes | [`docs/wireframes/`](docs/wireframes/) |
| Design Decision Log | [`docs/design-decisions.md`](docs/design-decisions.md) |

The full Technical Design Document is submitted separately as a PDF on the LMS.

---

## Team

| Role | Member | Student ID |
|---|---|---|
| Tech Lead — Architecture, Authentication, Foundation | _Add name_ | _Add ID_ |
| Income Module | _Add name_ | _Add ID_ |
| Expense Module | _Add name_ | _Add ID_ |
| Dashboard · Goals · Insights | _Add name_ | _Add ID_ |

---

## Contributing (Group Members)

This project follows a **GitHub Flow** branching strategy.

**Branch naming**

| Prefix | Purpose | Example |
|---|---|---|
| `feature/` | New feature work | `feature/login-screen` |
| `bugfix/` | Fixing broken behaviour | `bugfix/expense-empty-amount-crash` |
| `docs/` | Documentation only | `docs/firestore-schema` |
| `chore/` | Config, dependencies, refactor | `chore/upgrade-compose` |

**Workflow**

1. Pull the latest `main`: `git pull origin main`
2. Create a branch: `git checkout -b feature/<task-name>`
3. Commit using Conventional Commits style — `feat:`, `fix:`, `docs:`, `refactor:`, `chore:`, `test:`
4. Push and open a Pull Request linking the related issue with `Closes #<id>`
5. Wait for one teammate's approval, then **squash and merge**

**Branch protection.** `main` requires one approving review and an up-to-date branch. Direct pushes are blocked.

---

## Project Management

Tasks are tracked using **GitHub Projects** with the following columns:

```
Backlog  →  To Do  →  In Progress  →  Done
```

Issues are labelled by area: `auth`, `income`, `expense`, `dashboard`, `firebase`, `docs`, `bug`, `chore`.

---

## Academic Integrity

This project is submitted for **SE3092 — Platform Based Development** at the Sri Lanka Institute of Information Technology (SLIIT), Faculty of Computing, Department of Computer Science.

All source code, design decisions, and documentation represent the original work of the listed group members. AI-assisted tooling was used as a learning aid where applicable, in line with the course's academic integrity policy. No code has been copied from open-source finance applications, and no work has been shared between groups.

---

<div align="center">

**Sri Lanka Institute of Information Technology** · Faculty of Computing · 2026 Semester 1

</div>
