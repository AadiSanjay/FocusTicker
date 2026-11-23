# Learning log

Concepts in my own words, plus checkpoints.

For each topic, three checks:
- **Explain:** can I explain it out loud without notes?
- **Errors:** can I read its error messages and guess the cause?
- **Write:** can I write similar code without help?

Three yeses mean similar work can move to spec-and-review mode. Any no keeps
it in tutor mode.

| Topic | Explain | Errors | Write | Mode now |
|---|---|---|---|---|
| Extension architecture (my own code) | | | | n/a |
| v1: `refreshQueue` and race conditions | | | | tutor |
| v1: `storage.session` + checkpoint split | | | | tutor |
| v1: message passing (`return true`, polling) | | | | tutor |
| v1: Shadow DOM + drag/pointer capture | | | | tutor |
| HTTP: GET vs. POST, status codes, JSON | | | | tutor |
| SQL: SELECT / WHERE / ORDER BY | | | | tutor |
| SQL: INSERT / UPDATE / DELETE | | | | tutor |
| SQL: JOIN | | | | tutor |
| SQL: GROUP BY and aggregates | | | | tutor |

---

## Phase 0 checkpoint questions
Answer these in your own words below once you've done the reading.

**HTTP**
1. What's the difference between GET and POST? Which one should be safe to
   repeat, and why does that matter for a flaky network?
2. What do 200, 201, 400, 401, 404, and 500 mean? Which ones are "my fault"
   (the client's) and which are "the server's fault"?
3. What is JSON? Write the JSON for one FocusTicker usage record.
4. What's a header? Name one header you saw in a curl response.

**SQL**
5. Write a query: every row from a table, filtered and sorted.
6. Write an INSERT, then an UPDATE that changes that row. How do you make sure
   the UPDATE doesn't touch every row?
7. Write a JOIN between two tables. In one sentence, what does the JOIN do?
8. What does GROUP BY do? When would FocusTicker need it?

---

## My notes
_(Your words go here. Date each entry.)_

### Extension architecture
- Why does background.js checkpoint every minute instead of adding time only
  when I leave a site?
  -
