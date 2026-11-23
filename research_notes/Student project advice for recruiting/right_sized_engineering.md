# Right-Sized Engineering Rigor for a Solo Student Project with Real Users

Context: Chrome extension (~79 users) adding a TypeScript/Node/Postgres backend with Google sign-in, cross-device sync and a dashboard. Research date: Nov 2026. Several sources are classic essays (2015-2022) and are flagged with dates; the 2024-2026 material is mostly practitioner blogs and forum posts, which are opinion, not data.

## Over-engineering: microservices, Kubernetes, queues, Redis, GraphQL, multiple environments, elaborate CI/CD, monorepos

### Takeaway
Respected engineers broadly agree: one deployable app (a monolith), one Postgres database, and managed hosting is the right default for a solo project. Microservices, Kubernetes, separate queues or caches, and multi-environment pipelines solve coordination and scale problems a one-person app with 79 users does not have. Adopting them early is a well-known anti-pattern ("resume-driven development") unless the stated goal is learning that specific tool.

### Cited Findings
- **Choose Boring Technology (Dan McKinley, 2015, classic).** Each organization has a small supply of "innovation tokens" (about three early on). Spend them on the product, not on new databases or paradigms. "Boring" means "well understood," with known failure modes. Key line: "Adding the technology is easy, living with it is hard." Advice: "Pick the smallest set of tech that covers our problem domain." — [boringtechnology.club](https://boringtechnology.club/)
- McKinley also argues that polyglot persistence (each team picking its own datastore) creates operational burden and loses the benefits of a shared platform. His example: on a shared stack, a feature's usage grew 20x with little special attention. — [boringtechnology.club](https://boringtechnology.club/)
- **The Majestic Monolith (DHH, Feb 29, 2016, classic).** Microservices are "a wonderful way to parallelize" work across thousands of developers at Amazon or Google scale. For small teams, copying them is cargo culting. Distribution brings failure states, outage handling, coordinated migrations and knowledge silos, so avoid it unless forced. Basecamp served web, iOS, Android, Mac, Windows and email from one monolith built by about 12 programmers. In a May 2019 comment he said nothing had changed his reasoning. — [Signal v. Noise](https://signalvnoise.com/svn3/the-majestic-monolith/)
- **YAGNI (Martin Fowler, May 26, 2015, classic).** Presumptive features carry four costs: build, delay, carry (extra complexity slows every other change) and repair (built wrong before you understood the need). Fowler is explicit that YAGNI does not excuse skipping refactoring, self-testing code or continuous delivery. Those practices are what make it safe to defer design. — [martinfowler.com](https://martinfowler.com/bliki/Yagni.html)
- **In defense of simple architectures (Dan Luu, about 2022).** Computers are fast enough that most apps, even high-traffic ones, can run on simple architectures. Wave, a $1.7B mobile-money company with about 70 engineers, ran a Python monolith over Postgres and spent its "complexity budget" only where it was unavoidable (telecom and SMS integrations). — [danluu.com](https://danluu.com/simple-architectures/); [InfoQ summary](https://www.infoq.com/news/2022/05/wave-low-architecture-complexity/); [Changelog](https://changelog.com/news/lbg2)
- **Pieter Levels (levelsio).** He runs multiple profitable solo products on a deliberately primitive stack. His Nomads.com FAQ says it uses jQuery on the front end, PHP plus SQLite on the back end and a single Ubuntu/NGINX VPS, with no frameworks beyond jQuery. Revenue and server-cost figures in secondary sources conflict and are unverified. — [Nomads.com FAQ](https://nomads.com/faq/what-is-the-tech-stack-behind-nomadscom-6610937); [levels.io: how I build my MVPs](https://levels.io/how-i-build-my-minimum-viable-products)
- **"Just use Postgres" (2024-2026).** This is a popular argument that Postgres covers queues (`SELECT ... FOR UPDATE SKIP LOCKED`), caching (UNLOGGED tables), search and JSON documents, so Redis, Kafka or RabbitMQ are unnecessary early. Pushback: Redis data structures (sorted sets, streams) are real advantages, and one former advocate moved to "still mostly using Postgres" as their team grew. The consensus is to add Redis or Elasticsearch only after measuring a real bottleneck. — [Stephan Schmidt, AmazingCTO, updated Dec 2025](https://www.amazingcto.com/postgres-for-everything/); [Tiger Data, "It's 2026, Just Use Postgres"](https://www.tigerdata.com/blog/its-2026-just-use-postgres); [Xata, "Is Postgres really enough in 2026?"](https://xata.io/blog/is-postgres-really-enough-in-2026); [collectiveidea, Aug 2024](https://collectiveidea.com/blog/archives/2024/08/22/just-use-postgres/)
- **Kubernetes for solo developers (2025-2026 practitioner posts).** Kubernetes is called heavily over-engineered for low-traffic apps (under about 1,000 requests a day, one or two services). Use one server or Docker Compose, or a PaaS, and consider k3s only when zero-downtime deploys and real traffic demand it. Caveat from commenters: if the explicit goal is learning Kubernetes, doing it is fine. — [DEV: Kubernetes for solo developers](https://dev.to/whoffagents/kubernetes-for-solo-developers-when-its-worth-it-and-when-its-not-2mj2); [DEV: Kubernetes for solo devs in 2026](https://dev.to/ottoaria/kubernetes-for-solo-developers-in-2026-do-you-actually-need-it-3ak1)
- **Microservices regret.** Robin Wieruch reports that microservices became too hard to reason about as a solo developer and that he went back to a monolith. — [robinwieruch.de](https://robinwieruch.de/microservices-tradeoffs)
- **Over-engineering as procrastination.** Indie posts describe spending weeks on Kubernetes or event-driven architecture for projects with no users, calling it "procrastination that feels like progress." — [DEV: Stop over-engineering your indie project](https://dev.to/ntty/stop-over-engineering-your-indie-project-3j0h); [DEV: The overengineering trap](https://dev.to/ruhidibadli/the-overengineering-trap-youre-building-a-spaceship-when-you-need-a-bicycle-292m)
- **Simple monolith plus Postgres on HN (2024-2025, via mirrors).** Commenters describe running everything on one Postgres instance with vertical scaling, skipping Redis, Kubernetes and serverless. They add that high availability eventually needs a second server or a hot standby. — [HN item 41382687 (mirror)](https://web-tau-bice-50.vercel.app/item/41382687); [HN item 45832803 (mirror)](https://frontpage-app.vercel.app/news/45832803)

### Inferences
- For this project, a red-flag list (over-engineering at about 79 users): microservices; Kubernetes or Helm; Kafka, RabbitMQ or a separate queue service; Redis for caching; GraphQL when there is one first-party client; staging plus QA plus prod environments; multi-stage CI with deploy gates; Terraform for one app; a monorepo tool like Nx or Turborepo when there are only two packages (extension and server). A simple two-folder repo with shared types, or npm/pnpm workspaces, is enough.
- What the sources endorse instead: one TypeScript/Node service (REST/JSON is fine), one Postgres database, a managed host, and adding complexity only in response to a measured problem.
- Interviewers likely read the right-sized choice, plus a written explanation of why (for example "considered Redis; Postgres handles our load"), as a stronger signal than the complex stack. Engineers who quote McKinley and DHH reward judgment. This is inference, not a sourced hiring claim.
- Fowler's YAGNI caveat matters: deferring infrastructure is not the same as skipping tests and refactoring. The "don't over-engineer" advice is often misused to justify sloppiness.

### Gaps
- No primary 2024-2026 essay from DHH, McKinley or Fowler specifically about solo developers was found. Their classic essays are the backbone and are aimed at small teams.
- No authoritative source specifically on GraphQL or monorepos for solo projects was found. The inferences above are extrapolated from the general principles.
- A specific high-quality 2025 HN thread could not be located directly. Only mirror sites of HN items were found, and their dates are unconfirmed.

## Testing for solo projects

### Takeaway
Write a modest number of tests aimed at the risky logic: sync conflict resolution, auth and token verification, per-user data isolation, and migrations. Lean toward integration tests against a real Postgres over heavily mocked unit tests, and rely on TypeScript and a linter as the cheap base layer. A minimal CI run on push (typecheck, lint, test) is cheap and worth it, even for one person. Large end-to-end suites usually are not worth it at this stage.

### Cited Findings
- **Testing Trophy (Kent C. Dodds; post dated June 3, 2021).** From bottom to top the layers are static analysis, unit, integration and E2E, with most emphasis on integration. The guiding phrase, attributed to Guillermo Rauch: "Write tests. Not too many. Mostly integration." Weigh each test by the confidence it gives against the time it costs. — [kentcdodds.com](https://kentcdodds.com/blog/the-testing-trophy-and-testing-classifications)
- **On the Diverse and Fantastical Shapes of Testing (Martin Fowler, June 2, 2021).** The pyramid-versus-trophy debate is largely about definitions: Dodds's "integration tests" resemble what Fowler calls "sociable unit tests." Arguing about test percentages is "a distraction." What matters are tests that run quickly and reliably and fail only for useful reasons (quoting Justin Searls). — [martinfowler.com](https://martinfowler.com/articles/2021-test-shapes.html)
- **Kent Beck: "Make it run, make it right, make it fast."** Beck credits the phrase to his father, Douglas Beck. It is a sequencing discipline, and a related chapter appears in his *Tidy First?* work (book March 2024, Substack chapter Sep 2024, paywalled and not read). — [kentbeck.com](https://kentbeck.com/); [Tidy First? Substack](https://tidyfirst.substack.com/p/chapter-make-it-run-make-it-right); [heise review](https://heise.de/-9777074)
- **Fowler: self-testing code and continuous delivery are what make YAGNI safe**, so testing is not on the list of things to defer. — [martinfowler.com/bliki/Yagni](https://martinfowler.com/bliki/Yagni.html)
- **Indie developer disagreement:**
  - Skeptics say most tests aren't worth writing when you're small and can become a form of procrastination. Extensive E2E and integration tests need too much upfront work before anyone pays. — [Indie Hackers: Do you write tests?](https://www.indiehackers.com/post/solopreneurs-do-you-write-tests-541acb2c89); [Indie Hackers: Don't write tests for your MVP](https://www.indiehackers.com/post/dont-write-tests-for-your-mvp-7d9da5ee98)
  - Supporters say tests on the "more nuanced parts" stop you from breaking things, especially when you return to code infrequently. — [Indie Hackers: Testing on solo projects](https://www.indiehackers.com/post/testing-on-solo-developer-projects-how-effcbdaf59)
  - The middle ground is "just unit and a few integration tests" for side projects. — [Indie Hackers: CI as a solo developer](https://www.indiehackers.com/post/continuous-integration-as-a-solo-developer-80f533394c)
- **CI for one person.** Start with a first pipeline that only runs lint and tests, and add it "when the project can boot," not when it feels finished. CI guards against the person most likely to bypass your process, which is you, late at night. Over-complex CI/CD is a cost trap for indie developers. — [DEV: Add CI when the project can boot](https://dev.to/oranguengineer/add-ci-when-the-project-can-boot-not-when-it-feels-finished-20m9); [DEV: CI/CD over-complexity for indie hackers](https://dev.to/merbayerp/cicd-strategies-the-cost-of-over-complexity-for-indie-hackers-3kj3); [Getting value from CI (Dec 2024)](https://www.chiark.greenend.org.uk/~ryounger/2024/12/getting-value-from-ci/)
- **Simon Willison's "Perfect Commit" (Oct 29, 2022).** Each commit bundles implementation, tests, docs and an issue link, and keeps main deployable. This is a respected solo-maintainer practice: he maintains many open-source projects largely alone. — [simonwillison.net](https://simonwillison.net/2022/Oct/29/the-perfect-commit/)

### Inferences
- Concrete test plan for this project:
  - Integration tests for API routes against a real test Postgres (Docker or a Neon branch), covering auth required, user A cannot read user B's data, and sync merge and conflict behavior.
  - Unit tests for pure logic, such as merge and diff functions and extension storage migration.
  - One smoke test that the server boots and the migrations apply.
  - Skip broad Playwright E2E of the extension and dashboard for now. At most, add one happy-path E2E test later.
- CI on push with GitHub Actions running `tsc --noEmit`, lint and tests is roughly a 20-line YAML file. It is worth it, and it doubles as visible evidence of discipline to reviewers.
- Coverage targets (for example "90% coverage") are theater at this scale. Per Fowler, the useful measure is reliable tests on the risky code.

### Gaps
- No 2024-2026 essay from Dodds, Fowler or Beck specifically about solo projects was found. Beck's 2024 chapter is paywalled.
- No data (versus opinion) on defect rates of solo projects with and without tests was found.

## Process for one person: PRs to yourself, design docs, ADRs, changelogs, semver

### Takeaway
Keep the lightweight artifacts that help future-you and reviewers: issues as a working notebook, a short decision log, a CHANGELOG tied to releases, and a README. Skip process theater: self-approved PR ceremonies, formal design-doc templates, an ADR for every choice. PRs to yourself are useful only as a way to trigger CI and write a description. They are not review.

### Cited Findings
- **Issues as a notebook (Simon Willison, 2022).** Willison treats issue threads as a working notebook (background, decisions, screenshots, prototypes) and notes that most of his issue threads are him talking to himself. He prefers issues over long commit messages because they are discoverable, can embed media and can be updated. — [simonwillison.net](https://simonwillison.net/2022/Oct/29/the-perfect-commit/)
- **ADRs.** Typically one page of markdown kept in the repo; MADR is the common template. — [Martin Fowler, ADR bliki](https://www.martinfowler.com/bliki/ArchitectureDecisionRecord.html); [GitHub blog: Why write ADRs (2020)](https://github.blog/2020-08-13-why-write-adrs)
- **ADRs for solo work.**
  - One solo developer who wrote 74 ADRs in 70 days found the payoff mainly psychological: the record "hands you its reasons" so you can pick work back up. He also warns against documenting instead of shipping. — [DEV: 74 ADRs in 70 days](https://dev.to/michelfaure/what-74-adrs-in-70-days-actually-buy-a-solo-dev-no-hire-no-clients-just-the-file-13nn)
  - Counterpoint: ADRs trade usability for auditability, which is the wrong tradeoff for solo or small teams. Curate the log rather than only appending to it. — [DEV: Your decision log is an archaeological site](https://dev.to/gregsmethells/your-decision-log-is-an-archaeological-site-41bk)
  - A selection rule: record a decision if someone without context might break something or waste days re-deriving it. — [SDA](https://sda.company/blog/category/other/architecture-decision-records/)
- **Planning and documentation as hiring signal.** Gergely Orosz (Pragmatic Engineer) suggests juniors build side projects so they have "code in production to show at job interviews." In his educational side-project post he suggests borrowing ideas like planning first, documenting steps and a "production simulation." — [Pragmatic Engineer: An educational side project](https://blog.pragmaticengineer.com/an-educational-side-project/)
- **Changelogs.** The Keep a Changelog convention says changelogs are written for humans and grouped by Added, Changed, Fixed and so on. — [keepachangelog.com](https://keepachangelog.com/) (not fetched in this session; well-known convention)

### Inferences
- Useful for this project:
  - A `docs/decisions.md` with 5-10 short entries (why Postgres, why this auth approach, why this host, sync conflict strategy).
  - A CHANGELOG matching Chrome Web Store versions. Users exist and the store requires incrementing versions, so release notes have a real audience.
  - Simple semver-ish extension versions.
  - Branches plus PRs only to run CI and leave a written trail.
  - One short design note for the sync model, since that is the genuinely tricky part.
- Theater for one person: required approvals, PR templates with checklists, sprint boards, formal RFCs, semver policies for an API with exactly one consumer you control, and conventional-commit enforcement tooling.
- For recruiting, a decision log is the cheapest way to make judgment legible. This builds on Orosz's point that talent is illegible to people making hiring decisions. — [Orosz: The illegible nature of software development talent](https://www.goodreads.com/author_blog_posts/26142196-the-illegible-nature-of-software-development-talent?tab=book)

### Gaps
- No respected-engineer source directly addressing "PRs to yourself" was found. The recommendation above is inference.
- No authoritative source on semver specifically for browser extensions was fetched.

## Production practices worth doing for a small real app

### Takeaway
For a real app with real users' data, the non-negotiables are:
- Correct auth (verify Google ID tokens server-side with a library; key users by `sub`).
- Secrets in environment variables, never committed.
- Versioned schema migrations.
- Automated backups you have actually test-restored.
- Error tracking (for example a Sentry free tier) and basic structured logging.
- Basic rate limiting on auth and write endpoints.

Uptime dashboards, distributed tracing, multi-region setups and SLOs are overkill.

### Cited Findings
- **Google ID token verification (official docs).**
  - Never accept a plain user ID from the client.
  - Verify the signature against Google's public keys. Check that `aud` matches your client ID, that `iss` is `accounts.google.com` or `https://accounts.google.com`, and that `exp` has not passed.
  - Use an official library (Node.js has one) rather than custom code. The tokeninfo endpoint is for debugging only.
  - Use `sub`, not email, as the unique user key, because email "can be changed by the user."

  — [Google Identity: Authenticate with a backend server](https://developers.google.com/identity/sign-in/web/backend-auth)
- **Chrome extension auth.** `chrome.identity.getAuthToken` works for users signed into Chrome with a Google account. `launchWebAuthFlow` opens a provider pop-up and captures a redirect to `https://<extension-id>.chromiumapp.org/...`. — [Chrome Identity API reference](https://developer.chrome.com/docs/extensions/reference/identity/); [Chrome user authentication docs](https://developer.chrome.com/docs/apps/app_identity)
- **Roll-your-own sessions (Lucia, 2025).** Lucia deprecated its auth library in March 2025 and turned it into a learning resource that teaches you to implement sessions yourself. The maintainer's view was that it's better to teach the concepts than to cram them into a library. This legitimizes hand-written session handling built on vetted primitives, with OAuth and OIDC verification still done through libraries. — [lucia-auth.com](https://lucia-auth.com); [GitHub: lucia-auth/lucia](https://github.com/lucia-auth/lucia)
- **Error tracking and backups (2025-2026 solo-developer checklists).**
  - Error tracking is the top priority, and Sentry's free tier is enough early on.
  - Uptime checks miss failures where the server still returns 200s.
  - Test-restore backups before adding monitoring ("monitoring untested backups is just theater").
  - Prefer managed Postgres with point-in-time recovery.
  - Verify the error tracker is actually connected before launch.

  — [DEV: Solo production setup (Vercel, Neon, Sentry)](https://dev.to/whoffagents/solo-developer-production-setup-vercel-neon-sentry-and-zero-devops-gjb); [Production hardening checklist your solo SaaS skips](https://javascript.plainenglish.io/the-production-hardening-checklist-your-solo-saas-skips-until-its-too-late-2173c1ce0add); [DEV: Launch-day checklist](https://dev.to/ahmet_saridag_9232a4f1a24/a-launch-day-checklist-for-developers-that-doesnt-assume-everything-goes-smoothly-2d9b)
- **Boring choice of database.** Choose "the most boring technology that solves your problem," for example Postgres over niche options. — [DEV: Solo production setup](https://dev.to/whoffagents/solo-developer-production-setup-vercel-neon-sentry-and-zero-devops-gjb); see also [McKinley](https://boringtechnology.club/)

### Inferences
- Worth doing now:
  1. Server-side Google ID token verification with `google-auth-library`, a `users` table keyed on `sub`, and short-lived sessions or JWTs with secure cookies or bearer tokens.
  2. Authorization checks scoped by `user_id` on every query, plus a test for that.
  3. Migrations through a standard tool (for example node-pg-migrate, Drizzle or Prisma migrate) checked into the repo.
  4. `.env` files plus host-managed secrets, with `.env` gitignored.
  5. The managed host's automated backups, restore-tested once.
  6. Sentry or a similar error tracker on the server, and ideally on the extension too.
  7. Simple per-IP or per-user rate limiting middleware on auth and sync endpoints.
  8. CORS locked to the extension origin and the dashboard domain.
  9. A privacy policy that matches the data actually synced. Chrome Web Store user-data policies apply. The repo already has one.
- One staging environment is optional. A Neon branch or a local Docker Postgres usually substitutes for it at this scale.

### Gaps
- No authoritative source (for example OWASP) on rate limiting or migration tooling was fetched in this session. Those recommendations are standard practice but uncited here.
- Specific Chrome Web Store user-data policy requirements for sync backends were not researched (out of scope).

## Managed services vs self-hosting: auth, Postgres, deploy; learning vs shipping

### Takeaway
For a solo student, managed Postgres (Neon or Supabase) plus a simple PaaS (Render, Railway or Fly) or Vercel for the dashboard is the fastest path. Self-hosting on a VPS is a legitimate, cheaper "boring" option à la Levels, but it adds backup and patching duties. Watch the free-tier gotchas: Supabase pauses inactive free projects, Render free web services sleep after 15 minutes, and Neon free compute scales to zero. For real users, a few dollars a month to avoid cold starts is usually worth it. On learning versus shipping, practitioners say learning a tool is a valid goal, but say so explicitly; otherwise optimize for shipping.

### Cited Findings
- **Supabase.** Free-plan projects pause after low activity over a week, and paid plans never pause for inactivity. The restore window is reported inconsistently (90 days in one doc version, up to 1 year elsewhere), so verify on the current page. — [Supabase: Project pausing](https://supabase.com/docs/guides/platform/free-project-pausing); [Supabase KB](https://supabase.com/kb/faqs/platform/free-project-pausing)
- **Render.** Free web services spin down after 15 minutes of inactivity, which can add up to about 30 seconds of delay on the next request. Render staff discourage cron "keep-alive" pings and recommend paid instances. — [Render community: free tier sleep](https://community.render.com/t/do-web-services-on-a-free-tier-go-to-sleep-after-some-time-inactive/3303); [Render community: free tier queries](https://community.render.com/t/free-tier-queries/6555)
- **Neon.** Free-plan compute scales to zero after 5 minutes of inactivity, and this can't be disabled on the free tier. Neon says it reactivates in a few hundred milliseconds, far faster than a PaaS cold start. — [Neon: Scale to zero](https://neon.tech/docs/introduction/scale-to-zero); [Neon plans](https://neon.com/docs/introduction/plans)
- **Levels-style self-hosting.** A single VPS with NGINX can run real revenue-generating products. — [Nomads.com FAQ](https://nomads.com/faq/what-is-the-tech-stack-behind-nomadscom-6610937)
- **Zero-DevOps solo stack (2025-2026).** Practitioner posts recommend Vercel plus Neon plus Sentry as a near-zero-ops solo setup. — [DEV: Solo developer production setup](https://dev.to/whoffagents/solo-developer-production-setup-vercel-neon-sentry-and-zero-devops-gjb); [DEV: My SaaS infrastructure as a solo founder](https://dev.to/shayy/my-saas-infrastructure-as-a-solo-founder-2ghl)
- **Learning vs shipping.** Commenters distinguish resume-driven from product-driven projects: if the goal is strictly learning Kubernetes, go for it. — [Hashnode thread: your hobby project does not need to scale to millions of users yet](https://hashnode.com/forums/thread/your-hobby-project-does-not-need-to-scale-to-millions-of-users-yet)
- **Production experience as a hiring signal.** Orosz frames side projects' value as having "code in production to show at job interviews." — [Pragmatic Engineer](https://blog.pragmaticengineer.com/an-educational-side-project/)
- **Auth options.** Lucia's deprecation pushes TypeScript developers toward either a hand-written session layer (following Lucia's guide) or a managed provider (Supabase Auth, Clerk and others). — [lucia-auth.com](https://lucia-auth.com); [supastarter on Lucia's future](https://supastarter.dev/blog/lucia-auth-future)

### Inferences
- A suggested stack for this project, consistent with the sources:
  - Neon (or Supabase) Postgres; Neon's fast wake suits low traffic.
  - The Node API on Render, Railway or Fly. Pay for an always-on tier, because the extension's sync calls would otherwise hit 30-second cold starts.
  - The dashboard on Vercel or served by the same Node app.
  - Google sign-in via `chrome.identity`, plus server-side ID-token verification and your own small session table. This is a good learning-versus-shipping balance: you understand the auth flow without running an identity provider.
- Supabase Auth or Clerk would ship faster but hide the parts interviewers ask about. Hand-rolled OAuth or JWT signing is where students make security mistakes. The middle path (library-verified Google tokens plus your own sessions) teaches the most while staying on vetted primitives.
- If the goal includes learning DevOps, one VPS with Docker Compose, Caddy or NGINX, and scheduled `pg_dump` to object storage is the "boring" self-host path. Kubernetes is not.

### Gaps
- Current exact pricing for Render, Railway and Fly paid tiers was not verified in this session. A $7/month Render Starter figure appears in secondary sources only.
- No rigorous comparison of managed auth providers (Clerk, Supabase Auth, Auth.js/Better Auth) for Chrome-extension flows was found.
