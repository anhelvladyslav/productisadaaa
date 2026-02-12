# Production Workflow Control System

## What this application is
**Production Workflow Control System** is a music production management platform that brings together:
- tracks and their versions,
- tasks for each track,
- releases,
- demo submissions to labels,
- team activity history.

The application is designed for artists and collaborators to control the full track lifecycle: from draft to release.

---

## Core features

### 1) Track and version management
- Create and edit tracks.
- Manage track versions (for example: draft, mix, master).
- Attach files to versions (local storage).
- Control version statuses through the workflow.

### 2) Task management
- Create track-related tasks (mastering, artwork, fixes, etc.).
- Deadlines and progress tracking.
- Task statuses: `pending → in progress → done`.

### 3) Release management
- Create releases and add tracks to them.
- Check release readiness before publishing.
- Prevent releases without tracks.

### 4) Demo Submission
- Submit demos for specific track versions.
- Select a label for submission.
- Add notes and update submission processing status.
- Submission statuses: `pending → received → rejected → signed`.

### 5) Labels
- Label database with contact details.
- Link labels to demo submissions.

### 6) Authentication and roles
- JWT authentication.
- User roles:
  - `artist`
  - `collaborator`
- Protected API endpoints and role-based access control.

### 7) Activity Log
- Log key user actions.
- Keep a transparent history of production workflow changes.

---

## Data model

### Entities
- `User`
- `Track`
- `TrackVersion`
- `Task`
- `Release`
- `DemoSubmission`
- `Label`
- `ActivityLog`

### Relationships
- `Track 1—N TrackVersion`
- `TrackVersion 1—N DemoSubmission`
- `Track 1—N Task`
- `Release 1—N Track`
- `Label 1—N DemoSubmission`
- `User 1—N ActivityLog`

---

## Workflow statuses
- **TrackVersion:** `draft → mix → master → demo → signed → released`
- **DemoSubmission:** `pending → received → rejected → signed`
- **Task:** `pending → in progress → done`

Workflow rules prevent skipping lifecycle stages.

---

## Application interface

### Pages
- `Login`
- `Register`
- `Dashboard`
- Management sections:
  - Tracks / TrackVersions
  - Tasks
  - Releases
  - Demo Submissions
  - Activity Log

### What users see in the Dashboard
- Track and release tables.
- Filters and search by status/label/track.
- Task deadlines and current production pipeline visibility.

---

## Technology stack
- **Frontend:** React + TypeScript (Vite)
- **Backend:** Node.js + Express
- **Database:** PostgreSQL
- **Auth:** JWT
- **Storage:** local file storage (optional)

---

## System structure

```text
Production Workflow Control System
├── Tracks / TrackVersions
├── Tasks (mastering, artwork, fixes)
├── Releases
└── Demo Submissions
    └── Labels (email, contact person, notes)
```

All core modules are connected through `Track` and `TrackVersion`, while `ActivityLog` records user actions across the system.
