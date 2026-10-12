# CivilService Zone — deploy package

This project keeps the supplied `index.html` and visual theme, and adds a Node/Express API for accounts, marketplace products, orders, provider listings, bookings, owner dashboard and OpenAI AI help.

## GitHub + Render setup
1. Upload the contents of this ZIP to a GitHub repository (the `package.json` and `server.js` must be in the repository root).
2. In Render create **New Web Service** and connect the repository.
3. **Root Directory:** leave blank if files are in repository root. If you upload this folder inside a parent repository, set Root Directory to `csz_project`.
4. **Build Command:** `npm install`
5. **Start Command:** `npm start`
6. Add Render Environment variables:
   - `OPENAI_API_KEY` = your key from Google AI Studio
   - `OWNER_KEY` = `My life maa` (you can choose a different private key)
   - `JWT_SECRET` = a long random secret (Render can generate one)
   - `OPENAI_MODEL` = `gpt-4.1-mini`
7. For persistent customer data, configure `DATABASE_URL` to a PostgreSQL database. Render Free filesystem is temporary, so local JSON fallback is not permanent.

Never place the real OpenAI key in `index.html`, GitHub, or a public screenshot. The AI request is sent through `/api/ai/ask` on the server.

## Current scope / important notes
- The supplied dashboard HTML is retained and OpenAI error instructions are updated.
- The API enforces one role per mobile number and separates Customer, Provider and Seller login roles.
- Product photo data is stored with JSON records; keep images small. For production-scale use, move photos to object storage and use a managed database.
- COD orders and booking/status changes are supported. Online payments, SMS OTP, identity verification, and production-grade referral coupon accounting are not configured.
- The Owner key is an access gate, not a substitute for changing `JWT_SECRET`, rate limiting, backups and a database before public commercial launch.
- A conceptual AI house-plan brief is not an approved construction drawing. Get local code and structural design checked by a qualified engineer/architect.


## Targeted fixes in this ZIP (2026-10-11)
- Fixed the global image-to-data helper so legacy `imgToData` calls and Seller/Provider photo uploads work (JPG/PNG/WEBP, max 4 MB).
- Routed Room Search, Transportation, Provider and My Bookings pages to the server-backed functions; booking records now show for the customer and provider.
- Updated marketplace login to share the server auth token with the Seller/Provider/Customer flows, so listing, booking and material endpoints receive the correct token.
- AI Help now uses OpenAI Responses API with `OPENAI_API_KEY` and `OPENAI_MODEL`. `/api/health` reports whether the key variable is present (not whether the key is valid).
- Ran server and embedded-script syntax checks, plus a local API flow test for seller product upload/visibility and provider/customer bookings.

### Render AI configuration
The backend reads `OPENAI_API_KEY` from Render Environment at runtime. Add that exact key name with your own OpenAI API key in the Render service Environment settings, save/deploy, then check `/api/health` for `aiConfigured: true`. Never put the secret in `server.js`, `index.html`, or GitHub.

## Update fixes (2026-10-11)
- Fixed My Bookings calling an out-of-scope `api` function; it now uses the shared server API client and saved customer session.
- Configured `gpt-4.1-mini` as the default OpenAI model in the server and Render configuration.
- This update ZIP contains website/server files only; Android wrapper is not included.


## OpenAI + permanent data storage update
- AI Help now calls the OpenAI Responses API from the server. Set `OPENAI_API_KEY` in Render Environment; optional model variable is `OPENAI_MODEL` (default `gpt-4.1-mini`). Never put the key in `index.html` or GitHub. OpenAI API usage may require billing and is separate from ChatGPT subscription.
- Registration popup now scrolls on mobile/desktop; successful registration/login handlers hide it.
- Persistent storage support added through PostgreSQL. Create a PostgreSQL database (Render Postgres or another provider), then set `DATABASE_URL` in the Render Web Service Environment to the database's internal/external connection string as appropriate. The app stores users, products/material listings, rooms/transport listings, bookings and orders in the `csz_app_state` table.
- If `DATABASE_URL` is not set, app falls back to local `data/db.json`; on Render Free this file can disappear after restart/spin-down/redeploy. To keep data permanently, configure `DATABASE_URL` before using the website. Existing data already lost from prior restarts cannot be recovered automatically.
- The shared AI answer cache remains in memory per running instance; it is separate from persistent business data.
