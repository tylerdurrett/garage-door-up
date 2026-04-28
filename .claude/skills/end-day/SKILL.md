---
name: end-day
description: Evening reflection ritual. Walks the user through three reflection questions and captures answers verbatim into today's daily log as raw material for Friday's weekly post. Use when the user says "/end-day", "evening reflection", "wrapping up", "done for the day", "end of day", or otherwise signals they're closing out the workday. Should take ~5 minutes.
---

# End Day

The evening ritual. Goal: capture honest raw material from the day before it evaporates. The output is feedstock for Friday's weekly review — not a polished writeup.

## Procedure

### 1. Open today's daily log

- Compute today's date as `YYYY-MM-DD`.
- Open `daily-log/YYYY-MM-DD.md`.
- If it doesn't exist, note that there's no morning intent to reflect against and offer to create the file from `templates/daily-log-template.md`. Do not refuse to run — the ritual still has value without a morning entry.

### 2. Ask three questions, one at a time

Wait for each answer before asking the next. Capture answers in the corresponding sections under "Evening Reflection" in today's daily log.

1. **What did you actually do?**
2. **What did you learn, or what surprised you?**
3. **Was there a gap between intent and outcome?** (Capture under "The gap between intent and outcome.")

### 3. Capture verbatim

Write down what the user says, not a polished version. Stream of consciousness is fine. Resist the urge to summarize, structure, or improve their phrasing. Friday-you and future-you both benefit more from raw text than from tidied text.

### 4. Flag for the north-star doc

Ask: _"Is there anything from today worth pulling into the north-star doc?"_

If yes, capture under "One thing worth pulling into the north-star doc" in today's log. **Do not edit `north-star.md`.** That's Friday's job — these flags accumulate through the week and get reviewed together.

### 5. Stop

Keep the structured ritual under 5 minutes. If the user wants to keep talking after, that's fine — but don't extend the ritual itself. A short honest entry beats a long dutiful one.

## Files touched

- `daily-log/YYYY-MM-DD.md` — write/append (the evening section).
- `north-star.md` — **do not edit** here. Flag items only.
