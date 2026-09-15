# Web Development Details

## Phase 0 — Project & Development Setup

### W0.1 — Understand Project Requirements

Reviewed the project scope, architecture, technology stack, and frontend requirements to establish the web development foundation.

### W0.2 — Set Up Development Environment

Verified Node.js, npm, Git, VS Code, npm registry, architecture, and network connectivity.

    node -v
    npm -v
    git --version
    code --version
    npm config get registry
    node -p "process.arch"
    npm ping

### W0.3 — Create React + TypeScript + Vite Project

Created the React + TypeScript web application using Vite and verified the initial application build.

    npm create vite@latest . -- --template react-ts
    npm install
    npm run lint
    npm run build

### W0.4 — Configure ESLint & Prettier

Configured Prettier and ESLint to maintain consistent formatting and code quality.

    npm install -D prettier eslint-config-prettier
    npm run format
    npm run format:check
    npm run lint
    npm run build

Created:
- `.prettierrc`
- `.prettierignore`

### W0.5 — Define Web Project Structure

Created a scalable feature-oriented structure for application code, reusable components, features, services, configuration, hooks, types, and utilities.

    New-Item -ItemType Directory -Path "src/app","src/assets","src/components/common","src/components/layout","src/components/ui","src/config","src/features/admin","src/features/alumni","src/features/auth","src/features/community","src/features/connections","src/features/events","src/features/jnv","src/features/media","src/features/mentorship","src/features/notifications","src/features/opportunities","src/features/search","src/features/user","src/hooks","src/lib","src/pages","src/services/api","src/types","src/utils" -Force

Moved application files under `src/app`, updated imports, replaced the Vite starter screen, and removed unused starter assets.

### W0.6 — Configure Environment Variables

Configured environment-specific application settings and protected local environment files from Git.

    New-Item ".env" -ItemType File -Force
    New-Item ".env.example" -ItemType File -Force
    New-Item ".env.local" -ItemType File -Force

Configured:
- `VITE_APP_NAME`
- `VITE_API_BASE_URL`
- `VITE_APP_ENV`

Created:
- `.env.example`
- `.env.local`
- `src/config/env.ts`

Updated `.gitignore` to exclude `.env`, `.env.local`, build output, cache, and coverage files.

### W0.7 — Configure Git & Branching Workflow

Configured the web repository with `main` and `develop` branches and established the basic feature/fix/chore workflow.

    git config --global user.name "Sanjay Kumar"
    git config --global user.email "YOUR_GITHUB_EMAIL"
    git branch -M main
    git checkout -b develop
    git status
    git branch

Branch strategy:

    main
    develop
    feature/*
    fix/*
    chore/*

### W0.8 — Create Initial Application Shell

Created the initial React application shell and verified that the application runs successfully.

    npm run lint
    npm run format
    npm run format:check
    npx tsc -b
    npm run build
    npm run dev

Local application:

    http://localhost:5173/

## Phase 0 Verification

- ESLint: Passed
- Prettier: Passed
- TypeScript: Passed
- Production build: Passed
- Development server: Passed
- Project structure: Verified
- Environment configuration: Verified
- Git branching setup: Verified

## Phase 0 Status

**Completed**

## Phase 0 Commit

    git add .
    git commit -m "feat(web): complete Phase 0 project and development setup"