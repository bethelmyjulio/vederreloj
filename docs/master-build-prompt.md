# MASTER BUILD PROMPT

## App Name
Seasonal Skill Builder

## Audience
Hunters (whitetail, elk, western big game, waterfowl)

## Product Goal
Improve off-season retention and skill development with structured training and measurable progress.

---

## Build Specification

Create a full-stack web app called **Seasonal Skill Builder** with the following capabilities.

### 1) User Authentication

- Email/password authentication
- Optional social login (Google)
- User profile fields:
  - Primary hunt type (whitetail, elk, waterfowl, etc.)
  - Experience level (Beginner / Intermediate / Advanced)
  - Physical condition baseline (self-assessed)
  - Preferred weapon (rifle / bow / shotgun)

### 2) Dashboard (Main Screen)

After login, show:

#### Seasonal Progress Overview

- Current season phase:
  - Post-season recovery
  - Off-season training
  - Pre-season preparation
  - In-season maintenance
- Progress bar for current phase
- Weekly task completion percentage

#### Today’s Tasks

Dynamic checklist with completion tracking:

- Shooting drill
- Physical conditioning
- Knowledge module
- Gear preparation
- Scouting task (digital or field-based)

### 3) Training Module System

Each module includes:

- Title
- Description
- Skill type (Shooting / Fitness / Fieldcraft / Strategy)
- Difficulty level
- Estimated time
- Progress status

Include progressive unlocks based on user level and prior completions.

Example modules:

- Bow accuracy progression (4-week)
- Backcountry leg endurance
- Wind reading fundamentals
- Shot angle decision training
- Pre-season gear inspection checklist

### 4) Shooting Drill Tracker

Log entries with:

- Distance
- Group size
- Conditions
- Weapon used
- Notes

Visualize:

- Performance trend over time (line chart)
- Accuracy improvement percentage

### 5) Fitness Tracker

Log:

- Body weight
- Pack weight
- Miles hiked
- Elevation gain
- Strength exercises

Visualize:

- Weekly summary
- Endurance progress chart
- “Ready for season?” score from consistency and volume

### 6) Gamification

- XP per completed task
- Level progression
- Achievements:
  - 30-day streak
  - 100 shooting reps
  - 50 miles logged
  - 10 modules completed
- Optional MVP+: seasonal leaderboard

### 7) Content Management (Admin)

Admin dashboard to:

- Add/edit modules
- Adjust seasonal phases
- Add drills
- Manage achievements

No code edits required for content changes.

### 8) Notifications

- Weekly inactivity reminder
- Pre-season ramp-up alert
- Streak warning

### 9) UI Design

- Outdoor aesthetic
- Dark forest green primary
- Earth tones (sand, slate gray, muted orange)
- Clean, minimal, uncluttered
- Mobile-first responsive design

### 10) Technical Requirements

- Modern React framework
- Secure backend auth
- Relational database (PostgreSQL)
- Modular, scalable architecture
- Clean API structure
- Production-ready project layout

---

## MVP Scope Priority

1. Authentication
2. Dashboard
3. Module system
4. Shooting + fitness logging
5. Basic gamification

Leaderboards and advanced analytics are phase 2.

---

## Optional Phase 2 AI Summary

Add generated insights such as:

> “Based on your last 30 days, endurance is improving but shooting consistency drops beyond 200 yards.”

Implement as prompt-based analysis over structured user training data.
