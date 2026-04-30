---
name: sync-template
description: Pulls scaffolding updates from the upstream `template` git remote into this project. Use when the user says "/sync-template", "pull template updates", "sync from template", or "update skills from template".
---

# Sync Template

The maintenance ritual. Goal: bring the project's meta-files up to date with the upstream `template` remote without touching the user's content.

The template owns scaffolding. The user owns their daily logs, weekly posts, and north-star. This ritual moves bits in one direction only — from `template/main` into the working tree — and never touches user content.

## Procedure

### 1. Ensure the template remote exists

Run `git remote get-url template`. If it errors, the remote isn't set up — add it:

```
git remote add template https://github.com/tylerdurrett/garage-door-up.git
```

Announce in one line that the remote was added, then continue. Adding a git remote is reversible and non-destructive, so it doesn't need a confirmation gate.

### 2. Pre-flight: refuse to sync over uncommitted work in meta-paths

Run `git status --porcelain -- .claude/skills/ AGENTS.md README.md templates/`. If the output is non-empty, the user has uncommitted edits in the meta-paths. Stop, surface the output, and ask the user to commit, stash, or discard before re-running. Overwriting in-progress work would be silent data loss.

User content (`north-star.md`, `daily-log/`, `weekly-posts/`, `.claude/settings.local.json`) is intentionally outside this check — those paths are excluded from the sync, so dirty edits there are fine.

### 3. Fetch and diff

- `git fetch template`.
- `git diff --name-only HEAD template/main -- .claude/skills/ AGENTS.md README.md templates/` to list changed files in the meta-paths.

If the output is empty, say `Already up to date with template (template/main @ <short-sha>)` and stop. Get the sha with `git rev-parse --short template/main`.

### 4. Show the changes and ask

Print the changed-file list to the user. For each file, label it:

- `(modified)` — exists on both `HEAD` and `template/main`, will be overwritten.
- `(added on template)` — new file on template, will be created locally.
- `(local-only)` — exists locally but not on `template/main`, **will not be touched** by this ritual.

Use `git cat-file -e HEAD:<path>` and `git cat-file -e template/main:<path>` to determine each label.

Then ask: _"Apply these changes from template/main? (y/n)"_

If the user wants more detail before deciding, offer to show the full diff for a specific file (`git diff HEAD template/main -- <path>`). Don't dump full diffs by default — file lists are usually enough.

### 5. Apply

For each `(modified)` or `(added on template)` file: `git checkout template/main -- <path>`. Skip `(local-only)` files entirely.

Then run `git status` and show it to the user so they can see what landed in the working tree before the commit.

### 6. Commit & push

Per `AGENTS.md` ("Persist the work"), stage and commit the files this ritual touched, then push if a remote exists.

- **Files to stage:** only the files that were just checked out from `template/main`. Never `git add -A`.
- **Commit message:** `Sync from template @ <short-sha>` where `<short-sha>` is `git rev-parse --short template/main`.

The push targets `origin`. Never push to `template` — from this project's perspective the template is read-only.

### 7. Stop

Don't audit the synced skills, suggest follow-up edits, or open the diffs and start "improving" them. The point of the sync is to track upstream cleanly. If a synced skill no longer fits this project, that's a separate conversation.

## Files touched

- `.claude/skills/**` — overwrite from `template/main` for any file that differs.
- `AGENTS.md`, `README.md` — overwrite from `template/main` if changed.
- `templates/**` — overwrite from `template/main` for any file that differs.
- All other paths (`north-star.md`, `daily-log/`, `weekly-posts/`, `.claude/settings.local.json`, etc.) — never touched.
