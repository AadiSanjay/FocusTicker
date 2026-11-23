# FocusTicker v1 history

Condensed from the ChatGPT handoff (Sep–Oct 2026) and checked against the
code on 2026-11-23. Where the handoff and the code disagree, **the code wins**,
and the difference is noted.

## Identity
- Store item ID: `pghicmhngfmldcnoglcodkbaiaknjlah`
- Store: https://chromewebstore.google.com/detail/focusticker/pghicmhngfmldcnoglcodkbaiaknjlah
- Repo: https://github.com/AadiSanjay/ChromeExt4SocialMedia
- Published version: `1.0.0`, last updated Oct 5, 2026 (confirmed on the
  store listing, 2026-11-23). 80 users, 5.0★ from 7 ratings.
- Similar extensions shown next to it on the store: StayFocusd (a blocker),
  Web Timer, Site Timer, Visual Timer. FocusTicker's difference is a timer on
  the page that never blocks.

## How v1 got built (short timeline)
1. Session tracking in `background.js`: detect the active tracked site, start
   a session, checkpoint it when you leave.
2. The session moved from an in-memory variable into `storage.session`,
   because the MV3 service worker can be killed at any time.
3. A 1-minute alarm checkpoint was added. Splitting `sessionStartTime`
   ("Now" began) from `lastCheckpointTime` (saved up to here) fixed "Now"
   resetting every minute.
4. `refreshQueue` was added after finding that `tabs.onActivated` and
   `windows.onFocusChanged` fire nearly together and both read the same old
   session.
5. The content script went from one `GET_USAGE` on load to polling every
   second. The background stays the single source of truth.
6. The overlay design iterated: top-right pill → corner snapping (dropped) →
   free drag with exact saved coordinates, a separate details panel, keyboard
   moves, and reduced motion.
7. Store submission, with two rejections (see below). Live by Oct 2026.
8. LinkedIn launch: ~7.5k impressions, 75 reactions, 29 comments, 92 link
   clicks.

## Bugs found and fixed in v1 (good interview material)
| Bug | Cause | Fix |
|---|---|---|
| Session lost when the worker slept | Session lived only in memory | `storage.session` |
| Checkpoint read the *new* session | `checkpointSession()` not awaited | `await` before creating the new session |
| Double-counted or overwritten time | Two events read and wrote at once | `refreshQueue` |
| "Now" reset every minute | One timestamp used for two meanings | Split `sessionStartTime` / `lastCheckpointTime` |
| `NaN` times | `lastCheckPointTime` vs `lastCheckpointTime` typos | Consistent names |
| "Now" reset on same-site navigation | `onUpdated` recreated the session | Keep the session if the domain is unchanged |
| Time charged to the old site | Early `return` on invalid URL left a stale session | Clear the session |
| Bad state on focus loss | `WINDOW_ID_NONE` (-1) treated as a tab | Handle it explicitly |
| `youtube.com/shorts` didn't match | A path treated as a hostname | Match on the hostname only |
| Focus tests looked flaky | DevTools changes window focus | Test with ordinary windows |

## Store review lessons (still apply)
- **Keyword spam ("Yellow Argon"):** listing site brand names in the
  description got rejected. Say "popular social, video, and content
  platforms" instead. **This applies to the listing rewrite and to the custom
  sites feature.**
- **Privacy policy ("Purple Nickel"):** a GitHub `blob` URL was rejected as
  unavailable. The fix was a GitHub Pages URL.
- Metadata-only changes don't need a version bump. Package changes do. Zip
  with `manifest.json` at the root.

## Where the handoff and the code disagree
- **x.com:** the handoff says x.com support was discussed. The code has **no
  `x.com` anywhere**, so the planned cross-file audit never happened. (Cycle 3)
- **Default position:** the handoff says we moved away from the top-right
  default. The code still starts at `top: 64px; right: 12px` until the user
  drags it.
- **Details-panel side:** the handoff describes a center-of-screen test. The
  code compares the space on the left and right of the timer
  (`updateDetailsSide`).
- **Hostname normalization:** the handoff says lowercase plus strip `www.`.
  The code does neither explicitly. It relies on `URL` lowercasing hostnames
  and on `endsWith("." + domain)`, which covers `www.`. The result is the
  same.
- **"YouTube layout shift":** no layout-shift bug is on record, only the
  overlay colliding with the YouTube header.

## Privacy policy link: ⚠️ check now (2026-11-23)
- `aadisanjay.github.io/ChromeExt4SocialMedia/privacy.html` returns **404**.
  `privacy.html` **does exist** on GitHub (added Oct 2, 2026 from the
  website, with a Limited Use section). The site root also 404s, so GitHub
  Pages most likely isn't turned on for the repo.
- The old `blob/main/extension/PRIVACY.md` and `blob/main/Hello World/PRIVACY.md`
  links also return **404**, because the Oct 1 commits moved the file.
- Only `blob/main/PRIVACY.md` loads, and that's the URL style the store
  rejected.
- **Confirmed:** the store listing links to the `github.io/.../privacy.html`
  URL, which returns 404.
- **Fix:** turn on GitHub Pages (Settings → Pages → `main` / root). The file
  is already there. No store resubmission is needed, because the URL doesn't
  change.
- Lesson: my local clone was behind GitHub. Run `git pull` before starting
  work.

## Data disclosures look wrong (found 2026-11-23)
The listing says FocusTicker handles **"Personally identifiable information"**
and **"Authentication information"**. v1 handles neither: no names, no
emails, no passwords, no tokens. That's inaccurate, and it probably scares
off people deciding whether to install. Re-check the boxes in the dashboard's
Privacy tab against Google's definitions. v3 (Google sign-in) will change the
answer, so revisit then.

## Who wrote what (honest reconstruction)
- **background.js: collaborative.** Aadi wrote and iterated the core flow.
  ChatGPT introduced `storage.session` persistence, the checkpoint
  semantics, `refreshQueue`, the `await` fix, and the midnight-reset
  restructure.
- **content.js: mostly ChatGPT-written.** Aadi set the product requirements.
  The drag, pointer capture, coordinate persistence, clamping, details panel,
  keyboard moves, and reduced motion were generated and then integrated.
- **Consequence:** resume bullets 2–3 (event-driven tracking, Promise queue,
  Shadow DOM) describe parts I didn't fully write. Before interviews I must be
  able to explain and re-derive them myself (Cycle 0 explain-back).
- The git history is thin: 12 commits before the docs, with v1's code arriving
  in bulk. From now on, small commits are the authorship record.

## Ideas parked from v1
- A session grace period, so brief interruptions don't restart "Now"
- User-selectable display modes
- The old ChatGPT V2/V3 plan (FastAPI, SQLite, JWT and password hashing,
  Docker, AWS App Runner + RDS). **Replaced** by the current plan: TypeScript,
  Postgres, Google sign-in (no passwords), managed hosting. See DECISIONS.md.
