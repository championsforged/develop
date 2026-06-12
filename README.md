# ChampionsForged

A comprehensive sports participation platform connecting athletes, coaches, venue owners, tournament organizers, referees, and employers in a unified ecosystem.

## Repository Structure

```
championsforged/
├── backend/        # Node.js + NestJS + PostgreSQL + Redis + Socket.io
├── mobile/         # Flutter (iOS & Android)
└── web/            # React.js + Redux + Material-UI
```

## Tech Stack

### Backend
- **Runtime:** Node.js
- **Framework:** Express.js / NestJS
- **Database:** PostgreSQL
- **Caching:** Redis
- **Real-time:** Socket.io

### Mobile (iOS & Android)
- **Framework:** Flutter (Dart)
- **State Management:** Provider / Riverpod
- **Local Database:** Hive / Drift
- **Push Notifications:** Firebase Cloud Messaging

### Web Dashboard & Admin Panel
- **Framework:** React.js
- **State Management:** Redux
- **UI Framework:** Material-UI
- **Routing:** React Router

## Branch Strategy

| Branch | Purpose |
|---|---|
| `main` | Production — stable releases only |
| `develop` | Integration — merges from feature branches |
| `feature/*` | Feature development |
| `hotfix/*` | Critical production fixes |
| `release/*` | Release preparation |

## Getting Started

See individual READMEs in `backend/`, `mobile/`, and `web/` directories.
