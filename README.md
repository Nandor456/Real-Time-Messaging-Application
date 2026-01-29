# Real-Time-Messaging-Application

Real-Time-Messaging-Application is a chatting application which I will use for future projects:

- **Backend:** Node.js + Express (REST API)
- **Database:** Postgres (Docker)
- **Frontend:** Flutter (mobile + web)

## Repo Structure

```
backend/     # Node/Express API + DB setup
frontend/    # Flutter application
```

## Prerequisites

- **Node.js** (recommended: latest LTS)
- **Docker Desktop** (for Postgres via `docker-compose`)
- **Flutter SDK** (stable channel)

## Quick Start

### 1) Start the database (Docker)

From the backend folder:

```bash
cd backend
docker compose up -d
```

This will start Postgres and initialize the schema using:

- `backend/database/init.sql`

To stop the database:

```bash
docker compose down
```

### 2) Configure backend environment variables

The backend reads configuration from environment variables (see `backend/src/config/env.js` and `backend/src/config/database.config.js`).

Create a `.env` file in `backend/` (or export variables in your shell) with values that match your `docker-compose.yml`.

Typical variables look like:

```bash
# backend/.env
PORT=3000

DB_HOST=localhost
DB_PORT=5432
DB_USER=postgres
DB_PASSWORD=postgres
DB_NAME=earlytrip

# Auth (example)
JWT_SECRET=change_me
```

Note: exact variable names may differ depending on your config files.

### 3) Run the backend

```bash
cd backend
npm install
npm run start
```

If your project uses a dev script (watch mode), you can run:

```bash
npm run dev
```

Backend entrypoint:

- `backend/app.js`

Routes live in:

- `backend/src/routes/`

### 4) Run the Flutter app

```bash
cd frontend
flutter pub get
flutter run
```

To run on Chrome (web):

```bash
flutter run -d chrome
```

Flutter entrypoint:

- `frontend/lib/main.dart`

## Backend Overview

Main backend folders:

- `backend/src/controllers/` – request handlers (auth, user, group)
- `backend/src/routes/` – route wiring (`auth.routes.js`, `user.routes.js`, `group.routes.js`)
- `backend/src/middlewares/` – auth and access control middleware
- `backend/src/services/` – business logic (auth, notifications, database)
- `backend/uploads/` – uploaded files (if enabled)

### Authentication

Authentication logic is located under:

- `backend/src/controllers/auth.controller.js`
- `backend/src/services/auth.service.js`
- `backend/src/middlewares/auth.middleware.js`

## Flutter Overview

Main Flutter folders:

- `frontend/lib/screens/` – UI screens
- `frontend/lib/services/` – API/services layer
- `frontend/lib/models/` – data models
- `frontend/lib/widgets/` – reusable UI widgets
- `frontend/lib/utils/` – utilities/helpers
