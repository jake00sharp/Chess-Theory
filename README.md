# Chess Theory Trainer

I created a lightweight, client-side web app for practicing chess opening theory. It's designed to be a mode to practice instead of a wiki or YouTube video. Select lines, hit start, get instant feedback on your precision. All of this was created in fewer than 24 hours!

### Origin Story

My goal began as I started to learn the Kings Indian Defense from black's perspective. I learn best through repetition. I found it silly to skip around thorugh educational videos and ineffective to wait for the perfect game. My goal was simple: let me practice the lines I want, when I want, against another player (a bot). Here is my best effort to create such a resource.

## What We Are

**Repeatedly train different positions** from selected opening lines.
Create your own **personal repertoire** and practice!
**Detect when you stray from theory** and correct it in the moment.
**Finish the game**, if you choose, against Stockfish. Experience the middle- and end-games from your very own openings.

## What We Are Not

**No backend, no accounts, no secrets.** Everything persists locally in the browser.
Clearing site data wipes your Custom Book.
Our database is populated with my favorite openings. It by no means is exhaustive. The purpose is educational in nature.

## Tech Stack

- **Frontend:** React + TypeScript + Vite + TailwindCSS + react-router
- **Chess Logic/UI:** chess.js + react-chessboard
- **Engine:** Stockfish (WASM) running in a Web Worker
- **Testing:** Vitest + React Testing Library
- **Docs:** VitePress + TypeDoc
- **Tooling:** pnpm + ESLint + Prettier + Docker
- **CI/CD:** GitHub Actions

## Repo Layout

- `apps/web` — the web app
- `packages/core` — book manager, policy layer, engine adapter interface, storage wrapper, shared types
- `docs/` or `apps/docs` — developer docs source, generated site output

## Local development

### Prereqs:
- Node (LTS recommended)
- pnpm

### Run:
- From root:
  - `pnpm install`
  - `pnpm dev`
  - `pnpm test`
  - `pnpm build`
- Directly from apps:
  - `pnpm -C apps/web install`
  - `pnpm -C apps/web dev`

## License

GPL (see `LICENSE`).
