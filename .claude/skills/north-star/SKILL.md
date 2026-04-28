---
name: north-star
description: Project-initialization ritual. Walks the user through filling out a new north-star.md from templates/north-star-template.md and replaces [PROJECT NAME] in AGENTS.md. Use the first time someone runs this template repo, or when the user says "/north-star", "initialize the north star", "seed the north star doc", "set up this project", "I just cloned this", or otherwise signals they're starting a brand-new project. Takes ~15 minutes.
---

# North Star

The kickoff ritual. Goal: leave the user with a `north-star.md` they actually believe in and an `AGENTS.md` that knows the project's name. The North Star doc is the spine of `/start-day`, `/end-day`, and `/end-week` — a vague or aspirational first fill-out compromises every downstream ritual, so push back on weak answers in the same voice as the other skills. Do not write the user's content for them.

## Procedure

### 1. Preconditions

- Check whether `north-star.md` exists at the repo root.
  - If it exists: stop and ask whether to overwrite. Default to **no** — this doc is meant to be edited weekly via `/end-week`, not re-initialized. Overwrite only on explicit confirmation.
- Check that `templates/north-star-template.md` exists. If missing, report and stop — the repo isn't in expected shape.

### 2. Get the project name

Ask once: _"What's the project name?"_ Confirm spelling and capitalization before continuing — the name lands in two files.

### 3. Walk the template, one section at a time

Ask one question per section, wait for the answer, capture it verbatim into the corresponding blockquote or bullets. Push back on vagueness using the heuristics below — the template's own prompts are the source of truth for what "good" looks like, so quote them back when needed.

1. **§1 The One-Liner** — _"In one sentence a stranger would understand: what is this?"_
   - Reject multi-sentence answers. Reject jargon-only answers ("AI-native developer-velocity platform").
   - If they can't say it in one sentence, the template's own line applies: _"you don't understand it yet."_ Help by asking what they'd say to a friend at a coffee shop.

2. **§2 Why This Matters (to me)** — _"What's the personal reason you care enough to keep going when this gets hard? Not the pitch — the truth. Give me 1–3 bullets."_
   - If the answer sounds like a marketing line, ask: _"But why do **you** care?"_

3. **§3 Who It's For** — _"Name a real person or a sharp archetype. Not 'developers.' Not 'everyone.'"_
   - Quote the template's example back if they go generic: _"Solo devs building side projects who keep losing the thread"_ — that's the bar.

4. **§4 The Vision** — _"What does the world look like when this is working? Two or three paragraphs max."_
   - Wall of text? Ask them to cut.
   - One line? Ask what's actually different in the world.

5. **§5 Current Roadmap** — ask in three small parts:
   - **Now (this week):** one concrete task, not a theme. Apply the same standard `/start-day` uses — _"Wire up the OAuth callback,"_ not _"work on auth."_
   - **Next (next 2–4 weeks):** 2–4 items.
   - **Later (someday/maybe):** 0–3 items.
   - **Done** stays empty — `/end-week` rolls items into it.

6. **§7 Open Questions** — _"What are 2–5 things you don't know yet? Naming them is half the work."_
   - Empty is allowed but flag it: a brand-new project with zero open questions usually means the user hasn't sat with it long enough.

### 4. Skip the sections that fill themselves

Leave these as the template ships them — do not prompt the user:

- **§6 What I've Learned** — append-only via `/end-week`.
- **§8 Decisions Log** — empty table. `/end-week` adds rows.
- **§9 The Public Thread** — empty bullet. Filled as weekly posts ship.

### 5. Set the header

- Replace `[Project Name]` in the H1 with the project name from step 2.
- Set `_Last touched:_` to today's date (`YYYY-MM-DD`).
- Default status to `🌱 shaping`. Ask only if the user wants something different.

### 6. Write `north-star.md`

Create the file at the repo root with all of the above filled in. Use the template's structure verbatim — same headings, same order, same italicized prompt lines (those prompts help future-you on weekly reviews).

### 7. Update `AGENTS.md`

Replace the single occurrence of `[PROJECT NAME]` in `AGENTS.md` with the project name from step 2. Do not edit anything else in that file.

### 8. Read it back

Show the user their final one-liner and vision. Ask: _"Does the one-liner still feel true after writing it out?"_ A "no" here is the most useful signal of the session — invite them to revise on the spot before stopping.

### 9. Stop

Point them at `/start-day` for the next morning. Do not coach further, expand scope, or start working on the project itself.

## Files touched

- `north-star.md` (repo root) — **create.**
- `AGENTS.md` (repo root) — single string replacement of `[PROJECT NAME]`.
- `templates/north-star-template.md` — read only (seed).
