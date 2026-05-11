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

## 🛠️ Technologies Used

### Backend Stack
| Tool | Technology | Purpose |
| :--- | :--- | :--- |
| **Runtime** | Node.js | Server-side execution |
| **Framework** | Express.js | API Development |
| **Database** | PostgreSQL | Relational data storage |
| **Vector DB** | pgvector | AI Embedding storage |
| **ORM** | Prisma | Database modeling & migrations |
| **Cache/Queue**| Redis & BullMQ | Background tasks & Rate limiting |
| **Real-time** | Socket.IO | Instant updates |
| **Payments** | Stripe | Payment processing & Payouts |
| **AI/RAG** | OpenAI / Ollama | Semantic search & Chatbot |

### Frontend Stack
| Tool | Technology | Purpose |
| :--- | :--- | :--- |
| **Library** | React 19 | User Interface |
| **Build Tool** | Vite | Rapid development & bundling |
| **Styling** | Tailwind CSS 4 | Utility-first styling |
| **UI Components**| MUI / Radix UI | Accessible UI elements |
| **State** | Context API | Global state management |
| **Animations** | Framer Motion | Smooth transitions |

### Mobile Stack
| Tool | Technology | Purpose |
| :--- | :--- | :--- |
| **Framework** | React Native (Expo) | Cross-platform mobile development |
| **Navigation** | Expo Router | File-based routing |
| **Styling** | NativeWind | Tailwind CSS for Mobile |
| **Scanning** | Expo Camera | QR Code recognition |

---

## 📋 System Requirements

- **Operating System:** Windows 10+, macOS, or Linux.
- **Hardware:** 8GB+ RAM (16GB recommended for AI features), 5GB Free Storage.
- **Software:**
  - [Node.js (LTS)](https://nodejs.org/) and npm
  - [Docker Desktop](https://www.docker.com/products/docker-desktop/)
  - [PostgreSQL 15+](https://www.postgresql.org/) or use supabase on browser
  - [Redis 7+](https://redis.io/) or WSL on windows and install valkey
  - [Ollama](https://ollama.com/) (For local AI embedding)
  - [Stripe CLI](https://stripe.com/docs/stripe-cli) (For webhook testing)

---

## 🚀 Installation

### METHOD 1: Manual Setup (Development)

#### 1. Backend Setup
```bash
cd src/backend
# Configure .env file (see Environment Variables section)
npm run setup          # Initialize DB, run migrations and seeds
npm run dev            # Start API server
```

#### 2. Worker Setup (In separate terminals)
```bash
npm run queue:mail-worker      # Handle emails
npm run queue:embedding-worker # Handle AI embeddings
npm run queue:sms-worker       # Handle SMS notifications
npm run stripe:listen          # Listen for Stripe webhooks (requires Stripe CLI)
sudo service valkey-server start # Start Valkey for redis (Download WSL for windows)
```

#### 3. Frontend Setup
```bash
cd src/frontend
npm install
npm run dev            # Start web dashboard at http://localhost:5173
```

#### 4. Mobile Setup
```bash
cd src/mobile
npm install
npx expo start         # Start Expo Dev Server
```

---

### METHOD 2: Docker Installation (Recommended)

The entire stack (DB, Redis, Backend, Frontend, Workers, Mailhog) can be launched with a single command:

```bash
# Launch the full stack
docker compose up --build

# Launch with AI features (Ollama)
docker compose --profile ai up --build

# View logs
docker compose logs -f

# Shut down
docker compose down
```

---

## 🔐 Environment Variables

Create a `.env` file in `src/backend` based on `.env.example`:

### Backend (.env)
| Variable | Description | Example Value |
| :--- | :--- | :--- |
| `DATABASE_URL` | PostgreSQL Connection String | `postgresql://user:pass@localhost:5432/db` |
| `REDIS_URL` | Redis Connection String | `redis://127.0.0.1:6379` |
| `JWT_KEY` | Secret for Access Tokens | `your_super_secret_key` |
| `JWT_REKEY` | Secret for Refresh Tokens | `your_super_secret_key` |
| `STRIPE_SECRET_KEY` | Stripe Secret Key | `sk_test_...` |
| `GOOGLE_MAPS_API_KEY`| Google Maps API Key | `AIza...` |
| `AI_API_KEY` | OpenAI API Key | `sk-...` |
| `OLLAMA_BASE_URL` | Local Ollama URL | `http://localhost:11434` |

### Frontend (.env)
| Variable | Description | Example Value |
| :--- | :--- | :--- |
| `VITE_API_URL` | Backend API URL | `http://localhost:8000` |

---

## 🛠️ Compilation & Build

### Backend
```bash
cd src/backend
npm run setup
```

### Frontend
```bash
cd src/frontend
npm run build
```

### Mobile (Generate APK)
```bash
cd src/mobile
# Requires EAS account or local Android build environment
npx expo run:android --variant release
```

---

## 📖 Available Scripts

### Backend
- `npm run setup`: Run database setup, migrations, and seed data.
- `npm run dev`: Start development server with Nodemon.
- `npm run prisma:migrate`: Apply database migrations.
- `npm run queue:mail-worker`: Start the mailing background worker.
- `npm run queue:embedding-worker`: Start the AI vector embedding worker.
- `npm run stripe:listen`: start Stripe CLI to listen for webhooks.
- `npm run prisma:generate`: generate the db
- `npm run prisma:seed`: seed the db
- `npm run queue:sms-worker`: start the sms background worker

### Frontend
- `npm run dev`: Start Vite development server.
- `npm run build`: Build for production.
- `npm run preview`: Preview production build.

---

## 📚 Documentation

For a deeper dive into the system architecture and design, refer to the detailed documentation in the `src/backend/docs` folder:
- **Architecture:** `architecture.md`, `uml_class_diagram.md`
- **Database:** `database_erd.md`, `eer_diagram.md`
- **API Design:** `api_design.md`
- **Security:** `security.md`
- **Diagrams:** `sequence_diagram.md`, `activity_diagram.md`, `socket_flow.md`
- **AI/RAG Flow:** `sequence_ai_embedding.md`

---

## 🤝 Contributing

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/yourFeature`)
3. Commit your Changes (`git commit -m 'Add some yourFeature'`)
4. Push to the Branch (`git push origin feature/yourFeature`)
5. Open a Pull Request

---

## 📜 License
Distributed under the MIT License. See `LICENSE` for more information.

---
**Fa3liat** — Built with ❤️ for Graduation Project 2026.
