---
name: done
description: End-of-session wrap-up for the Hirement monorepo. Use when the user signals the session is finished, whether by "/done", "we're done", "let's wrap this", "that's it", "wrap up", or anything similar. Judge by intent, not exact words. Persists memory and project docs, commits only this session's files, pushes to GitHub, deploys if a deploy exists, then writes and displays a session file in `__/sessions/`. Flags: no-commit / no-push / no-deploy / no-session / just-docs.
---

# End the session (`/done`)

One pass that closes a working session: persist what's durable, ship what's
ready, and leave the user a file they can read later or hand to the next
session.

Runs in order. Each step reports what it did in one line. The detail goes in the
session file, not the chat.

---

## 0. Parse the flags, by intent, not exact spelling

Everything after `/done` is freeform. Match on meaning:

| Intent | Recognise (any of) | Effect |
|---|---|---|
| skip commit | `no commit`, `no-commit`, `nocommit`, `skip commit`, `don't commit`, `without committing` | No commit. Implies no GitHub push, nothing to push. Deploy still allowed, see the note below. |
| skip GitHub push | `no push`, `no-push`, `don't push`, `local only` | Commit, but don't `git push`. |
| skip deploy | `no deploy`, `no-deploy`, `don't deploy`, `no live` | Don't deploy. A no-op while no deploy exists. |
| skip session file | `no session`, `no-session`, `no file` | Skip steps 6 and 7. |
| persist only | bare `docs` / `notes` when that word is the whole argument, plus `just docs`, `just-docs`, `docs only`, `docs-only`, `only docs`, `just notes`, `notes only`, `just save`, `just memory`, `no code`, and the same shapes with docs/notes swapped | Shorthand for no-commit plus no-push plus no-deploy. Runs steps 1-3 and 6-7 only: memory and project docs get written, nothing is committed, pushed or deployed. The session file records the changes as "not committed, just-docs run" so the next session knows they're sitting uncommitted. |

Anything else in the argument is a note from the user and goes into the session
file's summary, e.g. `/done no-deploy waiting on the theme migration`.

The one genuine ambiguity is a bare `docs` or `notes`. It reads as the
persist-only flag, but `/done docs need a rewrite next time` is plainly a note.
Rule: treat it as the flag only when the word stands alone, or with a filler
like "just" or "only". If it opens a sentence, it's a note. When it could
honestly be either, ask. One question beats an unwanted commit or a silently
skipped one.

Ambiguous or unrecognised wording: ask, don't guess. A wrong read here either
skips a commit the user wanted or deploys when they said not to.

`no-commit` plus deploy is legal, since deploying uncommitted local work is
occasionally deliberate, but warn when it happens. Live would then hold code
that isn't in git.

## 1. Guard, is anything still in flight?

Before touching anything: if a background task, subagent, cron job, or a long
live command is still running, stop and say so. Don't wrap a session whose work
hasn't landed.

## 2. Persist: memory, then project docs

1. Memory
   (`~/.claude/projects/-media-data2-www-localhost-subs-hirement-httpdocs-repo/memory/`).
   Add or update memories for anything durable and non-obvious that surfaced:
   user preferences and working-style feedback with the reason behind them,
   project state, decisions, constraints not derivable from the code or git
   history, useful external references. Update an existing memory rather than
   duplicating, and keep the `MEMORY.md` index line in sync. Skip anything the
   repo already records (code structure, past fixes, git history,
   `.claude/CLAUDE.md`) or that only mattered to this conversation.
2. Project docs. If the work changed how the codebase or a workflow behaves,
   update the relevant in-repo doc: `.claude/CLAUDE.md`, or the per-dir
   `README.md` under `docs/`, `ops/`, `identity/`, `website/`. The doc is the
   source of truth, not the chat.

Quality over volume. A wrong or noisy memory is worse than none. If it's
genuinely borderline, ask instead of guessing.

Do this first, since it creates files that step 4 has to commit.

## 3. Pre-flight checks

Cheap checks against known foot-guns, on files this session changed only.

- No secrets in the diff. This repo's standing risk. Scan for DB passwords, WP
  salts, API keys, tokens, SSH credentials. One hit blocks the commit. See the
  secrets rule in `.claude/CLAUDE.md`.
- No `__*` paths staged. Those are local-only by convention and gitignored. If
  one shows up as tracked, stop and flag it.
- Nothing outside the repo was written or moved.
- No em dash, en dash, curly quotes or other non-keyboard characters in files
  written this session, per the writing rule in `.claude/CLAUDE.md`.
- `php -l` on every changed `.php` file. A parse error must never reach live.
  This is a no-op until the site is migrated in.

A failure here blocks the deploy in step 5. A secrets hit blocks the commit too.

## 4. Commit, only this session's files

Hard rule: stage by explicit path. Never `git add -A`, `git add .`, or
`git commit -a`.

The user may have more than one session open on this repo. Committing a foreign
session's work-in-progress is the failure mode this step exists to prevent.

1. `git status --short`, compared against the files this session actually
   edited.
2. Stage only this session's paths.
3. Any other dirty file: leave it alone and list it in the reply as "left alone,
   not this session's". Don't ask about it, just report it.
4. If a file this session touched contains changes you don't recognise, stop and
   ask. That's the concurrent-edit case and it can't be resolved by guessing.
5. Commit on `main`, no branches or PRs unless asked. Message style is a short
   scope prefix plus an imperative summary, matching what's already in the log:
   `ops: add rsync deploy script`, `docs: split hosting notes out of website
   notes`. Inside the theme, follow its own convention:
   `Admin/Panel/field_url(): fix escaping`. Body only when the reason isn't
   obvious from the summary. Keep the `Co-Authored-By` trailer.
6. Separate concerns, separate commits. Don't force one commit over unrelated
   work.
7. Nothing to commit: say so and move on. Not an error.

Residual risk, stated honestly: if another session edited a file this session
also edited, its changes ride along in the commit. There's no way to detect that
from the working tree. Flag anything that looks off rather than committing
silently.

## 5. Push, then deploy

- GitHub: `git push` on branch `main`, remote `origin`
  (`git@webmasterish.github.com:webmasterish/hirement.git`). Report the result.
- Deploy: there is no deploy from this repo yet. The site is still served from
  the external dev tree and production is updated by hand-run rsync. Until a
  script exists under `ops/deploy/`, report "no deploy yet, skipped" and move
  on. Never improvise an rsync to live.

  Once `ops/deploy/` lands, wire it in here: run it only if files under
  `website/wp/content/themes/hirement/` changed this session, skip it for a
  docs-only session, and honour the two production-only divergences recorded in
  `.claude/CLAUDE.md` (`Traffic_Generator.php` removed on prod,
  `Listings/Components` commented out in `DotAim.php`).
- A failed deploy gets reported, never swallowed, and goes in the session file's
  "needs doing" section.

## 6. Write the session file

Path: `__/sessions/session_YYYY-MM-DD.md`. If the same day already exists, add
`_2`, `_3` and so on. `__*` is gitignored; these files belong to the user, not
the repo.

Write it after the commit and deploy so it can record the sha and the deploy
result. Aim for 50 to 90 lines. It should read cold, weeks later, to someone who
wasn't here.

````markdown
# Session - YYYY-MM-DD[ _N]

**Focus:** one line on what this session was about.

## What was done
- Short bullets. Outcomes, not narration.

## Decisions
- The call, and why. This is the part worth re-reading in a month.
- Include rejected options where the rejection is the useful bit.

## Changes
- `path/to/file.php` - what changed, one clause.
- **Commit:** `<sha>` `scope: summary`  (or "not committed, <reason>")
- **Deployed:** yes / no / skipped (no deploy yet) / FAILED, <error>

## Open / deferred
- What's unfinished, and why it was left.

## Needs doing elsewhere
- Commands to run on live, things to do in wp-admin, Cloudflare or Hostinger,
  anything waiting on a person. Exact commands in a code block, copy-pasteable.

## Backed up
- `__/backups/<date>/<path>` - what it was and why it was replaced.

## Saved to memory / docs
- `memory/<file>.md` - one line on what it records.
- `.claude/CLAUDE.md` - section updated.

## Pick up from here

```
<A ready-to-paste prompt for the next session: the goal, where things stand,
the files that matter, and the first concrete step. Written as an instruction
to Claude, not a description of the past.>
```
````

Omit any section that would be empty. An empty "Open / deferred" is noise.
Follow the house formatting rules: no markdown blockquotes anywhere, since the
rendered gutter character breaks copy-paste, and copyable content goes in code
blocks.

## 7. Display it

Print the session file's content in the reply so the user can read it without
opening the file. Then a short closing line: path, commit sha, deploy status.

Keep the chat reply itself to a few lines beyond the file. The file is the
summary.

---

## Notes

- `/done` is a standing instruction to push. The "only push when asked" rule
  still holds for ordinary commits; `/done` is the ask.
- Fine to run mid-session as a checkpoint. It does not replace saving an
  important fact the moment it appears.
- Nothing gets deleted during wrap-up. Anything replaced goes to `__/backups/`,
  per the deletion rule in `.claude/CLAUDE.md`.
