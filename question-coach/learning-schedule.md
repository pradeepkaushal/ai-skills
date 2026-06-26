# Question Coach — 12-Week Learning Schedule

A deliberate-practice program to make your questions sharper, anchored to the conversations
already on your calendar. This file is the **spec** — every threshold, drill, and gate is pinned
here. The `question-coach` skill (same directory) is the **engine** that runs it weekly.

---

## 1. The decisions this plan is built on

These were settled during design. Don't silently drift from them — if one stops fitting, change it
here on purpose.

| Decision | Choice | Why |
|---|---|---|
| **Spine** | Eliciting truth in the **manager 1:1** | The one skill that transfers across manager / engineer / founder. Customer-discovery is shelved (0 calls/week today). |
| **Rep surface** | 4 one-on-ones + 2 technical/design discussions per week = **6 live reps** | Already on the calendar. No new meetings. |
| **Engine** | **70% live reps / 30% manufactured drills** | You learn by reviewing real conversations; drills only rehearse a specific move. |
| **Review depth** | **Deep on 1–2 "lab" reps, light tally on the rest** | One transcript you actually study beats six you skim. |
| **Targets (in order)** | Phase 1: **open questions** → Phase 2: **follow the thread** | Closed questions are the *cause*; dropped threads are the *symptom*. Fix the cause first. |
| **Capture** | Record + transcript for lab reps; **5-minute memory dump** as universal fallback | No feedback loop = no learning. Capture is non-negotiable. |
| **Measurement** | Process metric (open ratio) + **outcome metric (learned something new)** | Form without outcome is cargo-cult. Outcome is the real scoreboard. |
| **Honesty check** | Skill audits a pasted transcript (regular) + ask a report once/month | Self-scored 1:1s inflate. Needs an ego-free check. |
| **Horizon** | **12 weeks**, criteria-gated advancement, Week-5 method-check | Finite block you finish > open-ended program you abandon. |

---

## 2. The two targets

### Phase 1 — Open over closed (the cause)

The reflex to build: replace yes/no openers with ones that force a real answer.

- **Kill these openers:** *did / do / is / are / can / should / would / have you / didn't you*
- **Reach for these:** *what / how / walk me through / tell me about / what made you / what's the part that…*
- **The tell of a closed question:** your report can answer it in one word and the thread dies.

### Phase 2 — Follow the thread (the symptom)

The elite move, and the harder one. When a report says something live, you chase *it* instead of
returning to your pre-scripted next question.

- **The move:** echo their last meaningful word, then dig — *"You said the deploy 'felt rushed' — what was rushed about it?"*
- **The test:** of the important things they said, how many did you actually follow vs let drop?
- **The obstacle you committed to beating:** when the live thread isn't on your agenda, **drop the agenda and chase it.** This is the whole skill; finishing your list is the failure.

---

## 3. The weekly loop (~3 hrs of 4-hr budget — deliberately under-packed)

Your 6 meetings happen anyway; the budget is **prep + review + drills**, not the conversations.

| Block | Time | What you do |
|---|---|---|
| **Pre-lab prep** | 15 min | Pick the week's **lab 1:1**. Write 3 open questions in advance. Set one goal for the conversation. |
| **The lab rep** | 0 extra | The 1:1 happens. **Record it** (or 5-min dump right after). |
| **Deep review** | 60 min | Read the transcript. Count open vs closed. Find your **single worst closed question** and rewrite it open. (Phase 2: find **one dropped thread** and write the follow-up you should've asked.) |
| **Drills (the 30%)** | 60 min | Closed→open rewrite reps / live role-play. Run via the `question-coach` skill. |
| **Light tally** | ~5 min × 5 | On the other 5 reps, just mark open/closed counts for the trend line. |
| **Weekly retro** | 30 min | Did the metrics move? Log the week. Set next week's one goal. |

---

## 4. Metrics & gates

### Process metric (training wheels — gameable, build-the-habit)
**Open ratio** = open questions ÷ total questions asked, per lab rep.

### Outcome metric (the real scoreboard — harder to game)
**"Surfaced something new?"** — yes/no per lab: did this conversation reveal something you did **not
already know or expect**? Log one line on what it was. A high open ratio with no new information
means the ratio is lying.

### Phase-1 → Phase-2 advancement gate
Advance when **both**, for **2 consecutive weeks**:
- Open ratio **≥ 60%**, and
- "Surfaced something new" hits **≥ 3 of 4** weekly labs.

### Week-5 method-check (guardrail)
If you haven't passed the gate by **end of Week 5**, do **not** just wait — that's a signal the
*drill is wrong*, not that you need more time. Diagnose and change the method.

### Honesty hardening
- **Regular:** paste a lab transcript into the `question-coach` skill; it scores open ratio and
  outcome **independently** of your self-assessment.
- **Monthly:** ask one trusted report — *"Did that 1:1 feel different? Did you tell me something
  you normally wouldn't?"* This is the ground truth.

### Week-0 baseline (mandatory, before changing anything)
Instrument one ordinary 1:1 and record your **current** open ratio and outcome score. Without a
baseline you'll confuse *feeling* better with *being* better — the exact delusion this rig exists to
kill.

---

## 5. 12-week arc

| Week | Focus | Gate / event |
|---|---|---|
| **0** | Baseline | Measure current open ratio + outcome. Change nothing. |
| **1–2** | Phase 1: open questions | Build the reflex. Drill closed→open daily. |
| **3–4** | Phase 1 continued | Watch for the 2-week gate. |
| **5** | **Method-check** | Passed the gate? Advance. If not, change the drill, don't wait. |
| **6–8** | Phase 2: follow the thread | Drop-the-agenda reps. Score thread-follow rate. |
| **9–11** | Phase 2 under load | Hardest threads, highest-stakes 1:1s. Monthly report check. |
| **12** | **Stop & reassess** | Graduate / re-up on a new target / kill it. Review the full trend. |

---

## 6. Weekly log template

Copy one block per week into `log.md` (the skill appends here automatically).

```
## Week N — <phase> — <date>
Lab rep: <who / which meeting>
Open ratio: __% (baseline was __%)
Light-tally reps: open/closed → _/_, _/_, _/_, _/_, _/_
Surfaced something new? (this lab): Y/N — <one line on what>
Labs this week hitting "new": _/4
Worst closed question: "<quote>" → rewritten open: "<quote>"
[Phase 2] Dropped thread: "<quote>" → follow-up I should've asked: "<quote>"
Gate status: <not yet / 1st qualifying week / ADVANCED>
Next week's one goal: <…>
```
