# AI Coding Tools and Learning: How Students Should Build Projects to Learn and Get Hired (2024–2026)

## Vibe coding vs learning: what respected engineers and educators say

### Takeaway
Nearly every respected voice draws the same line: "vibe coding" (not reading the code) is fine for throwaway prototypes, but professional, career-building work is "agentic engineering," "vibe engineering" or "augmented coding," where you own, read and can explain every line. The coiner of "vibe coding" himself hand-wrote his serious 2025 project. Educators like CS50 go further for beginners and ban general AI tools for coursework, allowing only a guardrailed tutor.

### Cited Findings
- **Karpathy, origin (Feb 2, 2025; one outlet says Feb 3):** He coined "vibe coding" as fully giving in to the vibes and "forget that the code even exists," and said in the same post it is "not too bad for throwaway weekend projects." He also admitted that when the LLM can't fix a bug he works around it or asks for random changes. — [Know Your Meme summary](https://knowyourmeme.com/memes/vibe-coding); [Simon Willison tag page](https://simonwillison.net/tags/andrejkarpathy); date conflict noted by [OfficeChai](https://officechai.com/ai/vibe-coding-is-now-everywhere-but-andrej-karpathy-had-coined-the-term-exactly-a-year-ago)
- **Karpathy, nanochat (Oct 2025):** He said his roughly 8,000-line nanochat repo was "basically entirely hand-written" with tab autocomplete. He tried Claude and Codex agents, but they were "net unhelpful," possibly because the repo is too far off the training-data distribution. Commentators read this as a narrow point: agents are weaker on unusual, dense, hard-to-test code. — [Analytics India Mag](https://analyticsindiamag.com/ai-news-updates/andrej-karpathy-says-nanochat-is-entirely-hand-written-not-vibe-coded/); [Gizmodo](https://gizmodo.com/even-the-inventor-of-vibe-coding-says-vibe-coding-cant-cut-it-2000672821); [Slashdot](https://developers.slashdot.org/story/25/10/19/0022237/openai-cofounder-builds-new-open-source-llm-nanochat---and-doesnt-use-vibe-coding)
- **Karpathy, "agentic engineering" (early 2026, exact date unverified):** He proposed "agentic engineering" as the name for professional AI-assisted work, distinct from vibe coding. In the quoted framing, vibe coding raises the floor, while agentic engineering keeps the professional quality bar. — [The New Stack](https://thenewstack.io/vibe-coding-is-passe-karpathy-has-a-new-name-for-the-future-of-software/); [Business Insider via AOL](https://www.aol.com/articles/guy-coined-vibe-coding-says-181826669.html). Several Buttondown write-ups on this look AI-generated and are not used here.
- **Simon Willison (Mar 19, 2025), "Not all AI-assisted programming is vibe coding":** He says the term should not be stretched to cover all LLM-assisted coding. His personal rule is that he won't commit code he couldn't explain exactly to someone else. — [simonwillison.net](https://simonwillison.net/2025/Mar/19/vibe-coding/)
- **Willison (Oct 7, 2025), "Vibe engineering":** His term for seasoned professionals who use LLMs while staying accountable for the result. Practices that make agents effective: automated tests (test-first is "particularly effective with agents"), planning before handing work to the agent, documentation, git discipline, CI/linting, a code-review culture, manual QA, research skills, judgment about what to delegate, and updated estimation. His key line is that AI tools "amplify existing expertise." An update says "Agentic Engineering" is becoming the more popular term. — [simonwillison.net](https://simonwillison.net/2025/Oct/7/vibe-engineering/)
- **Willison (May 6, 2026):** He says the line between vibe coding and agentic engineering has started to blur for him, but still defines vibe coding as not looking at the code at all. — [simonwillison.net](https://simonwillison.net/2026/May/6/vibe-coding-and-agentic-engineering)
- **Addy Osmani (Dec 4, 2024), "The 70% problem":** AI gets you about 70% of the way fast, and the last 30% needs engineering judgment. His "knowledge paradox" is that AI helps seniors more than juniors. Seniors use it to speed up work they already understand. Juniors use it to learn what to do, so they accept outdated or incorrect solutions, miss security and performance issues, struggle to debug generated code, and build fragile systems. His advice: start with small, well-defined tasks, review every line, stay modular, learn concepts alongside AI use, and treat AI as a learning tool rather than a code generator. (The 70% is a heuristic, not a measurement.) — [Addy Osmani Substack](https://addyo.substack.com/p/the-70-problem-hard-truths-about); also [Pragmatic Engineer guest post](https://newsletter.pragmaticengineer.com/p/how-ai-will-change-software-engineering)
- **Osmani (later):** He defines agentic engineering as AI doing the implementation while the human owns architecture, quality and correctness. In a Nov 2025 talk he stressed that if your name is on submitted code, you are responsible for it. He later revisited the 70% framing as an "80% problem" for agentic tools. — [addyosmani.com/blog/agentic-engineering](https://addyosmani.com/blog/agentic-engineering/); [The 80% Problem](https://addyosmani.com/blog/the-80-problem-in-agentic-coding/)
- **Kent Beck (mid-2025), "Augmented Coding: Beyond the Vibes":** In vibe coding you care only about system behavior and feed errors back "into the genie." In augmented coding you care about the code, its complexity, its tests and their coverage, with the same values as hand coding: "tidy code that works." He built a production-grade B+ tree library in Python and Rust this way, enforcing TDD and catching the AI when it tried to cheat, for example by disabling tests. He has called AI an endlessly patient tutor. — [Kent Beck newsletter](https://newsletter.kentbeck.com/p/augmented-coding-beyond-the-vibes); [kentbeck.com summary](https://www.kentbeck.com/summaries/augmented-coding-beyond-the-vibes/)
- **Harvard CS50 policy (current):** Across CS50 courses it is academically dishonest to use AI tools other than CS50's own (ChatGPT, Claude, Copilot, Gemini and others) that suggest or complete answers or lines of code, unless a course explicitly allows it. CS50's own Duck (cs50.ai, cs50.dev) is allowed. — [CS50 AI academic honesty](https://cs50.harvard.edu/ai/honesty/); [CS50 R honesty](https://cs50.harvard.edu/r/honesty/)
- **CS50's Duck design (Harvard Gazette, Sep 25, 2026):** Malan calls the Duck a deliberately "less-helpful version" of ChatGPT that asks guiding questions. It uses two guardrail layers: prompts, plus code that screens responses before students see them. A "heart" system rate-limits questions because some students asked about 200. The Duck still emitted code up to a quarter of the time despite instructions not to. Malan warns students to be skeptical of output and acknowledges the worry that LLMs remove productive struggle. — [Harvard Gazette](https://news.harvard.edu/gazette/story/2026/09/taming-the-duck-for-starters/)
- **CS50 final projects:** One lecture transcript says the course encourages ChatGPT-style tools only once students reach their final projects. This may reflect an older policy. — [Coconote transcript (secondary)](https://coconote.app/notes/9f213e2b-55e3-4bc6-bfb6-c145548cd111/transcript)

### Inferences
- The consensus standard for a portfolio project is Willison's rule: commit nothing you can't explain. "I vibe-coded it" is an acceptable answer only for a throwaway prototype, never for the flagship project on a resume.
- CS50's model of guardrails during learning and freer tools for the capstone suggests a staged path. Learn fundamentals with AI as a Socratic tutor, then build portfolio projects with agents under engineering discipline (tests, review, plans).
- Disagreement or tension: Karpathy now sees vibe coding as passé for professionals yet still values it for prototypes, while educators like CS50 restrict AI for novices. These are different audiences, not a real contradiction. Willison and Beck are enthusiastic about agents. Osmani is more cautious about juniors.

### Gaps
- I did not retrieve Gergely Orosz's own opinion essays on students and AI beyond his interviewing surveys (much of it is paywalled).
- I did not find other universities' formal AI policies (Stanford, CMU, Berkeley) in this pass.

## Evidence that AI assistance reduces learning, and usage patterns that preserve it

### Takeaway
Multiple randomized studies from 2024–2026 show that unguarded AI use speeds up practice but lowers later unaided performance and comprehension. The gap is largest on debugging. How students use AI matters more than whether they use it. Asking conceptual or "explain this" questions, and resolving errors yourself, preserves learning. Delegating code, or using AI as a debugger, destroys it.

### Cited Findings
- **Anthropic RCT (Jan 29, 2026; Shen & Tamkin, arXiv:2601.20245):** 52 mostly junior engineers learned the unfamiliar Python async library Trio. The AI group scored 50% on a follow-up quiz vs 67% for hand-coders (Cohen's d = 0.738, p = 0.01), with the largest gap on debugging questions. Speed gain was about 2 minutes and not significant (p = 0.391). — [Anthropic research](https://www.anthropic.com/research/AI-assistance-coding-skills); [arXiv](https://www.arxiv.org/pdf/2601.20245)
- **Anthropic interaction patterns (association, not causation; small n):**
  - Low scorers, below 40%: "AI delegation" (39%), "progressive AI reliance," where they started with questions and then delegated everything (35%), and "iterative AI debugging," using AI to debug or verify rather than understand (24%, and slowest at about 31 minutes).
  - High scorers, 65% or more: "generation-then-comprehension," generating code and then asking follow-up questions (86%), "hybrid code-explanation," requesting code together with explanations (68%), and "conceptual inquiry," asking only conceptual questions and fixing errors independently (65%).
  - Recommendation: novices should accept cognitive effort and use AI for comprehension, for example through learning modes. Caveats: short-term quiz, and agentic tools like Claude Code may have stronger effects.
  - [Anthropic research](https://www.anthropic.com/research/AI-assistance-coding-skills); coverage by [InfoQ](https://www.infoq.com/news/2026/02/ai-coding-skill-formation)
- **Bastani et al., PNAS 2025, "Generative AI without guardrails can harm learning":** Nearly 1,000 Turkish high-school math students. An unrestricted GPT-4 chat ("GPT Base") improved practice performance by 48%, but later unaided exam scores fell 17% below control. A tutor with guardrails ("GPT Tutor," giving hints, not answers) improved practice by 127% and showed no exam harm, though no gain either. Logs showed most GPT Base students simply asked for answers, so the tool worked as a "crutch." — [Wharton Knowledge](https://knowledge.wharton.upenn.edu/article/without-guardrails-generative-ai-can-harm-education/); [SSRN](https://papers.ssrn.com/abstract=4895486); [IDEAS/PNAS record](https://ideas.repec.org/a/nas/journl/v122y2025pe2422633122.html)
- **Prather et al., ICER 2024, "The Widening Gap" (n=31 novice programmers):** All previously known metacognitive difficulties persisted and could be compounded by GenAI. New difficulties appeared, which the authors call "Progression," "Interruption" and "Mislead." Strong students accelerated, while struggling students who used it fell further behind and often had an illusion of competence. The authors recommend explicitly teaching problem-solving process and scaffolding. — [arXiv 2405.17739](https://arxiv.org/abs/2405.17739); [ICER 2024](https://icer2024.acm.org/details/icer-2024-papers/26/The-Widening-Gap-The-Benefits-and-Harms-of-Generative-AI-for-Novice-Programmers)
- **MIT Media Lab, "Your Brain on ChatGPT" (preprint, June 2025, not peer-reviewed; n=54, only 18 in session 4):** In essay writing, the LLM group showed the weakest EEG brain connectivity, the lowest sense of ownership, and trouble quoting their own work. The brain-only group showed the strongest connectivity. A secondary report says starting unaided and then adding AI looked better than starting with AI; this is unverified in the paper. — [MIT Media Lab](https://www.media.mit.edu/publications/your-brain-on-chatgpt/)
- **METR RCT (July 2025):** 16 experienced open-source developers on 246 real tasks in their own repos were 19% slower with AI (mainly Cursor with Claude 3.5/3.7 Sonnet). They forecast a 24% speedup and afterward still believed they had been 20% faster. METR calls this a point-in-time result specific to that setting. — [METR](https://metr.org/blog/2025-07-10-early-2025-ai-experienced-os-dev-study/); [The Register](https://www.theregister.com/2025/07/11/ai_code_tools_slow_down/)
- **Developer trust (Stack Overflow 2025 survey, July 29, 2025; 49k+ respondents):** 84% use or plan to use AI tools. 46% distrust the accuracy of AI output, up from 31%. Only about 29–33% trust it; Stack Overflow's own figures vary by page. — [Stack Overflow blog](https://stackoverflow.blog/2025/07/29/developers-remain-willing-but-reluctant-to-use-ai-the-2025-developer-survey-results-are-here); [Stack Overflow press](https://stackoverflow.co/company/press/archive/stack-overflow-2025-developer-survey/)

### Inferences
- For a student, the most damaging habit is pasting errors into AI until they go away. It was the lowest-scoring pattern in Anthropic's study, matches Karpathy's own description of vibe coding, and destroys exactly the debugging skill interviewers probe.
- The patterns that preserve learning are concrete and teachable:
  - Ask "why" and "how does this work" questions.
  - After generating code, interrogate it before moving on.
  - Ask for an explanation alongside any code.
  - Fix your own bugs.
  - Use a hints-only or "learning mode" tutor while learning new material.
- The guarded tutor in the PNAS study prevented harm but did not beat no-AI on exams. The case for AI-as-tutor is "no harm plus convenience," not proven better learning. Treat that as an open question.
- METR's perception gap suggests students should not trust their own sense of being faster or learning more with AI. Use tests, quizzes or "re-implement without AI" checks.

### Gaps
- No long-term (semester- or year-long) RCT on agentic tools (Claude Code, Cursor agent mode) for CS students was found. Anthropic notes that agentic tools may have larger effects.
- Small samples throughout (Anthropic n=52, Prather n=31, METR n=16, MIT n=54). Effect sizes should be presented as suggestive.
- I did not retrieve the Microsoft/CMU 2025 critical-thinking survey (CHI 2025) in this pass.

## How interviewers probe projects and detect AI-generated work the candidate doesn't understand

### Takeaway
Interviewers have shifted from "does it work" to "do you understand it." They ask why, ask granular follow-ups, re-ask questions, use rapid-fire questions, ask candidates to critique or debug code they didn't write, and increasingly bring back onsite rounds. Candidates should expect to explain any line, justify design tradeoffs, and debug live, with or without AI.

### Cited Findings
- **Pragmatic Engineer, Pulse #146 (Sep 18, 2025; interviewing.io survey of 63 interviewers):**
  - 81% of Big Tech and New Big Tech interviewers suspected AI cheating, and 31% had caught someone definitely doing it.
  - 58% of Big Tech interviewers adjusted questions: more open-ended prompts, LeetCode variants, longer setups, and more problem-solving than coding (Google).
  - Detection tactics: asking "why" and demanding detailed explanations, more granular follow-ups, re-asking a question later (AI answers are non-deterministic), and rapid-fire questions that leave no time to prompt.
  - Meta requires full-screen sharing and asks interviewers to flag suspected cheating.
  - Interviewers at Apple, Microsoft and Google expect in-person interviews to return.
  - None of the 53 Big Tech respondents said their company had dropped algorithmic questions.
  - [Pragmatic Engineer](https://newsletter.pragmaticengineer.com/p/the-pulse-146)
- **Google onsite rounds:** A Pragmatic Engineer podcast says Google restarted onsite coding interviews because that is the only way to be sure candidates aren't using AI cheating tools (secondhand claim). — [Pragmatic Engineer, Reality of Tech Interviews / podcast](https://newsletter.pragmaticengineer.com/p/the-reality-of-tech-interviews?r=1eba5a)
- **Cheating consequences:** Orosz reports a scaleup that fired an engineer after two weeks for AI-cheating in a remote interview, and an experiment showing cheating raised pass rates while going undetected. — [Pragmatic Engineer: Tech hiring inflection point](https://newsletter.pragmaticengineer.com/p/tech-hiring-is-this-an-inflection); [How GenAI is reshaping tech hiring](https://newsletter.pragmaticengineer.com/p/how-genai-changes-tech-hiring)
- **Code-audit exercises:** Some teams give candidates AI-generated code to critique, a different skill from writing it. — [Built In](https://builtin.com/articles/audit-interview-scorecard)
- **Portfolio "paper trail":** A finished, polished project alone now says little about the builder, so hiring managers look for evidence of the process. — [The New Stack, "How AI changes developer portfolios"](https://thenewstack.io/how-ai-changes-developer-portfolios/) (fetch blocked; claim from search summary)
- **Anecdote:** A widely shared LinkedIn post describes a fresh graduate with a clean, working portfolio who couldn't explain one part of his own code when asked. This is an anecdote, not data. — [LinkedIn post (via search)](https://bd.linkedin.com/in/avijit-gh)
- **Canva (June 2025):** In AI-allowed interviews, a critical skill is the ability to "read, understand, and improve" AI code, and engineers must fully own any code they produce. — [Canva engineering blog](https://canva.dev/blog/engineering/yes-you-can-use-ai-in-our-interviews)

### Inferences
- Practical interview bar for a student's flagship project:
  - Explain any file or function on demand.
  - Say why you chose this database, framework or data model over alternatives.
  - Describe a real bug you hit and how you found it.
  - Extend or modify a feature live.
  - Say what you would do differently.
- The re-asking and rapid-fire tactics mean memorizing AI-written explanations of your own project won't hold up. Only genuine understanding survives follow-ups.
- Because Big Tech still uses algorithmic rounds (often without AI) while startups use AI-allowed practical rounds, students need both. Be able to code unaided, and be able to drive AI well.

### Gaps
- No systematic data was found specifically on how interviewers probe resume side projects, as opposed to live coding. Evidence is mostly anecdote plus surveys about live interviews.
- Full paywalled Pragmatic Engineer deep dives were not read.

## Do employers want AI-fluent students, and how should a student show it?

### Takeaway
Yes, increasingly. Canva, Meta (pilot) and Shopify treat AI fluency as an expected skill, and Canva says candidates with little AI experience do worse even when they can code. Policies are split, though: Anthropic bans AI in its own live interviews and take-homes unless told otherwise. Fluency means judgment (decomposing work, verifying and fixing AI output, owning results), not just prompting.

### Cited Findings
- **Canva (June 11, 2025):** AI tools such as Copilot, Cursor and Claude are expected in technical interviews for backend, frontend and ML roles. A pilot "AI-Assisted Coding" round replaced the CS Fundamentals screen, with harder, more ambiguous problems that one prompt can't solve.
  - Evaluated: when and how to use AI, breaking down ambiguous requirements, sound decisions, catching and fixing problems in AI code, production standards, and fundamentals.
  - Strong candidates ask clarifying questions, use AI for well-defined subtasks while keeping control of the whole solution, critically review output, and debug when AI fails.
  - Weak candidates lack AI experience, can't steer it, or can't tell when suggestions are suboptimal.
  - [Canva engineering blog](https://canva.dev/blog/engineering/yes-you-can-use-ai-in-our-interviews); [The Register](https://www.theregister.com/2025/06/11/canva_coding_assistant_job_interviews/)
- **Meta (mid/late 2025):** Piloted "AI-enabled coding" interviews with an AI assistant built into the environment, reportedly in a multi-file codebase. Scope is disputed: invite-only pilot vs broader rollout. — [TechRadar](https://www.techradar.com/pro/meta-is-going-to-let-candidates-use-ai-in-job-interviews); [interviewing.io guide](https://interviewing.io/blog/how-to-use-ai-in-meta-s-ai-assisted-coding-interview-with-real-prompts-and-examples)
- **Shopify (memo leaked April 7, 2025):** Tobi Lütke called "reflexive AI usage" a baseline expectation. AI usage questions were added to performance and peer reviews, and teams must show AI can't do a task before asking for headcount. Startups including Shopify use interviews where candidates use AI while sharing their screen. Forrester argued the memo should have said "judicious," not "reflexive." — [Shopify AI usage page](https://www.shopify.com/careers/candidate-guide/ai-usage); [Tom's Hardware](https://www.tomshardware.com/tech-industry/artificial-intelligence/shopify-ceo-teams-must-prove-ai-cant-do-a-task-before-asking-for-new-hires-resources); [Forrester](https://www.forrester.com/blogs/what-you-can-learn-from-shopifys-ceos-memo-on-workforce-ai/); [Pragmatic Engineer Pulse #146](https://newsletter.pragmaticengineer.com/p/the-pulse-146)
- **Anthropic (revised July 2025):** Candidates may use Claude for research, preparation and refining materials, and should write first drafts themselves. Live interviews are "all you," with no AI unless indicated. Take-homes are also without Claude unless indicated. This reversed a blanket ban from May 2025. — [Anthropic candidate AI guidance](https://www.anthropic.com/candidate-ai-guidance); [Fortune](https://fortune.com/2025/07/21/billion-dollar-giant-anthropic-ai-ban-hiring-policy-change-job-seekers-interview-process/)
- **Adoption:** 84% of developers use or plan to use AI tools (Stack Overflow 2025), and Malan cites a LinearB survey finding almost 90% use AI in some form. — [Stack Overflow](https://stackoverflow.blog/2025/07/29/developers-remain-willing-but-reluctant-to-use-ai-the-2025-developer-survey-results-are-here); [Harvard Gazette](https://news.harvard.edu/gazette/story/2026/09/taming-the-duck-for-starters/)

### Inferences
- How a student should show fluency in a project writeup or README:
  - Include an "AI usage" section saying which tools were used for what. For example: scaffolding and tests by agent; core algorithm, data model and concurrency by hand. Also say what was rejected or fixed.
  - Show the engineering scaffolding Willison and Beck say makes agents work: tests and CI, a planning or design doc, small reviewed commits, and lint/format.
  - Write a "bugs AI got wrong and how I caught them" note. This shows the review and debugging judgment Canva grades.
  - A clean git history with meaningful commits is the "paper trail."
- Students should prepare for both regimes: AI-required (Canva, Shopify, Meta pilot) and AI-banned (Anthropic live rounds, Google onsites). That means practicing unaided coding and AI-driven coding.

### Gaps
- No employer survey quantifying how much AI fluency weighs in new-grad hiring decisions was found.
- No primary employer guidance specifically on how to present AI use in a portfolio; the README advice above is inferred.

## Practical workflows that preserve learning

### Takeaway
The best-supported workflow is staged. Learn a concept without AI or with a hints-only tutor. Build the core logic yourself. Then use AI for boilerplate, repeats, tests and exploration, and always interrogate generated code until you could rewrite it. Tests, plans and review keep agent-built code yours.

### Cited Findings
- **Hints-only tutor:** Guardrailed tutors (CS50 Duck, PNAS "GPT Tutor") avoid the learning harm of answer-giving chatbots. — [Harvard Gazette](https://news.harvard.edu/gazette/story/2026/09/taming-the-duck-for-starters/); [Wharton Knowledge](https://knowledge.wharton.upenn.edu/article/without-guardrails-generative-ai-can-harm-education/)
- **Generate then interrogate:** "Generation-then-comprehension" (86%) and "conceptual inquiry" (65%) were the highest-scoring patterns; Anthropic recommends learning modes for novices. — [Anthropic](https://www.anthropic.com/research/AI-assistance-coding-skills)
- **Small, reviewed tasks:** Start with isolated, well-defined tasks, review every line, and keep the code modular. — [Osmani](https://addyo.substack.com/p/the-70-problem-hard-truths-about)
- **TDD with agents:** Use test-driven development with agents and watch for the AI disabling or gaming tests. — [Kent Beck](https://newsletter.kentbeck.com/p/augmented-coding-beyond-the-vibes); [Willison](https://simonwillison.net/2025/Oct/7/vibe-engineering/)
- **Plan first:** Write a plan before delegating, and judge what to outsource. — [Willison](https://simonwillison.net/2025/Oct/7/vibe-engineering/)
- **Write it yourself first:** Anthropic tells candidates to write first drafts themselves before using Claude to refine them. — [Anthropic candidate guidance](https://www.anthropic.com/candidate-ai-guidance)
- **Hand-write novel, hard code:** Karpathy hand-wrote nanochat because agents failed on novel, dense code. — [Analytics India Mag](https://analyticsindiamag.com/ai-news-updates/andrej-karpathy-says-nanochat-is-entirely-hand-written-not-vibe-coded/)
- **Explainability as the commit bar:** Willison won't commit code he couldn't explain. — [Willison](https://simonwillison.net/2025/Mar/19/vibe-coding/)

### Inferences
- An opinionated student recipe:
  1. Write the first version of each new concept by hand, for example your first REST endpoint, first SQL schema, or first async code. Then let AI do the 2nd through Nth repetitions.
  2. Never paste an error into AI before forming your own hypothesis. Ask "what does this error mean," not "fix this."
  3. After any AI-generated chunk, ask the AI to explain it, then close the chat and explain it out loud yourself (a rubber-duck test).
  4. Keep the novel or core part of the project (the thing an interviewer will ask about) mostly hand-written.
  5. Use agents for boilerplate, config, UI scaffolding, test generation and refactors, under tests and git.
  6. Before interviews, re-implement one key module without AI.
- Disagreement: some argue (Hacker News commenters on Karpathy) that if the results are useful, the process doesn't matter. That may hold for shipping products, but the learning research and interview practices above suggest it does not hold for students trying to build and demonstrate skill.

### Gaps
- No primary source was found for the exact phrasing "write by hand first, then let AI do repeats" as a named workflow from a prominent engineer. It is an inference supported by the Anthropic patterns, the MIT order effect (secondary, unverified) and Karpathy's practice.
- No controlled study compares workflows such as boilerplate-only AI vs tutor-only AI for project-based learning.
