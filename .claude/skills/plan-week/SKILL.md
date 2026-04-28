---
name: plan-week
description: Optional weekly grounding ritual. Reads the "Now" box on north-star.md that was drafted in Friday's /end-week and lets the user confirm, tweak, or rewrite it before the workweek starts. Use when the user says "/plan-week", "ground the week", "plan the week", "Sunday check-in", "Monday morning planning", "look at the week ahead", or otherwise signals they want a fresh view of the week's intent before Monday's work begins. Should take ~5–10 minutes.
---

# Plan Week

The optional weekly grounding ritual. Goal: turn Friday's draft "Now" line into a confirmed-or-revised line that today-you actually believes in, in about ten minutes. Going into Monday with a fresh view of the plan helps the work feel grounded rather than rediscovered. If the user already feels grounded, this ritual should end fast.

## Procedure

### 1. Read the inputs

- Read `north-star.md`. Pull out the **"Now" box** from section 5 (Current Roadmap) and the `_Last touched: YYYY-MM-DD_` line.
- List `weekly-posts/`. If a file exists, identify the most recent `week-NN-post.md` — don't read it unless the user asks; just have it ready to surface.
- List `daily-log/` and identify the most recent 1–2 files from the past 7 days. Same rule — don't read until asked.

Show the user the "Now" box verbatim. Then ask: _"Does this still feel like the right Now for the week? Keep, tweak, or rewrite."_

If the user wants more context before answering, offer to read back the latest weekly post or the latest daily log. Don't push it — most weeks they won't need either.

### 2. Confirm-or-revise the "Now" box

Branch on the user's answer.

- **Keep:** no edit to the "Now" line. Update only the `_Last touched:_` date at the top of `north-star.md` to today.
- **Tweak:** capture the small edit (one or two words, a clarifying clause). Apply it to the "Now" line in §5. Update `_Last touched:_`.
- **Rewrite:** apply the same standard `/start-day` uses for the daily intent — a concrete task, not a theme. _"Wire up the OAuth callback,"_ not _"work on auth."_ If the rewrite is vague, push back once with that example. If the user resists, capture their version and move on. Update `_Last touched:_`.

### 3. Optional: name one risk

Skip on calm weeks. Ask on busy ones: _"Anything in the week ahead — meetings, travel, energy — that could eat the Now box?"_

If the answer is small or situational, naming it out loud is enough. Don't write anything down.

If the answer is structural (a recurring conflict, a constraint that will keep biting), append it to §7 Open Questions on `north-star.md`. One bullet, the user's words.

### 4. Stop

Do not break the "Now" into per-day subtasks. Do not plan Tuesday. Do not coach on energy management. The deliverable is one confirmed-or-revised line and a fresh `_Last touched:_` date. The user's job from here is to do the work — `/start-day` will surface this same line on Monday morning.

## Files touched

- `north-star.md` — read; edit §5 "Now" line and `_Last touched:_` only. Possibly append one bullet to §7 Open Questions if a structural risk surfaced.
- `weekly-posts/*.md` — read only, on request.
- `daily-log/*.md` — read only, on request.
