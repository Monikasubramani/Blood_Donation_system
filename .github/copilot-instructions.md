# Copilot / AI Agent Instructions for Social Welfare Connect

This repository is a small full-stack Express + MongoDB app serving static client pages in `public/`.
Follow these concise rules and examples to be productive quickly.

## Big picture
- Backend: `server.js` (single Express app). It defines Mongoose schemas (User, Blood/Organ/Money Donor/Receiver) and all REST endpoints under `/api/*`.
- Frontend: static HTML/JS in `public/` (no build step). Client code calls backend APIs via `fetch` and uses `localStorage` (key: `currentUser`) for session state.
- Persistence: MongoDB with connection string provided via `.env` (`MONGO_URI`).

## How to run / debug locally
- Install deps: `npm install` (see `package.json`).
- Create `.env` with `MONGO_URI` (and optional `PORT`). Example in `README.md`.
- Start: `npm start` (runs `node server.js`). Default port: `3000`.
- Logs: server prints `MongoDB connected` and `server is running on ...` to stdout. Check these first when troubleshooting.

## Key conventions & patterns (do NOT change lightly)
- Phone number is the primary identity: always 10 digits, validated on both client and server (`/api` routes expect `phone` as `\d{10}`).
- Authentication uses phone + password stored in MongoDB; passwords are hashed with `bcryptjs` (saltRounds = 10).
- Client-side OTP: Firebase handles OTP verification in `public/login.html`. The client still calls `/api/login` with phone+password after OTP.
- Verification workflow: many resources carry `verificationStatus` with enum `pending|approved|rejected`. Admin endpoints operate on `type` strings mapping to models (e.g. `blood-donor`).
- Image/data uploads: client often sends base64 images (e.g. `profilePhoto`, `verificationFile`) and server body parser limit set to `10mb` in `server.js`.

## Useful API examples (copy-paste-ready)
- Register: `POST /api/register` JSON -> { name, phone, password, profilePhoto }
- Login: `POST /api/login` JSON -> { phone, password }
- Get user: `GET /api/user/:id` (returns user without password)
- Admin verify: `POST /api/admin/verify` JSON -> { type, id, status: 'approved'|'rejected', notes }
- Pending verifications: `GET /api/admin/pending-verifications`

## What I expect an AI/code suggestion to respect
- Preserve `phone` validation and `verificationStatus` enum semantics.
- Keep `bodyParser` limits or, if changing, update client expectations for file/base64 sizes.
- Preserve localStorage key `currentUser` unless doing a coordinated migration across all pages.
- Use existing route shapes — ADD new endpoints rather than change existing ones unless asked.

## Files to inspect for context before edits
- `server.js` — primary source of truth for data models and API behavior
- `public/*.html` — client-side flows, Firebase OTP details (`login.html`), admin verification UI (`admin-verification.html`)
- `README.md` — setup and examples

## Quick troubleshooting notes
- If Mongo fails to connect: confirm `.env` and `MONGO_URI`. Server prints the connection error.
- If image uploads/truncated JSON: check `bodyParser` limits in `server.js` (currently 10mb).

If any of these assumptions are inaccurate or you want different guidance (for example: migrate session handling away from `localStorage` or replace Firebase OTP), tell me which area to update and I will regenerate the instructions.
