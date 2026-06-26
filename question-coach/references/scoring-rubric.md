# Scoring Rubric — classifying a manager's questions

Used by the `question-coach` skill when grading a transcript. Keep judgments consistent week to week
so the trend line means something.

## OPEN — counts for you
Forces a real, multi-word answer; invites narration; doesn't telegraph a preferred answer.
- *What happened when the deploy went out?*
- *Walk me through how you decided that.*
- *What's the part of this you're least sure about?*
- *Tell me about the pushback you got.*

## CLOSED — counts against you
Answerable in one word, or a yes/no that ends the thread.
- *Is it going okay?*  → "yeah"
- *Did you finish the migration?*  → "yes"
- *Are you blocked?*  → "no" (and you learn nothing)
Openers that usually signal closed: **did / do / is / are / can / could / should / would / have you / didn't you / right?**

## STATEMENT-AS-QUESTION — counts against you (the sneaky one)
An opinion or instruction wearing a question mark. Leads the witness; the report just agrees.
- *Don't you think we should just roll it back?*  (you already decided)
- *Have you considered doing it the other way?*  (that's advice)
- *Wouldn't it be cleaner to split the service?*  (your design, not their thinking)

## Borderline calls
Judge by the **answer it actually produced** in the transcript. A technically-open question that
got a one-word answer because it was vague still failed its job — note it. An open question on a
trivial topic doesn't earn full credit toward "surfaced something new."

## Phase-2 thread-follow scoring
For each meaningful thing the report said that invited a dig:
- **followed** — next manager question references that specific thing and goes deeper.
- **dropped** — manager returned to agenda / changed topic / accepted the thin answer.
Thread-follow rate = followed ÷ (followed + dropped). The costliest **dropped** is the teaching moment.

## The outcome test (the real scoreboard)
Did the manager end the conversation knowing something they didn't walk in knowing — a blocker, a
disagreement, a risk, a feeling, a fact? If not, **the open ratio is flattering them.** Say so.
