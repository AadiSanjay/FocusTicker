# Decisions

Each entry has three lines: what we chose, what we rejected, and why.
Write the "why" in your own words; this file is interview prep.
Entries marked *(draft)* were seeded by Claude from the project plan. Rewrite
them in your own words before treating them as yours.

---

### 2026-11-22: Fixed time, variable scope *(draft)*
- **Chose:** about 170h ending mid-May 2027, split into cycles with time
  budgets and a cut list decided ahead of time.
- **Rejected:** a ~300h "everything, done properly" plan that ran to
  fall 2027.
- **Why:** the recruiting cycle that matters opens summer 2027. A finished,
  explainable project with real users beats a bigger unfinished one.
  (Basecamp's Shape Up: fixed time, variable scope.)

### 2026-11-22: Boring stack, no extra infrastructure *(draft)*
- **Chose:** one Node service, one Postgres database (Neon), managed hosting,
  about a dozen integration tests, minimal CI.
- **Rejected:** microservices, Redis, queues, GraphQL, staging, Kubernetes.
- **Why:** none of them solves a problem 79 users have. Each one adds things
  to learn and maintain, and adding them without a reason is a red flag in
  interviews.

### 2026-11-22: Server language: TypeScript + Node *(draft)*
- **Chose:** TypeScript on Node.js.
- **Rejected:** Python + FastAPI.
- **Why:** it's the same async model (Promises, the event loop) I already use
  in the extension. It's one language across the extension, server, and
  dashboard, so they can share code like the site list. It also has fewer
  hidden layers than FastAPI's automatic validation and dependency injection.
  Trade-off I'm accepting: I have to learn TypeScript too.

### 2026-11-22: Database: PostgreSQL *(draft)*
- **Chose:** PostgreSQL.
- **Rejected:** SQLite (single file, awkward on hosted servers with several
  instances); MongoDB and other document stores (our data is small and
  regular, so tables fit it).
- **Why:** per-site daily totals are rows with a fixed shape, and we need
  aggregation for the dashboard. Postgres is also the most common production
  SQL database, so the skill carries over.

### 2026-11-22: Plain SQL through `pg`, no ORM yet *(draft)*
- **Chose:** handwritten SQL with the `pg` library.
- **Rejected:** Prisma, Drizzle, and other ORMs, for now.
- **Why:** an ORM writes SQL for you. I want to understand the queries first,
  so I can tell later what an ORM is doing and when it's doing it badly.

### 2026-11-22: The extension stays JavaScript *(draft)*
- **Chose:** keep the extension in plain JavaScript.
- **Rejected:** migrating it to TypeScript now.
- **Why:** it works and has users. Migrating would add a build step and risk
  to tracking accuracy without adding features. Revisit when we add sync code.

### 2026-11-22: Store only per-site daily totals *(draft)*
- **Chose:** store (site domain, date, seconds) on the server.
- **Rejected:** URLs, page titles, and per-visit event logs.
- **Why:** it's the least data that still powers sync and the dashboard.
  Less data means less to leak, a simpler privacy policy, and easier deletion.

### Open
- **Fastify or Express:** decide at the start of Phase 1, after comparing them.
- **Hosting:** decide in Phase 4, after comparing current free tiers.
