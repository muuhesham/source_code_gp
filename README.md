# Fa3liat - Advanced Event Management & E-Ticketing System

## 🌟 Project Overview
**Fa3liat** is a comprehensive graduation project designed to revolutionize the event management industry. It provides an end-to-end solution for organizers to create, manage, and monetize events, while offering consumers a seamless experience for discovering and purchasing tickets.

The system is architected as a robust mono-repository consisting of three core pillars:
1.  **Backend API**: A high-performance RESTful service handling complex business logic, security, and data persistence.
2.  **Web Frontend**: An interactive, responsive dashboard for event discovery and management.
3.  **Mobile Scanner Application**: A specialized tool for event staff to verify tickets in real-time using QR technology.

---

## 📂 Repository Structure
The project utilizes Git submodules to manage independent codebases within a unified root manager.

```text
project-root/
├── exe/                 # Pre-built distribution binaries (Android APK)
│   └── app-release.apk  # Latest stable mobile scanner build
├── src/                 # Source code for all system components
│   ├── backend/         # Node.js Express API (Business Logic & Database)
│   ├── frontend/        # React.js / Vite Web Application
│   └── mobile/          # React Native / Expo Scanner App
├── .gitignore           # Root ignore rules for mono-repo artifacts
├── .gitmodules          # Submodule configuration and path mapping
├── package.json         # Root scripts for project-wide management
└── README.md            # Comprehensive project documentation
```

---

## 🛠 Technologies Used
Our tech stack is selected for scalability, performance, and developer productivity.

*   **Runtime Environment**: [Node.js](https://nodejs.org/) (v18+)
*   **Backend Framework**: [Express.js](https://expressjs.com/)
*   **Database & ORM**: [PostgreSQL](https://www.postgresql.org/) with [Prisma ORM](https://www.prisma.io/)
*   **Web Frontend**: [React.js](https://reactjs.org/) powered by [Vite](https://vitejs.dev/)
*   **Mobile Framework**: [React Native](https://reactnative.dev/) with [Expo](https://expo.dev/)
*   **Package Manager**: [npm](https://www.npmjs.com/)
*   **Version Control**: [Git](https://git-scm.com/) (Submodules implementation)

---

## 📋 Prerequisites
Before setting up the project, ensure your environment meets the following requirements:

*   **Software**:
    *   **Node.js**: v18.x or higher
    *   **npm**: v9.x or higher
    *   **Git**: Latest version
    *   **PostgreSQL**: v14.x or higher (Local or Cloud instance)
    *   **Android Studio**: Required for building the mobile application locally
*   **Hardware (Recommended)**:
    *   **OS**: Windows 10/11, macOS, or Linux
    *   **RAM**: 16GB (Minimum 8GB)
    *   **Storage**: 5GB free space

---

## 🚀 Getting Started

### 1. Clone the Repository
Clone the main repository and all nested submodules simultaneously using the `--recurse-submodules` flag:

```bash
git clone --recurse-submodules https://github.com/muuhesham/source_code_gp.git
cd source_code_gp
```

### 2. Install Dependencies
Install all required packages for the root and all three sub-projects in one command:

```bash
npm run install-all
```

### 3. Environment Configuration
Each project in `src/` requires its own `.env` file. Refer to the `.env.example` files within each subdirectory for the necessary variables (Database URLs, API keys, etc.).

### 4. Running the Project
To start both the Backend and Frontend development servers concurrently:

```bash
npm run dev
```

### 5. Mobile Build
To generate a fresh Android APK from the mobile source:

```bash
npm run build-mobile
```
*The resulting APK will be automatically copied to the `/exe/` directory.*

---

## 👥 Team & Contribution
This project is developed as part of a University Graduation Project. All components are maintained for production-readiness and follow modern software engineering standards.
