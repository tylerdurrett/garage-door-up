---
name: start-day
description: Morning check-in ritual. Creates today's daily log from the template if missing, surfaces the "Now" box from north-star.md, and walks the user through a three-line intent (working on / why / done looks like). Use when the user says "/start-day", "morning check-in", "I'm starting my day", "what should I work on today", or otherwise signals the start of a working day. Should take ~3 minutes.
---

# Start Day

The morning ritual. Goal: get the user from "starting work" to "I have a concrete intent connected to the roadmap" in about three minutes. Do not coach, plan, or expand scope — just run the steps below and stop.

## Procedure

### 1. Open or create today's daily log

- Compute today's date as `YYYY-MM-DD`.
- Check for `daily-log/YYYY-MM-DD.md`.
- If missing: create the `daily-log/` directory if it doesn't exist, then copy `templates/daily-log-template.md` into the new file. Replace the `YYYY-MM-DD` placeholder in the H1 with today's date.
- If present: open it. If the morning section is already filled in, ask the user whether they want to add to it or skip the morning ritual.

### 2. Surface the roadmap

- Read `north-star.md` and pull out the **"Now" box** from section 5 (Current Roadmap).
- Show it to the user verbatim. Then ask: _"Is what you're about to do today the most direct path toward this?"_

### 3. Capture the three-line intent

Ask one question at a time. Capture answers in the corresponding blockquotes under "Morning Intent" in today's daily log.

1. **Today I'm working on:** the concrete thing — a task, not a theme.
2. **Because:** how this connects to the "Now" box. If the user can't answer in one line, pause and have them re-read the doc.
3. **Done looks like:** an observable end-state.

Push back when intents are vague or oversized. Examples:
- "Make progress on auth" → not a real intent.
- "Wire up the OAuth callback so I can log in with Google" → real.

If the user resists pushback, capture their version and move on. The point is to make the friction visible, not to win.

### 4. Optionally: derailment risk

Skip on calm days. Ask on busy ones: _"What's most likely to eat the day if it happens?"_ Capture under "Most likely derailment."

### 5. Stop

Do not start coaching, breaking down the task, or expanding scope. The user's job from here is to do the work.

## Files touched

- `daily-log/YYYY-MM-DD.md` — write/append (the morning section).
- `north-star.md` — read only.
- `templates/daily-log-template.md` — read only (used to seed a new log).
