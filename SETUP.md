# ChampionsForged — Project Setup Documentation

**Date:** June 12, 2026  
**Repository:** https://github.com/championsforged/develop  
**Local Path:** `/Users/bhaskaryalijala/Projects/championsforged`

---

## 1. Git Configuration

### Global Git Author
```bash
git config --global user.name "championsforged"
git config --global user.email "bhaskaryalijala@gmail.com"
```

### Claude Code Attribution
- Disabled Claude co-author footer in `~/.claude/settings.json`
- All commits authored solely as `championsforged`

---

## 2. GitHub Repository

### Repository Details
| Field | Value |
|---|---|
| Organization | championsforged |
| Repository | develop |
| URL | https://github.com/championsforged/develop |
| Visibility | Public |
| Collaborator | bhaskaryalijala-sketch (Write access) |

### GitHub Authentication
- Git credentials stored in macOS keychain
- Personal Access Token scopes: `repo`, `workflow`

---

## 3. Branch Strategy

| Branch | Purpose | Protection |
|---|---|---|
| `main` | Production — stable releases only | ✅ Protected |
| `develop` | Integration — merges from feature branches | ✅ Protected |
| `feature/initial-setup` | First feature branch | — |
| `feature/*` | All future features | Branch from `develop` |
| `hotfix/*` | Critical production fixes | Branch from `main` |
| `release/*` | Release preparation | Branch from `develop` |

### Branch Protection Rules
**`main`**
- No direct pushes allowed
- Requires 1 pull request review
- Stale reviews dismissed on new commits
- Enforced for admins

**`develop`**
- No direct pushes allowed
- Requires 1 pull request review
- Stale reviews dismissed on new commits

### Workflow
```
feature/* → PR → develop → PR → main
hotfix/*  → PR → main (then merge back to develop)
```

---

## 4. Repository Structure (Monorepo)

```
championsforged/
├── .github/
│   ├── ISSUE_TEMPLATE/
│   │   ├── bug_report.md          # Bug report template
│   │   └── feature_request.md     # Feature request template
│   ├── workflows/
│   │   ├── backend-ci.yml         # Node.js CI pipeline
│   │   ├── mobile-ci.yml          # Flutter CI pipeline
│   │   └── web-ci.yml             # React CI pipeline
│   └── pull_request_template.md   # PR checklist template
├── backend/                        # Node.js + NestJS
│   └── .gitignore
├── mobile/                         # Flutter (iOS & Android)
│   └── .gitignore
├── web/                            # React.js
│   └── .gitignore
├── .gitignore                      # Root gitignore
├── README.md                       # Project overview
└── SETUP.md                        # This document
```

---

## 5. Tech Stack

### 5.1 Backend
| Technology | Purpose |
|---|---|
| Node.js | Runtime |
| NestJS / Express.js | Framework |
| PostgreSQL | Primary database |
| Redis | Caching |
| Socket.io | Real-time communication |

### 5.2 Mobile (iOS & Android)
| Technology | Purpose |
|---|---|
| Flutter (Dart) | Cross-platform framework |
| Provider / Riverpod | State management |
| Hive / Drift | Local database |
| Firebase Cloud Messaging | Push notifications |

### 5.3 Web Dashboard & Admin Panel
| Technology | Purpose |
|---|---|
| React.js | UI framework |
| Redux | State management |
| Material-UI | Component library |
| React Router | Client-side routing |

---

## 6. CI/CD Pipelines (GitHub Actions)

### Backend CI (`backend-ci.yml`)
Triggers on push/PR to `main` or `develop` when `backend/**` changes.

Steps:
1. Spin up PostgreSQL 15 + Redis 7 services
2. Install Node.js 20 dependencies
3. Run linter
4. Run tests with real DB and Redis

### Mobile CI (`mobile-ci.yml`)
Triggers on push/PR to `main` or `develop` when `mobile/**` changes.

Steps:
1. Set up Flutter (stable channel)
2. Install pub dependencies
3. Run `flutter analyze`
4. Run `flutter test`

### Web CI (`web-ci.yml`)
Triggers on push/PR to `main` or `develop` when `web/**` changes.

Steps:
1. Install Node.js 20 dependencies
2. Run linter
3. Run tests
4. Build production bundle

---

## 7. GitHub Templates

### Pull Request Template
Located at `.github/pull_request_template.md`

Checklist includes:
- Type of change (Feature / Bug Fix / Hotfix / Refactor / Docs)
- Area (Backend / Mobile / Web / Infrastructure)
- Testing confirmation
- No secrets committed check
- Branch targets `develop`

### Issue Templates
**Bug Report** (`.github/ISSUE_TEMPLATE/bug_report.md`)
- Area selection
- Steps to reproduce
- Expected vs actual behavior
- Environment details

**Feature Request** (`.github/ISSUE_TEMPLATE/feature_request.md`)
- Area selection
- User role affected (Athlete / Coach / Venue Owner / Organizer / Referee / Employer)
- Feature description
- Acceptance criteria

---

## 8. Project Management

| Tool | Link |
|---|---|
| Zoho Projects | https://projects.zoho.in/portal/bhaskardotyalijalachampionsforgeddotcom#zp/projects/458355000000071831 |
| GitHub Repo | https://github.com/championsforged/develop |

---

## 9. Next Steps

- [ ] Scaffold NestJS backend starter project in `backend/`
- [ ] Scaffold Flutter app in `mobile/`
- [ ] Scaffold React web dashboard in `web/`
- [ ] Set up PostgreSQL database schema
- [ ] Configure Firebase project for push notifications
- [ ] Set up staging and production deployment pipelines
- [ ] Configure environment variables and secrets in GitHub

---

## 10. Security Notes

- Never commit `.env` files — use `.env.example` as template
- Store secrets in GitHub Secrets (`Settings → Secrets and variables → Actions`)
- Rotate GitHub Personal Access Tokens regularly
- Never share tokens in chat or email — use macOS keychain or a password manager
