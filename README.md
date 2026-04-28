# Garage Door Up Workflow

A starter kit for **working with the garage door up**. The kind where you narrate as you go and don't let your roadmap turn into a fossil.

## What you need

- [Claude Code](https://claude.com/claude-code) installed.
- A copy of this folder on your computer.
- About 15 minutes to set up. Then 5–10 minutes most days, optionally ~10 minutes on Sundays or Monday mornings, and ~1 hour on Fridays.

## How to use it

1. **Set up your project (once).** Open this folder in Claude Code and run `/north-star`. It asks you the questions that matter: what you're building, who it's for, why you care, what the next move is. It then writes the answers into a single document called `north-star.md`. Everything else in this system points back to that document. Takes about 15 minutes. Do this when you start; you won't do it again.

2. **Ground the week (optional).** Going into Monday with a fresh view of the week's plan helps the work feel grounded rather than rediscovered. If that's useful for you, run `/plan-week` [PLAN-WEEK TIMING] (~10 min). It reads back what Friday-you wrote into the "Now" box and lets you confirm, tweak, or rewrite it. Skip it if Friday's plan still feels live.

3. **Check in each morning.** Run `/start-day` (~3 min). It surfaces this week's "Now" box and asks you to name today's concrete task — a confirmation that today's work points at the week's plan.

4. **Reflect each evening.** Run `/end-day` (~5 min). Three short questions about how the day went, in your own words. Raw is fine — no need to polish.

5. **Wrap up on Friday.** Run `/end-week` (~60 min). It reads your week back to you, walks you through updating your north-star document, and helps you draft a short public post about what you learned.

6. **Publish the Friday post.** Somewhere, even if you don't yet have an audience. Garage door up.

> Each ritual ends by committing its output to git and pushing to your remote (if one is configured) — so you don't have to think about it. If you ever want to commit something else manually, run `/commit`.

The skills handle the structure so you don't have to. Your job is to build the thing and answer the questions honestly.
