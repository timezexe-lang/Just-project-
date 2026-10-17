# REAL LIFE ONLINE: CRIME, MONEY & POWER

A mobile-friendly, single-player city roleplay game where players build a character, earn job salaries, manage cash and bank savings, and see upcoming city systems.

## Run & Operate

- Use the existing Replit workflows to run the game preview and API server.
- `pnpm --filter @workspace/real-life-online run dev` — run the Vite web app (requires workflow-provided `PORT` and `BASE_PATH`)
- `pnpm --filter @workspace/api-server run dev` — run the Express API (requires workflow-provided `PORT`)
- `pnpm run typecheck` — typecheck libraries and artifacts
- `pnpm run build` — typecheck and build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from the OpenAPI spec
- Required secret: `SESSION_SECRET`
- SQLite file defaults to `artifacts/api-server/data/real-life-online.sqlite` (ignored by Git); set `SQLITE_PATH` to override it.
- To try it, create an account in the browser, check the $10,000 cash / $20,000 bank starting balances, take a shift, use the bank, visit Vehicle Dealership, buy a vehicle with cash, and check My Garage.
- Vehicle purchases use cash only; transfer money from the bank first if needed. Purchase requests are idempotent, each player can own one of each model, and the first vehicle is active automatically.
- Select another owned vehicle in My Garage to switch the active vehicle. Ownership and the active selection persist through logout/login.

## Stack

- pnpm workspaces, Node.js 24, TypeScript 5.9
- Web: React + Vite, responsive CSS
- API: Express 5
- DB: local SQLite via Node's built-in `node:sqlite`
- Passwords: bcrypt hashes; server-side sessions stored in SQLite
- Validation: generated Zod schemas from OpenAPI
- API codegen: Orval (from OpenAPI spec)
- Build: Vite and esbuild

## Where things live

- `artifacts/real-life-online/` — browser game interface and preview
- `artifacts/api-server/src/routes/auth.ts` — registration, login, logout, and current-player routes
- `artifacts/api-server/src/routes/game.ts` — dashboard, jobs, salary, and bank routes
- `artifacts/api-server/src/routes/vehicles.ts` — authenticated dealership purchases and personal garage routes
- `artifacts/api-server/src/lib/vehicle-data.ts` — vehicle catalog and player-owned vehicle queries/response mapping
- `artifacts/api-server/src/lib/sqlite.ts` — SQLite database, schema, starter jobs, vehicle tables, and session store
- `lib/api-spec/openapi.yaml` — API contract; generated client and validation schemas live under `lib/`

## Product scope

- Registration, login, logout, character stats, starting balances, job shifts, salaries, bank transfers, vehicle purchases, a personal garage, and recent activity are implemented.
- Properties, businesses, police, crime, and government roleplay are visibly marked as coming soon.
- The game is single-player; it does not currently have multiplayer, shared worlds, or live player presence.
- Passwords are never returned by the API or stored in plain text.

## Pointers

- See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details
