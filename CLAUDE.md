# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

A small Express REST API for users (in-memory data), used as the starter repo for the Claude Code course.

## Commands

- `npm run dev`: start the API on http://localhost:3000 and restart it when files change (`node --watch`)
- `npm test`: run all tests (Node's built-in test runner, `node --test`)
- `node --test --test-name-pattern="404"`: run only the tests whose names match the pattern
- `npm run lint`: run ESLint; CI fails on lint errors

## Architecture

- `server.js` builds the Express app, mounts one router per resource (`/users` → `routes/users.js`, `/health` → `routes/health.js`), and exports `app`. It only calls `listen()` when run directly, so tests import `app` without opening a port.
- Routes never hold data themselves; they call functions in `db/store.js`, an in-memory array that resets on every restart. Nothing is persisted.
- Tests in `tests/` use `supertest` against the exported `app`, so a running dev server doesn't interfere with them.

## Conventions

- Use CommonJS (`require` / `module.exports`), not ES modules. ESLint is configured with `sourceType: "script"`.
- Add a new resource as its own file in `routes/` with an `express.Router()`, and mount it in `server.js`.
- Access data only through functions exported from `db/store.js`; don't read or write the `users` array from routes.
- Send errors as JSON `{ "error": "<message>" }` with the matching status code (400 for invalid input, 404 for not found). Respond 201 when something is created.
- Write tests with `node:test` and `node:assert` plus `supertest`. Don't add Jest or Mocha.
- `PORT` comes from the environment (see `.env.example`). Never read or commit `.env`.
