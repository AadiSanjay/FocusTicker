# FocusTicker roadmap

**Build deadline:** mid-May 2027 (end of spring semester).
**Recruiting-ready:** end of June 2027, before the Summer 2028 internship
cycle opens (about July–September 2027).
**Budget:** about 8 hours/week, which is roughly **170–190 hours** after
finals and slippage.

The rule, from the research (`reports/Student project advice for recruiting.md`):
**the time is fixed, the scope gives.** Each cycle has an *appetite* (a time
budget). If a cycle runs over, cut scope from the cut list. Don't extend the
date.

## What we're optimizing for
1. **Real users and steady shipping.** 79 users, 5★, and a dated release
   history are the project's main recruiting asset, and they're hard to fake.
2. **One honestly hard backend slice I can defend line by line.** Interviewers
   now ask "why" follow-ups specifically to catch code you didn't write.
3. **Boring engineering.** One Node service, one Postgres database, managed
   hosting, about a dozen tests on the risky logic, and a tiny CI file. No
   microservices, Redis, Kubernetes, GraphQL, staging environment, or Docker
   in production.

## How we work (unchanged)
- I hand-write the first version of every new concept (tutor mode). AI does
  repeats, config, and UI after I understand the pattern.
- Form my own hypothesis before pasting any error. Never commit code I can't
  explain.

---

## The schedule

| Cycle | When (approx.) | Appetite | Ships |
|---|---|---|---|
| 0. Resume + v1 explain-back | this week → early Dec | ~8h | Fix the privacy-policy link; update the resume numbers; explain v1's AI-written parts myself |
| 1. Attention timer | now → mid-Dec | ~16h | **v1.1**: color shift, pulse, soft limit, settings |
| 2. Local history | winter break | ~30h | **v1.2**: stats popup, 30–90 days of history, correct midnight handling, onboarding |
| 3. Custom sites | late Jan → Feb | ~24h | **v1.3**: custom sites via optional permissions, x.com fix. SQLBolt alongside |
| 4. Walking skeleton | Mar → early Apr | ~40h | Deployed API + Postgres; a dev build on 2 Chrome profiles shows a summed total |
| 5. Real accounts | Apr → early May | ~35h | **v2.0** submitted: Google sign-in, opt-in sync, delete-my-data, updated privacy policy |
| 6. Polish | May → June | ~25h | Store review buffer, a one-page dashboard, README + GIF, write-up |
| | | **~170h** | |

### Cut list (decided now, used in this order if behind)
1. The dashboard shrinks to a "synced from N devices" line in the popup.
2. Onboarding polish shrinks to the welcome page only, no tooltip.
3. The soft limit in v1.1 goes, keeping the color shift and pulse.
4. Custom sites moves after v2.0.

**Never cut:** tests on auth, cross-user isolation, and sync retries, or the
permission check before each release.

### Not in this plan (and why)
- **Metrics phase:** sync will be opt-in, so server data would only cover some
  users. Use the store's weekly-users count. Maybe revisit in summer.
- **React dashboard, OpenAPI spec, staging, E2E suite, structured-logging
  stack:** each is real work with no payoff at 79 users.
- **Converting the extension to TypeScript:** it's about 1,300 lines and
  works. The server is TypeScript, and that's where I'll learn it.

---

## Cycle 0: Resume + v1 explain-back (~8h)
- **First, fix the privacy policy link.** The GitHub Pages URL returns 404
  (see HISTORY.md). Check which URL the store dashboard uses, and publish the
  policy as a real page.
- **v1 explain-back** (tutor mode, ~5h). These parts were mostly
  ChatGPT-written but appear on my resume. For each one, I explain it out
  loud, predict what breaks if it's removed, then remove it and check:
  `refreshQueue`, `storage.session` + the checkpoint split, the `await`
  ordering, `WINDOW_ID_NONE` handling, `return true` in the message listener,
  Shadow DOM, and pointer capture in the drag code.
- Bullet: *"Built and shipped FocusTicker, a Chrome extension with 79 users
  (5.0★) that tracks active time on social sites"*, with the name linked to
  the store page.
- Apply to programs still open for first-years (e.g., Ford Ignite, deadline
  around Jan 1, 2027) plus mid-size companies and startups.
- Keep up weekly LeetCode-style practice outside the 8 project hours. No
  project replaces the coding round.

## Cycle 1: Attention timer → v1.1 (~16h)
1. **Minimal guardrails** (agent mode, ~3h): ESLint, plus a GitHub Actions
   file that runs lint on push.
2. **Settings** (tutor mode): `storage.sync` with defaults, plus a small
   options page.
3. **Color stages** neutral → amber → red, with thresholds from settings.
4. **Pulse** every N minutes (default 10), using `transform` only, so it never
   shifts page layout. Respects `prefers-reduced-motion`. Test on YouTube.
5. **Soft limit** (first on the cut list for this cycle). It never blocks.
6. **x.com support** (my spec, 2026-11-23): X should be on for new installs,
   and existing users should get a "what's new" summary. Design still to
   decide (see the trade-off below).
7. **What's new page:** `runtime.onInstalled` with reason `"update"` opens a
   one-screen summary of new features. Only for feature releases, never for
   patch fixes, to stay non-intrusive.
8. Ship, then reply to the people who asked for it.

**x.com trade-off (decide before coding):**
- *Static manifest:* new installs get X automatically. But the update adds a
  host warning, so Chrome likely **disables FocusTicker for all existing users
  until they accept**, and some won't.
- *Optional permission:* the welcome page (new installs) and the what's-new
  page (existing users) each get a "Turn on X" button that calls
  `permissions.request`. That's one click, and nobody gets disabled. It needs
  `optional_host_permissions` + `scripting`. Verify `scripting` shows no
  warning. Cycle 3's custom sites reuse the same mechanism.
- Before shipping either one, preview the permission warnings using Chrome's
  documented method.

## Cycle 2: Local history → v1.2 (~30h, winter break)
1. **Pull the time math into pure functions** (no Chrome API calls) and add
   **Vitest** tests with a fake clock. This is where testing starts, because
   the midnight split is the risky logic.
2. **Storage redesign** (tutor mode, spec first): per-day, per-site totals
   kept for 30–90 days. **This becomes exactly the shape sync uploads later.**
3. Split sessions that cross midnight between the two days.
4. Migrate existing users' `usage` data without losing today.
5. **Popup** (the `action` manifest key, no new permission): today's total,
   per-site breakdown, last 7 days.
6. **Onboarding:** `onInstalled` opens a one-screen welcome page.
7. Add the tests to CI.

## Cycle 3: Custom sites → v1.3 (~24h)
1. Add/remove domains with validation and normalization
   (`https://www.Reddit.com/r/x` → `reddit.com`), and toggle built-in sites.
2. `optional_host_permissions` + `permissions.request` when the user adds a
   site, + `scripting.registerContentScripts`. **Check that the update shows
   no new install warning**; if it did, all 79 installs would be disabled
   until users accept.
3. One source of truth for the site list.
4. Reuse the optional-permission flow from x.com (Cycle 1).
5. **Side track:** SQLBolt (about 8h over this cycle) plus a few curl requests
   against a toy API. This replaces the old Phase 0.

## Cycle 4: Walking skeleton (~40h)
The goal is one thin path through every layer working end to end, before any
real login.
1. Decide Fastify vs. Express and record it in DECISIONS.md.
2. `backend/`: Node + TypeScript (strict), Vitest, local Postgres for
   dev/test, Neon for production.
3. Schema on paper → first migration, by hand.
4. **Sync design question, answered by me on paper first:** how do two
   devices and retried requests avoid double-counting? Then the upsert
   endpoint, by hand.
5. Temporary **hard-coded dev token** in place of auth.
6. Deploy to an always-on host (free tiers that sleep break background sync),
   with secrets in environment variables.
7. The extension's dev build syncs from an `alarms` timer through
   `refreshQueue`, with an offline outbox and retry.
8. Integration tests: retries are idempotent, two devices sum correctly.
   Migrations run in CI.

**Done means:** two Chrome profiles show the correct combined total after
forced retries. If this isn't working by early April, cut, don't extend.

## Cycle 5: Real accounts → v2.0 (~35h)
1. Google sign-in via `chrome.identity`. Keep the manifest `key` stable so the
   extension ID matches the OAuth client.
2. Server verifies the ID token with Google's library (checks `aud`, `iss`,
   `exp`) and keys users on `sub`, not email.
3. Small sessions table of our own, plus middleware. Every query is scoped to
   the signed-in user.
4. `DELETE /me`: delete all of a user's data.
5. Tests: signed-out requests get 401, and user A can't read user B's data.
6. Rate limiting on auth and sync routes, CORS locked down, free-tier error
   tracking, and one real backup restore.
7. Sync **opt-in and off by default**. Permissions optional. Update the
   privacy policy and store disclosures. Submit **one** store update for all
   backend changes.

## Cycle 6: Polish (~25h)
- Store review buffer and bug fixes from real users
- One read-only dashboard page (first on the cut list)
- README: GIF at the top, why the project exists, a small architecture
  diagram, key decisions, known limitations, and a "How I used AI" note that
  includes one bug the AI introduced and how I caught it
- One write-up on the hardest bug or the sync design
- Rehearse a 2-minute and a 10-minute walkthrough, including "what would you
  reverse today?"
- Before interviews: re-implement the sync endpoint from scratch with no AI

## Not code (reminders)
- Record a 15–30s GIF of the timer for the store listing.
- Rewrite the store description so its first lines say what happens in the
  first minute. **No list of site brand names**; that got v1 rejected for
  keyword spam.
- Track installs ÷ listing views before and after the listing changes.
