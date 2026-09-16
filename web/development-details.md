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

## Phase 1 — UI Foundation & Routing

### W1.1 — Define Design System

Defined the initial design system and reusable design tokens for consistent colors, typography, spacing, borders, and layout styling.

Created:

- `src/styles/tokens.css`

### W1.2 — Create Global Styles

Configured global application styles, typography, box sizing, page dimensions, and base browser styling.

Updated:

- `src/index.css`

### W1.3 — Create Reusable UI Components

Created the initial reusable UI component foundation for buttons, inputs, cards, and loading indicators.

    New-Item -ItemType Directory -Path "src/components/ui/Button","src/components/ui/Input","src/components/ui/Card","src/components/ui/Spinner" -Force

    New-Item "src/components/ui/Button/Button.tsx" -ItemType File -Force
    New-Item "src/components/ui/Button/Button.css" -ItemType File -Force

    New-Item "src/components/ui/Input/Input.tsx" -ItemType File -Force
    New-Item "src/components/ui/Input/Input.css" -ItemType File -Force

    New-Item "src/components/ui/Card/Card.tsx" -ItemType File -Force
    New-Item "src/components/ui/Card/Card.css" -ItemType File -Force

    New-Item "src/components/ui/Spinner/Spinner.tsx" -ItemType File -Force
    New-Item "src/components/ui/Spinner/Spinner.css" -ItemType File -Force

Created:

- `src/components/ui/index.ts`

Configured centralized exports for reusable UI components.

### W1.4 — Create Application Layout

Created the main application layout to provide a common structure for header, sidebar, and page content.

    New-Item -ItemType Directory -Path "src/components/layout/AppLayout" -Force

    New-Item "src/components/layout/AppLayout/AppLayout.tsx" -ItemType File -Force
    New-Item "src/components/layout/AppLayout/AppLayout.css" -ItemType File -Force

Created:

- `src/components/layout/index.ts`

Integrated the application layout with the main application shell.

### W1.5 — Create Header & Navigation

Created the application header with branding, primary navigation, and profile navigation.

    New-Item -ItemType Directory -Path "src/components/layout/Header" -Force

    New-Item "src/components/layout/Header/Header.tsx" -ItemType File -Force
    New-Item "src/components/layout/Header/Header.css" -ItemType File -Force

Added navigation links for:

- Home
- Alumni
- JNV
- Opportunities
- Profile

Installed React Router dependency for application navigation.

    npm install react-router-dom

### W1.6 — Create Sidebar & Responsive Navigation

Created the application sidebar with navigation links for major platform sections.

    New-Item -ItemType Directory -Path "src/components/layout/Sidebar" -Force

    New-Item "src/components/layout/Sidebar/Sidebar.tsx" -ItemType File -Force
    New-Item "src/components/layout/Sidebar/Sidebar.css" -ItemType File -Force

Added navigation for:

- Home
- Alumni
- JNV
- Opportunities
- Mentorship
- Events
- Community

Integrated the sidebar into the application layout.

### W1.7 — Configure React Router

Configured client-side routing using React Router and connected application pages with the layout.

Updated:

- `src/app/router.tsx`
- `src/app/App.tsx`

Configured the root application route and nested page routing.

### W1.8 — Configure Public Routes

Created initial public route pages and configured them in React Router.

    New-Item -ItemType Directory -Path "src/pages/Home","src/pages/Alumni","src/pages/JNV","src/pages/Opportunities","src/pages/Mentorship","src/pages/Events","src/pages/Community" -Force

Created:

- `HomePage.tsx`
- `AlumniPage.tsx`
- `JNVPage.tsx`
- `OpportunitiesPage.tsx`
- `MentorshipPage.tsx`
- `EventsPage.tsx`
- `CommunityPage.tsx`

Created:

- `src/pages/index.ts`

Configured public routes:

    /
    /alumni
    /jnv
    /opportunities
    /mentorship
    /events
    /community

### W1.9 — Configure Protected Routes

Created the protected route foundation for authenticated application areas.

    New-Item -ItemType Directory -Path "src/components/common/ProtectedRoute" -Force

    New-Item "src/components/common/ProtectedRoute/ProtectedRoute.tsx" -ItemType File -Force
    New-Item "src/components/common/index.ts" -ItemType File -Force

Created:

- `ProtectedRoute`

Created temporary Login and Profile pages for protected-route verification.

    New-Item -ItemType Directory -Path "src/pages/Login","src/pages/Profile" -Force

    New-Item "src/pages/Login/LoginPage.tsx" -ItemType File -Force
    New-Item "src/pages/Profile/ProfilePage.tsx" -ItemType File -Force

Configured:

    /login
    /profile

The `/profile` route is protected and currently redirects unauthenticated users to `/login`.

Real authentication and JWT integration will be implemented in Web Phase 3.

### W1.10 — Create Error & Not-Found Pages

Created application error and 404 pages to handle invalid routes and routing errors.

    New-Item -ItemType Directory -Path "src/pages/Error","src/pages/NotFound" -Force

    New-Item "src/pages/Error/ErrorPage.tsx" -ItemType File -Force
    New-Item "src/pages/NotFound/NotFoundPage.tsx" -ItemType File -Force

Created:

- `ErrorPage.tsx`
- `NotFoundPage.tsx`

Configured React Router with:

- `errorElement`
- Catch-all `*` route

Verified invalid routes display the 404 page correctly.

## Phase 1 Verification

- ESLint: Passed
- Prettier: Passed
- TypeScript: Passed
- Production build: Passed
- Development server: Passed
- Design system: Verified
- Global styles: Verified
- Reusable UI components: Verified
- Application layout: Verified
- Header navigation: Verified
- Sidebar navigation: Verified
- React Router: Verified
- Public routes: Verified
- Protected routes: Verified
- Error handling: Verified
- 404 page: Verified

## Phase 1 Status

**Completed**

## Phase 1 Commit

    git add .

    git commit -m "feat(web): Phase 1 - Complete UI foundation and routing"

    git push origin main

## Phase 2 — API & Application Foundation

### W2.1 — Configure API Client

Configured Axios as the centralized HTTP client for communication between the React application and backend APIs.

    npm install axios

Created:

- `src/services/api/client/apiClient.ts`

- `src/services/api/client/index.ts`

- `src/services/api/index.ts`

Configured:

- Base API URL from environment configuration

- Request timeout

- JSON content type

### W2.2 — Configure API Environments

Configured environment-specific API settings for local, development, staging, and production environments.

Created:

- `.env.development`

- `.env.staging`

- `.env.production`

Updated:

- `src/config/env.ts`

Configured:

- `VITE_APP_NAME`

- `VITE_API_BASE_URL`

- `VITE_APP_ENV`

Added environment variable validation to ensure required application configuration is available at runtime.

Updated `.gitignore` to protect local environment files and prevent environment-specific local configuration from being committed.

### W2.3 — Define API Types & Contracts

Created reusable TypeScript interfaces for API responses, API errors, authentication, users, and JNV data.

Created:

- `src/types/api/apiResponse.ts`

- `src/types/api/apiError.ts`

- `src/types/auth/auth.ts`

- `src/types/user/user.ts`

- `src/types/jnv/jnv.ts`

Created centralized barrel exports:

- `src/types/api/index.ts`

- `src/types/auth/index.ts`

- `src/types/user/index.ts`

- `src/types/jnv/index.ts`

- `src/types/index.ts`

Defined contracts for:

- Login request and response

- Refresh token request and response

- User information

- JNV information

- Generic API response

- API error response

### W2.4 — Create API Service Structure

Created a feature-oriented API service structure for authentication, users, and JNV operations.

Created:

- `src/services/api/auth/authService.ts`

- `src/services/api/auth/index.ts`

- `src/services/api/user/userService.ts`

- `src/services/api/user/index.ts`

- `src/services/api/jnv/jnvService.ts`

- `src/services/api/jnv/index.ts`

Configured API operations for:

- User login

- Refresh token

- Logout

- Get current user

- Get user by ID

- Get all JNVs

- Get JNV by ID

Created centralized API exports through:

- `src/services/api/index.ts`

The configured endpoint paths represent the frontend API contract and will be connected to the Spring Boot backend during backend integration.

### W2.5 — Configure TanStack Query

Configured TanStack Query for server-state management, API caching, request lifecycle handling, and asynchronous data management.

    npm install @tanstack/react-query

    npm install -D @tanstack/react-query-devtools

Created:

- `src/lib/query/queryClient.ts`

- `src/lib/query/index.ts`

Configured:

- Query stale time

- Query garbage collection time

- Query retry behavior

- Window focus refetch behavior

- Mutation retry behavior

Integrated `QueryClientProvider` into the application provider layer.

Updated:

- `src/app/providers.tsx`

Enabled React Query Devtools for development-time API state inspection.

### W2.6 — Configure Global Error Handling

Created centralized API error normalization and HTTP status handling utilities.

Created:

- `src/utils/error/apiError.ts`

- `src/utils/error/httpStatus.ts`

- `src/utils/error/index.ts`

Configured handling for common HTTP responses including:

- 400 Bad Request

- 401 Unauthorized

- 403 Forbidden

- 404 Not Found

- 409 Conflict

- 422 Unprocessable Entity

- 429 Too Many Requests

- 500 Internal Server Error

- 502 Bad Gateway

- 503 Service Unavailable

- 504 Gateway Timeout

Updated:

- `src/services/api/client/apiClient.ts`

Added an Axios response interceptor to normalize API errors into a consistent application-level error structure.

### W2.7 — Configure Loading & Empty States

Created reusable application-level components for loading, empty, and error states.

Created:

- `src/components/common/LoadingState/LoadingState.tsx`

- `src/components/common/LoadingState/LoadingState.css`

- `src/components/common/EmptyState/EmptyState.tsx`

- `src/components/common/EmptyState/EmptyState.css`

- `src/components/common/ErrorState/ErrorState.tsx`

- `src/components/common/ErrorState/ErrorState.css`

Updated:

- `src/components/common/index.ts`

Configured reusable states for:

- Loading API data

- Empty data collections

- API or application errors

- Optional action buttons

### W2.8 — Create Common Hooks & Utilities

Created reusable React hooks and utility functions required across the application.

Created:

- `src/hooks/useDebounce.ts`

- `src/hooks/useMediaQuery.ts`

- `src/hooks/index.ts`

Implemented:

- Debounced value handling

- Responsive media-query detection using `useSyncExternalStore`

Created formatting utilities:

- `src/utils/format/formatDate.ts`

- `src/utils/format/index.ts`

Implemented reusable date formatting using `Intl.DateTimeFormat`.

Created validation utilities:

- `src/utils/validation/validation.ts`

- `src/utils/validation/index.ts`

Implemented validation helpers for:

- Required values

- Email format

- Password length

Updated:

- `src/utils/index.ts`

Configured centralized exports for error handling, formatting, and validation utilities.

## Phase 2 Verification

- ESLint: Passed

- Prettier: Passed

- TypeScript: Passed

- Production build: Passed

- Git diff check: Passed

- Development server: Passed

- API client: Verified

- API environment configuration: Verified

- API types and contracts: Verified

- API service structure: Verified

- TanStack Query: Verified

- Global error handling: Verified

- Loading state: Verified

- Empty state: Verified

- Error state: Verified

- Common hooks: Verified

- Formatting utilities: Verified

- Validation utilities: Verified

## Phase 2 Status

**Completed**

## Phase 2 Commit

    git commit -m "feat(web): Phase 2 : API & Application Foundation"