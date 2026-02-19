# Seasonal Skill Builder — MVP Architecture

## 1. System Overview

A modular full-stack app with role-based access:

- **User app** for training, logging, and progress visualization
- **Admin app** for modules, phases, drills, and achievements
- **API layer** with secure auth and domain services
- **PostgreSQL** as source of truth

Suggested deployment topology:

- Next.js frontend + API routes (single deployable)
- PostgreSQL (managed)
- Scheduled jobs for reminders (cron)

---

## 2. Tech Stack

- **Frontend**: Next.js 14+ (App Router), TypeScript, Tailwind CSS
- **Backend**: Next.js Route Handlers + service layer
- **Auth**: NextAuth/Auth.js (credentials + Google OAuth)
- **Database**: PostgreSQL + Prisma ORM
- **Validation**: Zod
- **Charts**: Recharts
- **Scheduling**: Vercel Cron / BullMQ (if worker introduced)

---

## 3. Domain Model

Core entities for MVP:

- `User`
- `Profile`
- `SeasonPhase`
- `TaskTemplate`
- `DailyTask`
- `TrainingModule`
- `ModuleProgress`
- `ShootingLog`
- `FitnessLog`
- `XpLedger`
- `Achievement`
- `UserAchievement`

### Initial relational schema (conceptual)

```sql
User(id, email, passwordHash, role, createdAt)
Profile(userId FK, huntType, experienceLevel, physicalBaseline, preferredWeapon)
SeasonPhase(id, name, startDate, endDate, isActive)
TaskTemplate(id, title, category, xpReward, isActive)
DailyTask(id, userId FK, taskTemplateId FK, dueDate, completedAt)
TrainingModule(id, title, description, skillType, difficulty, estimatedMinutes, unlockLevel, isPublished)
ModuleProgress(id, userId FK, moduleId FK, status, percent, completedAt)
ShootingLog(id, userId FK, date, distanceYards, groupSizeInches, conditions, weapon, notes)
FitnessLog(id, userId FK, date, bodyWeight, packWeight, miles, elevationGain, strengthNotes)
XpLedger(id, userId FK, sourceType, sourceId, points, createdAt)
Achievement(id, code, name, description, thresholdType, thresholdValue)
UserAchievement(id, userId FK, achievementId FK, earnedAt)
```

---

## 4. API Contract (MVP)

### Auth

- `POST /api/auth/register`
- `POST /api/auth/signin`
- `POST /api/auth/signout`
- `GET /api/auth/session`

### Dashboard

- `GET /api/dashboard/overview`
  - current phase, phase progress, weekly completion, XP, level
- `GET /api/dashboard/today-tasks`
- `POST /api/dashboard/today-tasks/:taskId/complete`

### Modules

- `GET /api/modules`
- `GET /api/modules/:id`
- `POST /api/modules/:id/start`
- `POST /api/modules/:id/complete-step`

### Shooting

- `GET /api/shooting/logs`
- `POST /api/shooting/logs`
- `GET /api/shooting/metrics`

### Fitness

- `GET /api/fitness/logs`
- `POST /api/fitness/logs`
- `GET /api/fitness/metrics`

### Gamification

- `GET /api/gamification/summary`
- `GET /api/gamification/achievements`

### Admin

- `POST /api/admin/modules`
- `PATCH /api/admin/modules/:id`
- `POST /api/admin/phases`
- `PATCH /api/admin/phases/:id`
- `POST /api/admin/achievements`

---

## 5. Frontend Information Architecture

- `/login`
- `/onboarding/profile`
- `/dashboard`
- `/modules`
- `/shooting`
- `/fitness`
- `/achievements`
- `/admin` (role-protected)

Dashboard widgets:

1. Season phase card + progress bar
2. Weekly completion + XP
3. Today’s task checklist
4. Shooting trend mini chart
5. Fitness readiness card

---

## 6. Business Rules

- Daily tasks are generated from active templates and user profile context.
- Completing tasks grants XP; level derived from cumulative XP.
- Modules unlock by level and prerequisite completion.
- Readiness score example:
  - 40% activity consistency (days active / 7)
  - 35% endurance load (miles + elevation trend)
  - 25% strength frequency
- Achievement evaluation runs on each log/task completion and by nightly job.

---

## 7. Notifications (MVP)

- Weekly inactivity: if no activity for 7 days
- Streak warning: if streak exists and no action by late day
- Pre-season alert: X days before phase transition

Delivery channels:

- In-app notifications (MVP)
- Email optional (phase 1.5)

---

## 8. Security and Reliability

- Password hashing with Argon2/Bcrypt
- Server-side validation with Zod
- Rate limiting on auth endpoints
- RBAC middleware for admin routes
- Audit logging for admin content changes

---

## 9. Implementation Plan (2–3 Sprints)

### Sprint 1

- Auth (credentials + profile onboarding)
- Dashboard shell + daily tasks
- Base DB schema and seed data

### Sprint 2

- Module listing/progress + unlock logic
- Shooting log + chart + metrics
- Fitness log + readiness score

### Sprint 3

- XP + levels + achievements
- Admin CRUD for modules/phases/achievements
- Scheduled notifications

---

## 10. Definition of Done (MVP)

- A new user can sign up, complete onboarding, and view dashboard
- User can complete daily tasks and gain XP
- User can log shooting and fitness data and see trends
- User can complete modules with unlock progression
- Admin can manage modules, phases, and achievements in UI
- App is mobile responsive and deployable with environment-based config
