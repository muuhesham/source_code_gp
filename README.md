# Project Mono-Repo

This repository manages the Backend, Frontend, and Mobile applications for the Graduation Project using Git submodules.

## Structure

- `src/backend`: Node.js Express API ([Repo](https://github.com/muuhesham/graduation_project.git))
- `src/frontend`: Vite React Web App ([Repo](https://github.com/AmrKhaled996/Event-Agency.git))
- `src/mobile`: Expo React Native App ([Repo](https://github.com/AmrKhaled996/Fa3liat_Scan.git))
- `apk/`: Contains the generated Android release APK.

## Prerequisites

- [Node.js](https://nodejs.org/) (v18+)
- [npm](https://www.npmjs.com/)
- [Java Development Kit (JDK)](https://www.oracle.com/java/technologies/downloads/) (for mobile build)
- [Android SDK](https://developer.android.com/studio) (for mobile build)

## Getting Started

1. **Clone the repository with submodules:**
   ```bash
   git clone --recursive <this-repo-url>
   ```
   If you already cloned it without submodules:
   ```bash
   git submodule update --init --recursive
   ```

2. **Install all dependencies:**
   ```bash
   npm run install-all
   ```

## Available Scripts

- `npm run install-all`: Installs dependencies for root and all sub-projects.
- `npm run run-backend`: Starts the backend in development mode.
- `npm run run-frontend`: Starts the frontend in development mode.
- `npm run build-mobile`: Performs an Expo prebuild and generates a release APK, then copies it to the `apk/` directory.

## Mobile Build Note

The `build-mobile` script assumes you have a local Android development environment configured. It will:
1. Run `npx expo prebuild` to generate the `android` folder.
2. Run `gradlew assembleRelease` to build the APK.
3. Copy the resulting APK to `apk/app-release.apk`.
