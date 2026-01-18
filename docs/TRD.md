# Technical Requirements Documentation
## Chess Theory Trainer

Status: Draft
Owner: Jacob Sharp
Last updated: 01-17-2026

## 1. Summary

**Purpose:** This web app helps users practice chess theory. It focuses on repeated training of established book openings and user-defined personal repertoires.

**Objectives:** Ship a lightweight, client-side web application deployed to GitHub Pages. This MVP must be developed and usable in fewer than 24 hours.

## 2. Scope

This MVP is a static, client-only app. It is a monorepo with Docker-based local dev and GitHub Actions for build/test/deploy.

This is a public, portfolio / education project. We are fine going GPL and staying fully open-source.

The MVP includes:
- A training loop that drills selected opening theory.
- A Custom Book editor that lets the user add their own lines to be included in training.
- In-browser Stockfish plays against user after diversion from theory.
- Basic test coverage.
- An auto-generated developer documentation site.

## 3. Product Behavior

This app should feel like practice, not browsing theory.

A user should be able to:
1) Pick openings and specific lines to practice.
2) Hit start and immediately begin.
3) Get instant feedback on precision.
4) Add lines to their Custom Book.
5) Continue playing beyond the opening.

## 4 Functional Requirements

This section is a list of requirements with acceptance criteria. Anything not listed is not required for the MVP.

Acceptance criteria can be found in GitHub Projects.

### 4.1 Chess Gameplay
**REQ-001:** User is able to play chess against a bot with full game functionality.

### 4.2 Training Selection
**REQ-002:** User may select one or more openings to practice from a bundled collection of theory lines.
**REQ-003:** User may select specific lines/variations within an opening when available.

**REQ-004:** User may toggle to include/exclude Custom Book content in training.

### 4.3 Training Loop
**REQ-005:** User may run a theory drill loop over the user's selected opening(s)/line(s).

**REQ-006:** App detects when the user diverges from theory.

**REQ-007:** Move hint suggests different moves in the current position that follow theory.

### 4.4 Engine Takeover
**REQ-008:** After divergence from theory, the app offers an option to continue against the engine from the current position.

**REQ-009:** Engine only runs after divergence from theory.

**REQ-010:** The engine runs client-side and does not block the main thread.

### 4.5 Custom Book
**REQ-011:** User may create and edit a Custom Book locally.

**REQ-012:** User can paste a FEN to add to their Custom Book.

## 5. Constraints and Assumptions

This is a GitHub Pages app which disallows a backend. There are no accounts or secrets. Everything persists locally in the browser. If the user clears site data, their Custom Book is gone. The engine runs fully client-side and must not block the UI thread. The app should remain responsive while the engine is thinking.

The bundled theory set is intentionally small of my personal favorites. The point is to demonstrate the training loop and system design. There are other massive opening databases.

This repo is GPL as are many of the dependencies. This project is created to be public, educational, and portfolio-first.

## 6. System Design

This app has four major internal components:
- **Game Controller:** owns the board state, legal moves, turn handling, and move history.
- **Book Manager:** owns the opening theory lookup and decides bot moves while the game is still inside theory which includes a storage layer for local persistence.
- **Policy Layer:** decides whether the game is still “in theory” or in "out of theory” state; gates engine adapter.
- **Engine Adapter:** wraps Stockfish running in a web worker.

**General Structure:**
- `apps/web`: the web app
- `packages/core`: Book Manager, Policy Layer, Engine Adapter interface, storage wrapper, shared types
- `apps/docs` or `docs/`: developer docs site input + generated output

**CI:**
- lint
- typecheck
- unit tests
- build
- deploy (on main)

## 7. Tech Stack

### 7.1 Repo + Tooling
- **Node:** Node LTS (target Krypton)
- **Package Manager:** pnpm
- **Lint/format:** ESLint + Prettier
- **Typecheck:** TypeScript
- **Local Dev:** Dockerfile and Wrapper

### 7.2 Frontend (`apps/web`)
- **Language:** TypeScript
- **Framework:** React
- **Build tool:** Vite
- **Styling:** TailwindCSS
- **Routing:** react-router
- **Chess:** chess.js
- **Board UI:** react-chessboard
- **State:** React State
- **Persistence:** LocalStorage
- **Engine:** Stockfish (WASM build) in a Web Worker

### 7.3 Testing
- **Unit/Integration Runner:** Vitest
- **UI Test Utilities:** React Testing Library

### 7.4 Documentation (auto-generated)
- **Site:** VitePress (`/docs`)
- **API/Type:** TypeDoc

### 7.5 CI/CD
- **PR Checks:** lint, typecheck, unit tests, build
- **Deploy:** build and deploy `apps/web` to GitHub Pages
- **Docs Deploy:** build and deploy documentation
