# Fa3liat — Event Management & E-Ticketing Platform

Fa3liat is a production-grade Event Management & E-Ticketing system designed for seamless event organization and secure ticket purchasing. The platform offers a robust backend API, a responsive web dashboard for organizers and attendees, and a specialized mobile application for real-time QR-based ticket validation.

## 🌟 Project Overview

Fa3liat provides a complete end-to-end solution for:
- **Ticketing System:** Secure QRcode ticket purchasing with Stripe integration, supporting both free and paid events.
- **Seat Selection:** Interactive seat maps for venues with tier-based pricing.
- **Organizer Dashboard:** Comprehensive tools for managing events, sessions, tickets, and financial payouts.
- **Mobile Scanner:** Real-time QR code validation app for event staff to verify tickets at the gate.
- **Real-time Notifications:** Instant updates via Socket.IO and background workers for emails/SMS.
- **Event Discovery:** AI-powered search and recommendations (RAG) for finding the perfect events.

---

## 📂 Repository Structure

```text
fa3liat/
├── src/
│   ├── backend/           # Express.js API, Prisma ORM, BullMQ Workers
│   ├── frontend/          # React.js Web Application (Vite)
│   └── mobile/            # React Native (Expo) Scanner Application
├── exe/
│   └── app-release.apk    # Pre-built Android Scanner App
├── docker-compose.yml     # Root orchestration for the entire stack
└── README.md              # Project documentation
```

---

## 🚀 Quick Start (Docker)

The platform is optimized for Docker. Follow these steps to get started:

### Prerequisites
- Docker and Docker Compose installed.
- `.env` files configured in `src/backend` and `src/frontend` (use the provided `.env.example` templates).

### 1. Configure Environment Files
```bash
# (Optional) Docker Compose overrides (ports, profiles)
cp .env.example .env

# Required for Docker + local dev
cp src/backend/.env.example src/backend/.env
cp src/frontend/.env.example src/frontend/.env

# Optional (mobile app)
cp src/mobile/.env.example src/mobile/.env
```

### 2. Start the Application
This command builds the images and starts all services (DB, Redis, backend, workers, frontend).

```bash
docker compose up -d --build
```

The application will be available at `http://localhost:5173`.

> Note: the backend container runs `prisma migrate reset` + seeds the database on startup (development convenience). This **wipes existing data** in the Docker database volume.

### 3. Stopping the Application

To stop all running services:

```bash
docker compose down
```

---

## 🛠️ Manual Development Setup

### Backend Setup
```bash
cd src/backend
# 1. Configure .env (ensure PORT=3000)
# 2. Install dependencies
npm install
# 3. Setup DB & Generate Client
npm run setup
# 4. Start Server
npm run dev
```

### Frontend Setup
```bash
cd src/frontend
npm install
npm run dev
```

---

## 🔐 Environment Variables

### Backend (`src/backend/.env`)
| Variable | Description | Standard Value |
| :--- | :--- | :--- |
| `PORT` | API Server Port | `3000` |
| `DATABASE_URL` | PostgreSQL URL | `postgresql://fa3liat:fa3liat@localhost:5434/fa3liat` |
| `REDIS_URL` | Redis URL | `redis://localhost:6381` |
| `MAIL_HOST` | Mail SMTP Host | `localhost` |
| `STRIPE_SECRET_KEY` | Stripe Test Key | `sk_test_...` |
| `OLLAMA_BASE_URL` | AI Engine URL | `http://localhost:11436` |

---

## 📖 Available Commands

### Backend
- `npm run setup`: Full database initialization (migrate + seed).
- `npm run dev`: Start API with hot-reload.
- `npm run queue:mail-worker`: Start email background worker.
- `npm run queue:sms-worker`: Start SMS background worker.
- `npm run queue:embedding-worker`: Start AI vector worker.

---
**Fa3liat** — Built with ❤️ for Graduation Project 2026.
