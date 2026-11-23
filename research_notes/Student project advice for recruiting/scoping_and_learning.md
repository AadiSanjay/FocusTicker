# Scoping, Sequencing, and Learning New Tech Through a Real Project (Student, ~8 hrs/wk, Nov 2026 to May 2027)

Context: a live Chrome extension (79 users, all 5-star) that tracks time on social sites. Planned work: user-requested features (timer color shift/pulse, daily stats popup with local history, custom sites, onboarding), then a TypeScript/Node/Postgres backend with Google sign-in, cross-device sync, and a web dashboard. Budget: about 8 hrs/week x about 24 weeks, so roughly 190 hours in total, before exams and slippage.

## Tutorials vs project-based learning ("tutorial hell"); how much upfront study before building

### Takeaway
Practitioners and educators broadly agree: learn by building a real project, and use tutorials and docs "just in time" when you get stuck. A short, bounded dose of upfront basics is fine (for example SQLBolt's 18 lessons, which take days, not weeks). For TypeScript, the usual advice is to convert the existing JS codebase file by file rather than take a course first.

### Cited Findings
- The test for whether you are in tutorial hell: look at your last project and ask whether you can explain what the tools you used actually do — [freeCodeCamp](https://www.freecodecamp.org/news/how-to-learn-from-coding-tutorials-and-avoid-tutorial-hell/)
- Suggested split of about 20% tutorials/docs and 80% building. Learn on demand: when you hit a roadblock, learn just enough to get past it, then return to the project — [daily.dev](https://daily.dev/blog/how-to-escape-tutorial-hell/), [freeCodeCamp](https://www.freecodecamp.org/news/how-to-break-free-from-tutorial-hell/)
- "Keep it simple, start with what you know, then go just a little bit beyond your comfort zone." One freeCodeCamp author says a personal-problem project was too much as a total beginner. (The student here is already past that stage: the project already ships.) — [freeCodeCamp](https://www.freecodecamp.org/news/how-to-break-free-from-tutorial-hell/)
- Boot.dev suggests a first project of about 20–40 hours — [Boot.dev on DEV](https://dev.to/bootdotdev/build-your-first-coding-project-and-avoid-tutorial-hell-ioa)
- Backend advice from a freeCodeCamp forum reply: start building APIs right after basic routing, and leave auth until you can pass data between a client and a database — [freeCodeCamp forum](https://forum.freecodecamp.org/t/what-should-a-beginner-focus-on-when-learning-backend-development/799729)
- "Stop learning backend by tutorials — build one boring system" until it is battle-ready — [DEV](https://dev.to/myroslavmokhammadabd/stop-learning-backend-by-tutorials-build-one-boring-system-instead-f6). Beginners who avoid SQL by picking NoSQL end up learning SQL "the hard way" later — [DEV](https://dev.to/matteodem/most-beginners-learn-full-stack-development-backwards-4128)
- SQLBolt: 18 browser-based lessons, each with interactive exercises, no setup. HN commenters recommend it for picking up the basics quickly — [SQLBolt](https://sqlbolt.com/), [SaaSHub mentions aggregator](https://www.saashub.com/sqlbolt). A critique: it teaches syntax well but hides real-world messiness, and its datasets are small — [Scrimba guide 2026](https://scrimba.com/articles/how-to-learn-sql-a-practical-guide-for-beginners-2026/)
- SQL basics take about 1–2 weeks of consistent practice; practical proficiency takes about 1–3 months (vendor guide, so treat as a rough estimate) — [Scrimba 2026](https://scrimba.com/articles/how-to-learn-sql-a-practical-guide-for-beginners-2026/)
- The Odin Project's Node course sequence: Authentication Basics (sign-up/login/logout with Passport), then the "Members Only" project (PostgreSQL plus auth, deployed to a PaaS), then the Odin-Book capstone. In other words, an established curriculum teaches Node/Postgres/auth by building — [TOP Members Only](https://www.theodinproject.com/lessons/node-path-nodejs-members-only), [TOP Auth Basics](https://www.theodinproject.com/lessons/node-path-nodejs-authentication-basics)
- The TypeScript handbook's official migration path: set `allowJs` so JS and TS can import each other, turn on checking gradually (`// @ts-check` per file, then `checkJs`), and rename .js to .ts one file at a time, starting with small utility modules — [TypeScript Handbook: Migrating from JavaScript](https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html), [Microsoft TS blog (2019)](https://devblogs.microsoft.com/typescript/how-to-upgrade-to-typescript-without-anybody-noticing-part-1)
- Counterpoint: one 2026 migration guide says migration is often not worth it for projects under about 1,000 LOC or quick prototypes — [OneUptime 2026](https://oneuptime.com/blog/post/2026-01-24-migrate-javascript-to-typescript/view)

### Inferences
- Recommended upfront study is small and bounded: SQLBolt (about 4–6 hours across 1–2 weeks at this pace) plus the TS handbook's "TS for JS programmers" page. Everything else should be learned inside the project.
- Learn TS on the extension first, on code the student already understands. That separates "learning the type system" from "learning the backend," so they are not fighting two unknowns at once. If the extension is very small (under about 1k LOC), start TS in the new backend instead.
- Follow the forum advice literally: get Express/Fastify returning JSON from Postgres before touching Google OAuth.

### Gaps
- No rigorous study (as opposed to practitioner opinion) comparing tutorial-first and project-first learning for backend/SQL turned up. The evidence is anecdotal and blog-level.
- No 2024–2026 Pragmatic Engineer article specifically on student learning strategy was found in searches.

## Scoping methods for solo projects with deadlines (MVP, vertical slices, walking skeleton, Shape Up appetite)

### Takeaway
Fix the time and vary the scope. Set an "appetite" (a time budget) per chunk, build a thin end-to-end slice first (a walking skeleton), and start with the part that is core, small, and novel, not with login or setup. Cutting scope is the default response to slipping. Extending time is not.

### Cited Findings
- Shape Up: "Estimates start with a design and end with a number. Appetites start with a number and end with a design." Time is fixed and scope varies. Cycles are small batch (1–2 weeks) or big batch (6 weeks) — [Shape Up ch. 3, Set Boundaries](https://basecamp.com/shapeup/1.2-chapter-03) (Basecamp, 2019)
- "Scope hammering" means forcefully questioning a design, implementation, or use case to cut scope and finish inside the fixed time box — [Shape Up ch. 3](https://basecamp.com/shapeup/1.2-chapter-03)
- Shape Up "Get One Piece Done": aim for something tangible and demoable within about the first week by integrating one front-end and back-end slice. Stubbed data, hard-coded values, and temporary auth are fine at first. "First make it work, then make it beautiful." — [Shape Up ch. 11](https://basecamp.com/shapeup/3.2-chapter-11)
- Shape Up "start in the middle": don't start with setup like login. Pick work that is core, small (a few days), and novel ("prefer the thing that you've never done before") because it removes the most uncertainty — [Shape Up ch. 11](https://basecamp.com/shapeup/3.2-chapter-11)
- Walking skeleton (Alistair Cockburn, 1990s, in *Crystal Clear*): "a tiny implementation of the system that performs a small end-to-end function," linking the main architectural components so architecture and functionality can evolve in parallel. Cockburn reportedly put build time at 20 minutes to 2 weeks — [Code Climate](https://codeclimate.com:443/blog/kickstart-your-next-project-with-a-walking-skeleton), [Henrico Dolfing](https://henricodolfing.com/2018/04/start-your-project-with-walking-skeleton.html), [O'Reilly 97 Things](https://oreilly.com/library/view/97-things-every/9780596800611/ch60.html)
- Gojko Adzic's variant, "put it on crutches": ship the skeleton with manual or temporary pieces, then replace them — [gojko.net (2014)](https://gojko.net/2014/06/09/forget-the-walking-skeleton-put-it-on-crutches/)
- Practitioners vary in how they define the walking skeleton (prototype vs production code) — [Ben's Guide](https://bensguide.substack.com/p/walking-skeleton)

### Inferences
- Applying Shape Up's "start in the middle" to this backend: the core, novel piece is "a day's usage totals leave the extension and land in Postgres, and come back on a second device." Google sign-in is the setup work Shape Up says not to lead with. For the first slice, a hard-coded dev user/token is acceptable (Shape Up explicitly allows temporary auth).
- A suggested appetite plan for about 190 hours:
  - **Cycle A (about 3 weeks, about 24 hrs):** user-requested extension features (timer color shift/pulse, custom sites). Small batch, shipped to the 79 users.
  - **Cycle B (about 3 weeks):** daily stats popup with local history, plus onboarding. This also defines the local data model (per-day, per-site rows) that sync will later upload, so it is not throwaway work.
  - **Cool-down/learning (about 1–2 weeks):** SQLBolt and TS conversion of the extension.
  - **Cycle C (about 6 weeks, about 48 hrs):** walking skeleton: Node+TS API, Postgres, a deployed endpoint, the extension posting day-totals with a dev token, and a minimal dashboard page reading them.
  - **Cycle D (about 6 weeks):** real Google sign-in, multi-device merge, and permission/privacy updates.
  - **Buffer (about 3–4 weeks):** exams, Chrome Web Store review, polish.
- Pre-decide the cut list in priority order: (1) web dashboard → replace with popup "synced from N devices" or a single read-only page; (2) a cross-device "live" sync → a daily batch upload; (3) onboarding polish.

### Gaps
- No 2024–2026 source specifically addresses solo student use of Shape Up. The adaptation above is inference.

## Shipping cadence: small increments to real users vs one big release

### Takeaway
All the scoping sources favor small, demoable, deployed increments. For this student the existing 79-user base is an unusual asset: shipping the requested features in small releases keeps ratings high and produces evidence of use, which career sources say makes projects stand out. One caveat: each Chrome Web Store submission costs review time, so batch releases somewhat, especially any that add permissions.

### Cited Findings
- Shape Up's emphasis is on making something "tangible and demoable early" rather than finishing layers separately — [Shape Up ch. 11](https://basecamp.com/shapeup/3.2-chapter-11)
- Career guidance: new grads should have substantive (non-tutorial) projects, and evidence that people use the project (user numbers, validation) makes it stand out. Skip a project that was only a followed tutorial — [Simplify](https://simplify.jobs/blog/sofware-engineer-side-projects), [CodePath](https://codepath.org/news/how-to-have-side-projects-that-stand-out-and-why), [techinterview.org](https://www.techinterview.org/post/3233474610/side-projects-open-source-engineering-resume/?format=md)
- Interviewers often ask about choices made in the project ("why did you make the choices you made?") — [CodePath](https://codepath.org/news/how-to-have-side-projects-that-stand-out-and-why)
- Chrome Web Store: most reviews finish "within a few days, but it can take up to a few weeks." Contact support if an item is pending more than 3 weeks. New developers or extensions, dangerous permissions, broad host permissions, and significant code changes all trigger closer review — [Chrome docs: Review process](https://developer.chrome.com/docs/webstore/review-process)
- April 2026 PSA from the CWS team: review times rose because of a surge in submissions, affecting new items and updates. Broken privacy policy URLs are a common rejection reason — [chromium-extensions group](https://groups.google.com/a/chromium.org/g/chromium-extensions/c/VJ6DcpEn51Y)
- Aug 20, 2026 CWS blog: reviews were brought back to "expected baselines" (no numbers given). New pre-submission install testing runs on draft upload. Publishers get a default of two extension slots (existing published extensions are grandfathered). The rating system now weights recent reviews more heavily — [Chrome blog](https://developer.chrome.com/blog/cws-review-updates-2026)
- Developer reports from 2025–2026 describe updates stuck "pending review" for days, in one case 11+ days. A dashboard option lets you cancel a pending review and resubmit — [chromium-extensions threads](https://groups.google.com/a/chromium.org/g/chromium-extensions/c/tJfyKrk2rdg), [cancel review blog](https://developer.chrome.com/blog/chrome-webstore-cancel-review?hl=hi)

### Inferences
- Because ratings now weight recent reviews, shipping user-requested features (and replying to the requesters) is a cheap way to keep the 5-star average current.
- Ship about every 2–3 weeks during Cycles A and B. Ship backend-related extension changes in one or two releases so review delays and permission prompts happen once.
- Use a separate unlisted or dev build, or local unpacked loading, for backend iteration, so production users aren't exposed to half-built sync.

### Gaps
- No quantitative data on current median CWS review times (Google publishes none). Evidence is the docs ("a few days") plus forum anecdotes.

## Is sync + accounts the most valuable "hard problem"? What sync/local-first experts say

### Takeaway
General sync is genuinely hard (Ink & Switch say ad-hoc sync tends to be "unreliable and brittle"). But this app's data is a near-ideal case for a simple, server-authoritative design: per-device, per-day, per-site counters that only one device writes. Keying rows by (user, device, date, site) with idempotent upserts avoids conflicts entirely, and the dashboard sums across devices. CRDTs are overkill. The interesting, demonstrable problem is really "correct, idempotent, offline-tolerant upload of locally-first data," plus tracking accuracy. Accounts (Google sign-in) are mostly plumbing and integration time.

### Cited Findings
- Ink & Switch, "Local-first software" (Kleppmann, Wiggins, van Hardenberg, McGranaghan, April 2019; Onward! 2019): seven ideals (no spinners, multi-device, network optional, seamless collaboration, long now, security/privacy, user ownership). Apps that hand-write their own diff/merge sync often end up "unreliable and brittle." CRDTs are a promising foundation but have open issues (networking, history growth, schema migration) — [Ink & Switch](https://www.inkandswitch.com/essay/local-first/)
- The same essay says conflicts arise only when users "concurrently modify the same property of the same object" — [Ink & Switch](https://www.inkandswitch.com/essay/local-first/)
- Paul Butler (Jamsocket, Dec 2022), "You might not need a CRDT": with a central server, simpler authoritative-server approaches often suffice (full text was not retrievable this session) — [Jamsocket](https://jamsocket.xyz/blog/you-might-not-need-a-crdt). A similar argument comes from Ably/Zak Knill: most collaborative apps don't need CRDTs — [Ably](https://ably.com/blog/you-dont-need-crdts-for-collaborative-experiences), [zknill.io](https://zknill.io/posts/collaboration-no-crdts/)
- Last-write-wins fits independent scalar fields (settings, titles) but is wrong for concurrent prose edits, where it can silently drop changes — [Reading CRDTs for Mortals, dimfeld](https://www.dev.to/dimfeld/reading-the-crdts-for-mortals-example-code-2pb), [DEV local-first solo apps](https://dev.to/raxxostudios/local-first-architecture-for-solo-apps-when-crdts-help-and-when-they-hurt-4pj0)
- Notion reportedly uses server-decided last-write-wins rather than a CRDT for text (HN comment, secondhand) — [Brian Lovin HN mirror](https://brianlovin.com/hn/38289327)
- PowerSync case study: Cinapse moved away from CRDTs to simpler server-authoritative sync — [PowerSync blog](https://powersync.com/blog/why-cinapse-moved-away-from-crdts-for-sync)
- Redis: the alternative to coordination is reconciling later, usually with LWW. CRDT counters exist for distributed increments — [Redis](https://redis.io/en/blog/how-crdts-power-active-active-database-replication/)

### Inferences
- Recommended data design: each device owns its rows. `UPSERT (user_id, device_id, date, site) SET seconds = GREATEST(existing, incoming)` (or a plain overwrite with the device's absolute total) is idempotent, so retries and offline catch-up are safe. Cross-device totals are a `SUM` over devices. This is effectively a grow-only, per-replica counter (G-Counter-like) without a CRDT library, and it makes a strong interview talking point ("why I didn't need a CRDT").
- Settings and custom-site lists are the only truly shared mutable state. Per-field LWW with `updated_at` is enough.
- A more impressive, cheaper alternative or complement: tracking accuracy under MV3 (service worker suspension, idle/locked screen, multiple windows, tab focus), with automated tests. It is core to user trust and needs no server. This is inference. I did not research MV3 timing specifics in this pass.
- A strong scoped version that demonstrates the core hard problem: local-first history (already planned) + idempotent batch upload + a read-only dashboard. Defer real-time sync and two-way settings sync.

### Gaps
- Could not retrieve Jamsocket's full text to quote its specific recommendations.
- Did not find expert sources specifically on sync of time-tracking or analytics counters. The G-Counter analogy is inference.

## Time to a first Node+Postgres API with auth deployed; common time sinks

### Takeaway
No reliable published benchmark exists for how long beginners take. Curricula (Odin) treat "Express + Postgres + auth + PaaS deploy" as one mid-size project. The predictable time sinks for this project are Google OAuth in an extension (extension ID/client ID matching, redirect URIs, consent screen), deployment and environment config, and Chrome Web Store review plus permission-warning re-approval, which can disable the extension for existing users.

### Cited Findings
- `chrome.identity.getAuthToken` is for Google accounts and takes its client ID and scopes from the manifest's `oauth2` section. If the registered app ID doesn't match the extension's ID, getAuthToken errors. To keep a stable ID during development, copy the `key` into the source manifest — [Chrome docs: User Authentication](https://developer.chrome.com/docs/apps/app_identity), [identity API](https://developer.chrome.com/docs/extensions/reference/api/identity)
- `launchWebAuthFlow` (for non-Google providers or a custom flow) needs the redirect URI `https://<extension-id>.chromiumapp.org/...` registered with the provider — [identity API](https://developer.chrome.com/docs/extensions/reference/api/identity)
- Don't request tokens interactively on startup, or users get context-free sign-in prompts. Tokens are cached in memory, so non-interactive calls are fine — [Chrome docs](https://developer.chrome.com/docs/apps/app_identity)
- Permission warnings: if an update adds a permission that triggers a new warning, "the extension will be disabled until the user accepts the new permission." Chrome recommends requesting permissions at runtime (optional permissions) and `activeTab`, which shows no warning — [Chrome docs: Permission warnings](https://developer.chrome.com/docs/extensions/develop/concepts/permission-warnings)
- Broad host permissions (`<all_urls>`, `https://*/*`) and significant code changes trigger extra review scrutiny — [CWS review process](https://developer.chrome.com/docs/webstore/review-process)
- Odin Project's Members Only project bundles Postgres setup, auth, and deploying to a PaaS. No hour estimate was found — [TOP](https://www.theodinproject.com/lessons/node-path-nodejs-members-only)

### Inferences
- Budget rules of thumb (inference, not sourced):
  - First deployed "hello JSON from Postgres" API: about 8–15 hrs for a first-timer.
  - Google sign-in end to end (extension + backend token verification + dashboard login): about 10–20 hrs, much of it console and config debugging.
  - Each CWS submission: plan for days, possibly 1–2 weeks.
  - At 8 hrs/week, the auth plus first deploy alone could take a month.
- Adding the `identity` permission or new host permissions for the API domain may trigger a warning and disable the extension for all 79 users until they re-accept. Mitigations: declare the API host and `identity` as optional permissions, requested at runtime when the user opts into sync, and put sync behind an opt-in so local-only users are unaffected. Verify against the Permissions reference which exact permissions warn; this pass did not confirm `identity` specifically.
- Update the privacy policy before submitting the sync release. Data now leaves the device, and broken or outdated privacy policies are a common rejection reason.

### Gaps
- No credible dataset on beginner time-to-deploy for Node+Postgres+auth was found. The estimates above are inference.
- Did not confirm in this pass whether the `identity` permission itself triggers an install warning. Check the Chrome Permissions reference/warning list.
- Hosting free-tier changes in 2025–2026 (Render, Railway, Fly, Neon, Supabase) were not researched here and are a known deployment time sink.
