---
name: sync-template
description: Pulls scaffolding updates from the upstream `template` git remote into this project. Use when the user says "/sync-template", "pull template updates", "sync from template", or "update skills from template".
---

# Sync Template

The maintenance ritual. Goal: bring the project's meta-files up to date with the upstream `template` remote **without losing project-specific content**.

The template owns scaffolding. The user owns their daily logs, weekly posts, and north-star — and also owns the project-specific edits made to template files (the project name, substituted placeholders, sections added on top of the template). This ritual is a **deliberate cherry-pick**, not a blind overwrite. It moves bits in one direction only — from `template/main` into the working tree — and it preserves local customizations.

`git checkout template/main -- <path>` is the wrong tool here. It will silently destroy the project name, placeholder substitutions, and any project-specific sections the user added on top of the template. Use `Edit` instead, hunk by hunk.

## Procedure

### 1. Ensure the template remote exists

Run `git remote get-url template`. If it errors, the remote isn't set up — add it:

```
git remote add template https://github.com/tylerdurrett/garage-door-up.git
```

Announce in one line that the remote was added, then continue. Adding a git remote is reversible and non-destructive, so it doesn't need a confirmation gate.

### 2. Pre-flight: refuse to sync over uncommitted work in meta-paths

Run `git status --porcelain -- .claude/skills/ AGENTS.md README.md templates/`. If the output is non-empty, the user has uncommitted edits in the meta-paths. Stop, surface the output, and ask the user to commit, stash, or discard before re-running. Merging on top of in-progress edits would mangle them.

User content (`north-star.md`, `daily-log/`, `weekly-posts/`, `.claude/settings.local.json`) is intentionally outside this check — those paths are excluded from the sync, so dirty edits there are fine.

### 3. Fetch and list changes

- `git fetch template`.
- `git diff --name-only HEAD template/main -- .claude/skills/ AGENTS.md README.md templates/` to list changed files in the meta-paths.

If the output is empty, say `Already up to date with template (template/main @ <short-sha>)` and stop. Get the sha with `git rev-parse --short template/main`.

For each changed file, label it:

- `(modified)` — exists on both `HEAD` and `template/main`. Needs a careful merge.
- `(added on template)` — new file on template, doesn't exist locally. Safe to copy directly.
- `(local-only)` — exists locally but not on `template/main`. **Will not be touched** by this ritual.

Use `git cat-file -e HEAD:<path>` and `git cat-file -e template/main:<path>` to determine each label.

### 4. Build the merge plan, file by file

For every `(modified)` file, run `git diff HEAD template/main -- <path>` and read the full diff. Do not skim. The point of this ritual is to look at what's actually changing.

Classify every hunk into one of three buckets:

- **Apply** — pure scaffolding change (new principle, reworded instruction, new section that doesn't conflict with anything local, structural cleanup). The hunk doesn't touch project-specific content.
- **Preserve** — the hunk would clobber project-specific local content. Skip it. The local version stays.
- **Apply-with-substitution** — the hunk reworks a section that locally contains a placeholder substitution (e.g. project name, weekly cadence). Apply the structural change but keep the local substituted value.

#### How to spot project-specific content

Watch for these patterns in the local (HEAD) version. They are project-specific and must be preserved:

- **Placeholder substitutions.** The template ships with `[PROJECT NAME]`, `[PLAN-WEEK TIMING]`, and similar bracketed placeholders that the `/north-star` ritual fills in. If the diff shows the template "adding back" a `[…]` placeholder where local has a real value, that's a substitution — preserve the substitution, apply any other change to the surrounding text.
- **Project-specific sections.** Sections present locally but absent from `template/main` (e.g. a section pointing to a sibling repo, paths to external systems, project-specific operational notes, Slack/Discord workspace info). The diff will show these as `-` lines because the template doesn't have them. Do not remove them.
- **Locally-edited bullets or sentences.** Single lines where local content has been tailored to the project. Harder to detect — the giveaway is that the local version names something specific (a person, a tool, a path, a domain) that the template wouldn't know about.

When unsure whether a `-` line in the diff is "template removed this" or "we added this locally and template never had it," check `git log template/main -- <path>` and look at the file's history on the template side. If the line was never in the template's history, it's a local addition — preserve.

#### Surface the plan

For each `(modified)` file, write a short plan to the user. Format:

```
<path>
  Apply:
    - <one-line description of each scaffolding hunk to apply>
  Preserve:
    - <one-line description of each local section / substitution being kept>
```

For `(added on template)` files, just list them — they'll be copied as-is.

Then ask: _"Apply this plan? (y/n, or name a file to see its full diff)"_

If the user wants the raw diff for a file before deciding, run `git diff HEAD template/main -- <path>` and show it.

### 5. Apply the merge

For each `(modified)` file, use `Read` to load the local file and the template version (`git show template/main:<path>` for the template content), then use `Edit` to apply each "Apply" hunk. Skip "Preserve" hunks. For "Apply-with-substitution" hunks, edit the surrounding wording but type the local substituted value into the new text by hand.

For each `(added on template)` file: `git checkout template/main -- <path>` is fine — there's no local content to preserve.

Never run `git checkout template/main -- <path>` on a `(modified)` file. That's the bug this rewrite exists to fix.

After all edits, run `git status` and `git diff` and show them. The user should be able to read the resulting diff and see exactly what landed — both the scaffolding gains and the preserved local content.

### 6. Commit & push

Per `AGENTS.md` ("Persist the work"), stage and commit the files this ritual touched, then push if a remote exists.

- **Files to stage:** only the files this ritual touched (the merged `(modified)` files plus any `(added on template)` files). Never `git add -A`.
- **Commit message:** `Sync from template @ <short-sha>` where `<short-sha>` is `git rev-parse --short template/main`.

The push targets `origin`. Never push to `template` — from this project's perspective the template is read-only.

If the user said something like "don't commit until I review," stop after step 5 and let them inspect the working tree before you commit.

### 7. Stop

Don't audit the synced skills, suggest follow-up edits, or open the diffs and start "improving" them. The point of the sync is to track upstream cleanly. If a synced skill no longer fits this project, that's a separate conversation.

## Files touched

- `.claude/skills/**` — merge from `template/main` for any file that differs; preserve local customizations.
- `AGENTS.md`, `README.md` — merge from `template/main` if changed; preserve project name, placeholder substitutions, and project-specific sections.
- `templates/**` — merge from `template/main` for any file that differs.
- All other paths (`north-star.md`, `daily-log/`, `weekly-posts/`, `.claude/settings.local.json`, etc.) — never touched.
