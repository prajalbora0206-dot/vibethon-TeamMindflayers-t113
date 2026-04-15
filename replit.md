# VibeLearn AI Workspace

## Overview

pnpm workspace monorepo using TypeScript. Contains the VibeLearn AI interactive AIML learning platform.

## Stack

- **Monorepo tool**: pnpm workspaces
- **Node.js version**: 24
- **Package manager**: pnpm
- **TypeScript version**: 5.9
- **API framework**: Express 5
- **Frontend**: React + Vite + Tailwind CSS v4
- **Database**: In-memory storage (no external DB required)
- **Validation**: Zod (`zod/v4`), `drizzle-zod`
- **API codegen**: Orval (from OpenAPI spec)
- **Build**: esbuild (CJS bundle)

## Key Commands

- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from OpenAPI spec
- `pnpm --filter @workspace/api-server run dev` — run API server locally
- `pnpm --filter @workspace/vibelearn-ai run dev` — run frontend locally

## Project Structure

```
artifacts/
  api-server/         # Express backend (in-memory data store)
    src/
      data/store.ts   # In-memory users, modules, quizzes, progress
      routes/
        auth.ts       # Register, login, logout, /me
        modules.ts    # Get modules list + detail
        quiz.ts       # Get quiz + submit answers
        progress.ts   # Get progress + mark module complete
  vibelearn-ai/       # React + Vite frontend
    src/
      pages/          # Home, Login, Register, Dashboard, Modules, Module Detail, Quiz
      lib/auth.tsx    # Auth context + token management
      components/     # Shared UI components
lib/
  api-spec/           # OpenAPI specification
  api-client-react/   # Generated React Query hooks
  api-zod/            # Generated Zod schemas
```

## Features

1. **Auth** — Register/Login with Bearer token stored in localStorage
2. **Learning Modules** — "Introduction to Machine Learning" with 4 sections (text, example, visual with chart)
3. **Quiz System** — 5 MCQs with instant feedback, score tracking, explanations
4. **Progress Dashboard** — Completed modules, quiz scores, total score, progress bars
5. **Gamification** — Point system (20pts/correct answer, 50pts/module complete), badges: Beginner, Quiz Taker, Perfect Score

## API Endpoints

- `POST /api/auth/register` — Create account
- `POST /api/auth/login` — Login
- `POST /api/auth/logout` — Logout
- `GET /api/auth/me` — Current user (requires Bearer token)
- `GET /api/modules` — List all modules
- `GET /api/modules/:id` — Module with sections
- `GET /api/quiz/:moduleId` — Quiz questions
- `POST /api/quiz/:moduleId/submit` — Submit answers, get results + badges
- `GET /api/progress` — User progress (requires auth)
- `POST /api/progress/complete-module` — Mark module complete (requires auth)

## Note

In-memory storage means data resets on server restart. This is by design for the prototype.
