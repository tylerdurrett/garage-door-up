---
name: end-week
description: Friday weekly review and public post ritual. Reads the week's daily logs, surfaces patterns, walks the user through updating north-star.md, helps them pick a single thread for the public post, drafts the post in weekly-posts/, and runs a five-question gut-check before publishing. Use when the user says "/end-week", "weekly review", "Friday review", "weekly post", "wrap up the week", or "end of week". Takes ~60 minutes.
---

# End Week

The Friday ritual. Goal: turn five days of raw daily logs into (1) an updated north-star doc and (2) a publishable weekly post. The north-star update is the spine of the whole system — never skip it. The post is the public artifact that forces the weekly zoom-out.

## Procedure

### 1. Read the week first

Before the user writes anything:

- List the five most recent files in `daily-log/` (or however many exist this week).
- Read them in chronological order.
- Look for: recurring themes, the arc of the week, surprises, drift, "I learned X" bullets that compound across days.
- Report back what you noticed — patterns and the shape of the week, not a per-day summary.

The user reads your read of the week before they start their own. This is the input to everything that follows.

### 2. Update the north-star doc

Walk through `north-star.md` with the user, section by section. Edit in place.

- **Section 1 (One-Liner):** ask _"Is the one-liner still true?"_ Rewrite if needed.
- **Section 5 (Current Roadmap):** roll completed items into "Done" (keep last 5 only). Rewrite "Now" / "Next" / "Later" based on what the week revealed.
- **Section 6 (What I've Learned):** append a new `## Week of YYYY-MM-DD` heading with 1–3 bullets drawn from the week's daily logs (especially the "one thing worth pulling into the north-star doc" lines). This section is **append-only** — never edit older entries.
- **Section 7 (Open Questions):** add new ones; strike resolved ones.
- **Section 8 (Decisions Log):** if a real call was made this week (architecture, scope, naming), add a row with date and one-line "why."

Update the `_Last touched: YYYY-MM-DD_` line at the top.

Ask the doc's own prompts: _"Is the one-liner still true? Does the vision still pull you?"_ A "no" here is the most important signal of the week — write about it.

### 3. Pick the thread of the week

Help the user choose **one** story for the post. Push back if they try to cram three threads in.

A thread can be: a thing they built and what it taught them, a question they wrestled with, a shift in how they see the project, a failure that surprised them. Not all three at once.

### 4. Pick the week number

- Scan `weekly-posts/`. List the existing `week-NN-post.md` files.
- Suggest the next number (max NN + 1, or `01` if empty).
- Confirm with the user — they may have a different convention (e.g., week 0 for an intro post).
- Use two-digit zero-padded numbers: `week-01`, `week-07`, `week-12`.

### 5. Draft the post

Create `weekly-posts/week-NN-post.md` with this loose structure (adjust to fit the thread):

```markdown
# [Project] — Week NN: [Thread title]

_[Optional one-line subtitle.]_

---

## [The hook — what made this week interesting]

[2–4 paragraphs. Lead with the concrete thing, not the meta-frame.]

## [What I learned / what shifted]

[The honest part. What changed in your understanding of the project this week?]

## [Where this leaves things]

[One short paragraph on what's next or what's still unresolved.]

---

_Week NN+1 coming Friday._
```

Reference `templates/post-sample.md` for voice — concrete, honest, comfortable saying "I don't know yet." Don't force the sample's structure; let the thread shape the post.

Help the user draft, but **do not write the post for them**. Suggest framings, surface bullets from their daily logs, ask "what do you actually want to say here?" — let their voice do the work.

### 6. Pre-publish gut-check

Before they publish, walk through these five questions one at a time:

1. **Is there a sentence in this that scares you a little?** (If no, the post is probably too safe. The honest part is usually the part that almost didn't make it in.)
2. **Did you tell one story, or three?** (Three threads make a worse post than one. Cut.)
3. **Would you say this out loud to someone who knows you well?** (If the prose sounds different from how you'd talk, soften the prose.)
4. **Is there a "lesson learned" you didn't actually learn?** (Aspirational lessons are obvious to readers and they erode trust. Cut anything you're hoping is true rather than knowing is true.)
5. **What's the one detail that proves this is real, not generic?** (Numbers, names, specific moments. Without one, the post could be about anyone's project. Add one if missing.)

Don't quiz the user — read each question, let them sit with it, and only edit if their answer reveals a real problem.

### 7. Stop

The user publishes (or doesn't). Don't push for a polished close — sometimes the best move is to leave the post slightly rough and ship it. Garage door up.

## Files touched

- `daily-log/*.md` — read only.
- `north-star.md` — read and edit (sections 1, 5, 6, 7, 8 + last-touched date).
- `weekly-posts/week-NN-post.md` — create.
- `templates/post-sample.md` — read only (voice cue).
