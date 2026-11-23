# Progress

Full plan, cycles, and cut list: [ROADMAP.md](ROADMAP.md).

## Current cycle
**Cycle 0 (resume now)** and **Cycle 1 (attention timer → v1.1)**, from
2026-11-22 to about mid-December.

## Done
- 2026-11-22: First session. Read through the extension's architecture and
  listed the sync hazards below. Created the docs.
- 2026-11-22: **A1 audit done.** The "~3s engagement" number is time on the
  Chrome Web Store listing page, not extension use. The extension has no
  analytics code or network calls.
- 2026-11-22: Researched how strong engineers recommend building student
  projects (`reports/Student project advice for recruiting.md`). Re-planned
  to a fixed budget of about 170h, ending mid-May 2027, as cycles with a cut
  list.

## Next step
1. **Cycle 0:** add FocusTicker to the resume, with the link and the real
   store numbers, and check which first-year programs are still open.
2. **Cycle 1:** write the spec for the attention timer: color thresholds,
   pulse interval, and soft-limit behavior. Then Claude proposes the design
   and the Chrome APIs before any code.

## Known sync hazards (from the first read-through)
Each is tagged with the cycle that handles it.
1. Usage is wiped at midnight, not archived. (Cycle 2)
2. Time since the last checkpoint goes to the checkpoint's date, so up to
   ~1 minute before midnight lands on the next day. (Cycle 2)
3. Totals are fractional seconds, so the server needs a rounding rule. (Cycle 4)
4. The date is the device's local date, so time zones can disagree. (Cycle 4)
5. There's no device ID. (Cycle 4)
6. All storage writes must go through `refreshQueue`, sync included. (Cycle 4)
7. The tracked-site list lives in three places. (Cycle 3)
8. x.com isn't tracked. Fixing it needs a spec. (Cycle 3)
9. New permissions can disable the extension for existing users. Check before
   every release. (Cycles 3 and 5)
10. Existing `usage` data must be migrated on update. (Cycle 2)
