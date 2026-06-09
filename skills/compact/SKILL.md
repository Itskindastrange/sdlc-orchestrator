---
name: compact
description: >
  Trigger this skill immediately and without hesitation whenever the user types the word "COMPACT"
  (case-insensitive) anywhere in their message. When triggered, summarize the entire conversation
  into a structured, copy-paste-ready briefing for a new chat session. Do NOT ask clarifying
  questions — just produce the summary. Also trigger if the user says things like "compact this",
  "run compact", or "give me a compact summary".
---

# COMPACT Skill

## Purpose
Produce a dense, copy-paste-ready conversation summary that lets a new Claude session pick up
exactly where this one left off — with zero loss of critical context.

---

## Output Format

### Header (always first)
```
## 📋 Continuing from previous session
```
Then one line of plain-English context: what the conversation was about and what stage it reached.

Example:
> **Session:** Building a Python ETL pipeline with idempotent load patterns. Reached a working
> generator-based UPSERT solution; discussing chunked batch commits next.

---

### Bullet Points (5–7 total)

Each bullet must be dense and self-contained — written so that a *new* Claude instance with zero
prior context can understand it without follow-up questions.

**Bullet rules:**
- Start each bullet with a bold **[Topic]** label, e.g. **[Goal]**, **[Decision]**, **[Problem]**,
  **[Code]**, **[Context]**, **[Next Step]**, **[Constraint]**
- Write in present tense ("The pipeline uses…", not "We decided to use…")
- Short inline code uses backticks: `upsert_record()`
- Longer code (3+ lines) goes in a fenced block directly *below* the bullet it belongs to,
  labeled with the language

**Prioritize equally across:**
1. **Decisions & outcomes** — what was chosen and why; rejected alternatives
2. **Code & technical details** — key functions, patterns, schemas, commands
3. **Open questions & next steps** — what was unresolved or planned next

---

### Footer (always last)
End with a single line:
```
> ⚡ Paste this block at the start of a new chat to resume instantly.
```

---

## Example Output

````
## 📋 Continuing from previous session
**Session:** Exploring Python generator patterns for an ETL pipeline. Reached working
idempotent UPSERT solution; open question on chunked batch commit strategy.

- **[Goal]** Build a production ETL pipeline in Python that loads data idempotently — re-runs must not create duplicates; target DB is PostgreSQL.

- **[Decision]** Using generators for memory efficiency over loading full dataset into a list. Tradeoff accepted: generators are single-use, so retry logic must checkpoint progress, not restart the whole stream.

- **[Code]** Core UPSERT pattern agreed on:
  ```python
  def upsert_record(conn, record):
      conn.execute("""
          INSERT INTO events (id, payload, updated_at)
          VALUES (:id, :payload, NOW())
          ON CONFLICT (id) DO UPDATE SET payload = EXCLUDED.payload
      """, record)
  ```

- **[Problem]** Long-running generator + single transaction causes lock contention; solution is chunked commits every N records using `itertools.islice()`.

- **[Context]** User is familiar with Python, generators, and SQL; prefers code-first explanations over theory.

- **[Next Step]** Implement and test the chunked batch commit wrapper; evaluate whether a checkpointing table is worth adding for large backfills.

> ⚡ Paste this block at the start of a new chat to resume instantly.
````

---

## Execution Steps

1. **Read the full conversation** — scan from top to bottom, including any code blocks, decisions reversed, and corrections made.
2. **Identify the top 5–7 moments** that a new session *must* know: the goal, key decisions (including rejected alternatives), critical code, blockers, and next steps.
3. **Draft bullets** — each one dense, labeled, and self-contained.
4. **Handle code**: inline for short snippets (`like_this()`), fenced block for anything 3+ lines.
5. **Write header + footer**, then assemble the full output inside a single markdown code block so the user can copy it in one click.
6. **Do not add commentary** after the block — the output speaks for itself.

---

## Edge Cases

| Situation | How to handle |
|---|---|
| Very short conversation (<5 meaningful exchanges) | Use 3–4 bullets instead of forcing 7; quality over count |
| Conversation has lots of code | Code bullets can have blocks; still cap at 7 total bullets |
| Multiple unrelated topics in one chat | Add a **[Topic Switch]** bullet to flag the shift |
| User typed "compact" mid-sentence (e.g. "compact cars are great") | Do NOT trigger — only trigger when "compact" is clearly a command, not a word in a sentence |
