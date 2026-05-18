# Fa3liat — Event Management & E-Ticketing Platform

Fa3liat is a production-grade Event Management & E-Ticketing system designed for seamless event organization and secure ticket purchasing. The platform offers a robust backend API, a responsive web dashboard for organizers and attendees, and a specialized mobile application for real-time QR-based ticket validation.

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

## 📥 Project Setup / Clone Repository

This project uses **Git Submodules** to manage the frontend, backend, and mobile components as separate repositories. This architecture allows each part of the platform to be developed and versioned independently while remaining part of a unified stack.

### 1. Cloning for the First Time
To clone the main repository and automatically pull all submodule source code in one step:

```bash
git clone --recurse-submodules <repo-url>
```

### 2. If You Already Cloned (Empty Folders)
If you have already cloned the repository normally and find the `src/` subdirectories empty, run the following to initialize and fetch the code:

```bash
git submodule update --init --recursive
```

### 3. Keeping Submodules Updated
When pulling new changes from the main repository, ensure your submodules are also updated to their latest pinned commits:

```bash
git pull origin main
git submodule update --recursive
```

### ⚠️ Troubleshooting
- **Empty Folders**: If `src/backend`, `src/frontend`, or `src/mobile` are empty after cloning, run the initialization command in Step 2.
- **Submodule Not Updated**: If the project fails to build after a pull, your submodules might be out of sync. Run `git submodule update --recursive`.
- **Detached HEAD Warning**: Submodules are pinned to specific commits. It is normal for them to be in a "detached HEAD" state. If you need to make changes within a submodule, remember to `git checkout main` (or your target branch) inside that specific directory first.

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

### Mobile App Setup (Scanner)
To run the mobile application for ticket scanning:
1. **Download Expo Go**: Install the **Expo Go** app from the [Google Play Store](https://play.google.com/store/apps/details?id=host.exp.exponent) or [Apple App Store](https://apps.apple.com/app/expo-go/id982107779) to open our mobile app.
2. **Start the App**:
   ```bash
   cd src/mobile
   npm install
   npx expo start
   ```
3. **Open the App**: Scan the QR code displayed in your terminal using the Expo Go app to start scanning tickets.

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

**Fa3liat** — Built with ❤️ for Graduation Project 2026.
