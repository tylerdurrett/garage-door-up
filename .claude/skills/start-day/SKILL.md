---
name: start-day
description: Morning check-in ritual. Creates today's daily log from the template if missing, surfaces a brief reminder of why the project matters and the "Now" box from north-star.md, then walks the user through a three-line intent (working on / why / done looks like). Use when the user says "/start-day", "morning check-in", "I'm starting my day", "what should I work on today", or otherwise signals the start of a working day. Should take ~3 minutes.
---

# Start Day

The morning ritual. Goal: get the user from "starting work" to "I have a concrete intent connected to the roadmap" in about three minutes. Do not coach, plan, or expand scope — just run the steps below and stop.

## Procedure

### 1. Open or create today's daily log

- Compute today's date as `YYYY-MM-DD`.
- Check for `daily-log/YYYY-MM-DD.md`.
- If missing: create the `daily-log/` directory if it doesn't exist, then copy `templates/daily-log-template.md` into the new file. Replace the `YYYY-MM-DD` placeholder in the H1 with today's date. Also strip the template-only helper line `_One file per day. Morning at the top, evening at the bottom. Keep it in the same folder as your north-star doc._` and the blank line that follows it — that note belongs on the template for whoever opens it, not in every daily log.
- If present: open it. If the morning section is already filled in, ask the user whether they want to add to it or skip the morning ritual.

### 2. Surface the why and the priorities

Read `north-star.md` and show the user two things, in this order:

1. **Why this matters** — pull 1–2 bullets from section 2 ("Why This Matters") and show them as a brief reminder. Pick the bullets that feel most live this week, not all of them. This is a short grounding moment ("here's why you're doing this at all"), not a recital — keep it to a couple of lines.
2. **The "Now" box** from section 5 (Current Roadmap) — show verbatim. This is the current priority.

Then ask: _"What slice of the Now box are you carving out for today?"_

The Now box is a week-sized chunk; the morning intent is a day-sized slice carved out of it. Phrase the question to help the user **choose** today's slice, not to verify a pre-chosen one — many mornings the user is using this ritual to figure out what today is, not to confirm it. Acceptable slices include a sub-component, a decision (e.g. "pick SQS vs Postgres"), a spike, a UI sketch, or a planning/architecture pass — anything day-sized that moves the week forward.

### 3. Soft branch: stale "Now"?

Check the `_Last touched: YYYY-MM-DD_` line at the top of `north-star.md`. If it's more than 2 days old (i.e. Friday's `/end-week` was the last edit and the optional `/plan-week` hasn't run this week), ask once:

_"Looks like the 'Now' box hasn't been touched since the weekly review. Want to run the optional `/plan-week` first for a fresh view of the week, or proceed with today?"_

Not a hard gate — accept either answer and continue. Frame it as a one-time nudge, not a recurring guilt trip; if they decline, don't ask again later in the week.

### 4. Capture the three-line intent

Ask one question at a time. Capture answers in the corresponding blockquotes under "Morning Intent" in today's daily log.

1. **Today I'm working on:** the concrete thing — a task, not a theme.
2. **Because:** how this connects to the "Now" box. If the user can't answer in one line, pause and have them re-read the doc.
3. **Done looks like:** an observable end-state.

Push back when intents are vague or oversized. Examples:

- "Make progress on auth" → not a real intent.
- "Wire up the OAuth callback so I can log in with Google" → real.

If the user resists pushback, capture their version and move on. The point is to make the friction visible, not to win.

### 5. Optionally: derailment risk

Skip on calm days. Ask on busy ones: _"What's most likely to eat the day if it happens?"_ Capture under "Most likely derailment."

**If you skip the question** (or the user declines), delete the entire `**Most likely derailment:**` heading and its placeholder blockquote from today's log — an unused placeholder is just visual noise.

### 6. Commit & push

Per `AGENTS.md` ("Persist the work"), stage and commit the files this ritual touched, then push if a remote exists.

- **Files to stage:** `daily-log/YYYY-MM-DD.md`.
- **Commit message:** `Morning intent for YYYY-MM-DD` (today's date).

### 7. Stop

Do not start coaching, breaking down the task, or expanding scope. The user's job from here is to do the work.

## Files touched

- `daily-log/YYYY-MM-DD.md` — write/append (the morning section).
- `north-star.md` — read only.
- `templates/daily-log-template.md` — read only (used to seed a new log).
