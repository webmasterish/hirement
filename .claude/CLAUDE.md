# Hirement monorepo

Monorepo for everything related to **hirement.com** — a curated directory of
hiring/recruitment resources (WordPress-based), owned and run by Webmasterish
(Bassam Mardini / DotAim).

**Status: scaffold only.** The repo currently holds structure, config and docs.
The actual website has *not* been migrated in yet — it still lives at the
external paths below. Do not assume a path exists in this repo without checking.


********************************************************************************

## Scope — stay inside the repo


**Do not read, write, or run anything outside this repo directory unless
explicitly asked to.** That includes the whole surrounding `httpdocs/` tree —
the live dev site, and especially `httpdocs/notes/`, which is the owner's
personal scratchpad, not project input.

The paths below are recorded for orientation only. They are not yours to touch
until asked, file by file.


--------------------------------------------------------------------------------

### Where things live today


| What | Path |
| --- | --- |
| This repo | `/media/data2/www/localhost/subs/hirement/httpdocs/repo` |
| Local dev WP install | `/media/data2/www/localhost/subs/hirement/httpdocs/website/wp` |
| WP theme (own git repo) | `…/website/wp/content/themes/hirement` |
| Website notes (3k+ lines) | `…/website/Hirement_website_notes.md` |
| Dev notes | `…/notes/Hirement_Dev_Notes.md` |
| Business notes (**secrets**) | `/media/data2/www/sites/Hirement.com/Hirement_notes.md` |
| Brand identity assets | `/media/data2/www/sites/Hirement.com/identity` |

`Hirement_website_notes.md` is the project's real history — hosting setup,
Apache vhosts, SSL, DB migrations, the 2025-08 DigitalOcean → Hostinger move,
deploy commands, MCP setup. It is chronological, newest at the bottom. Useful
background for infra work, but ask before opening it.


--------------------------------------------------------------------------------

### Remotes

- Monorepo: `git@webmasterish.github.com:webmasterish/hirement.git` (branch `main`)
- Theme: `git@webmasterish.github.com:webmasterish/hirement_wp_theme.git` (branch `master`)

Note the SSH host alias `webmasterish.github.com` — it maps to a specific key in
`~/.ssh/config`. Keep it; a plain `github.com` remote will use the wrong identity.


********************************************************************************

## Secrets — hard rule


The notes files and `wp/.config/*` contain **live plaintext credentials**:
DB passwords, WP salts, Cloudflare / Twitter / Adzuna API keys, Mailchimp,
Google/GitHub/social account passwords, Hostinger SSH and MCP app passwords.

- **Never commit any of it**, not even to a private repo.
- When migrating notes into `docs/`, strip credentials and leave a pointer to
  where they live outside the repo.
- `wp/.config/master_config.php`, `config.php` and `api_keys.php` are
  environment files — commit `*.sample.php` templates only.
- Before any `git add`, check for keys/passwords in the diff.
- Do not paste these values into commit messages, PR bodies, or issues.


********************************************************************************

## WordPress install layout (non-standard)


The install uses a relocated core and content dir:

```
website/wp/
	cms/          → WordPress core (vendored, upgraded via WP admin — not ours)
	content/      → wp-content: themes/, plugins/, uploads/, logs/
	.config/      → master_config.php, config.php, api_keys.php (env, secrets)
	wp-config.php → loads .config/
	.htaccess
```

- Local URL: `http://hirement.localhost/website/wp` — local DB `hirement_website_wp`
  (root/root).
- Core (`cms/`) is **not** versioned here and should stay excluded.
- Third-party plugins are not ours: wp-job-manager, contact-form-7 (+ conditional
  fields, flamingo), mailster, newsletter (+ extensions), wp-super-cache,
  wp-crontrol, advanced-cron-manager, wp-extended-search, wp-term-order,
  mailgun, mcp-adapter.


********************************************************************************

## The theme — `content/themes/hirement`


~920 PHP files / ~290k LOC. Not a typical WP theme: it carries a homegrown
framework under `includes/DotAim/` (namespace `DotAim`, custom autoloader in
`NS.php`) providing an admin panel/component/field system, listings, jargon,
upvotes, shortcodes, meta boxes, REST API.

- `includes/DotAim/Admin/` — Panel/Component/Field builder used by all settings screens
- `includes/DotAim/Admin/__/` and any `__*` path — scratch/experimental, **gitignored**
- `assets/css/compiled_styles.css`, `assets/js/compiled_scripts.js` — **generated**,
  gitignored; edit the sources, not the compiled output
- `style.css` holds only the WP theme header, no styles
- Releases: `npm version patch|minor|major -m "msg"` (auto `git add --all`,
  push + tags via npm hooks)


--------------------------------------------------------------------------------

### Code conventions (follow these — the codebase is highly consistent)

- **Tabs** for indent, LF, UTF-8, final newline, ~80 col (see `.editorconfig`)
- **Allman braces** — opening brace on its own line, for everything
- Aligned `=` in assignment blocks and aligned `:` in doc/property lists
- Every function/method ends with a `// function_name()` comment
- `@since 1.0.0` docblocks on classes, methods, properties
- Banner comments delimit sections:

```php
	/* ===========================================================================
	 * ---------------------------------------------------------------------------
	 * PROPERTIES - START
	 * ---------------------------------------------------------------------------
	 * ======================================================================== */
```

- Inline separator between logical steps:
  `// ---------------------------------------------------------------------------`
- `@consider` / `@todo` tags mark deferred work — leave them in place
- Early returns / guard clauses over nesting
- `_debug_log( $val, $title )` in `functions.php` writes to `logs/debug.log`


********************************************************************************

## Environment


PHP 8.5 CLI (theme was patched for 8.3 compat; `style.css` still claims 7.4
minimum — treat that header as stale). WP-CLI 2.12, Node 24, npm 11.
Local stack is Apache + MySQL under `/media/data2/www/localhost`.


********************************************************************************

## Deployment (current, manual)


Production is on **Hostinger** (`ssh u918436082@hostinger`,
`~/domains/hirement.com/public_html/`), moved from DigitalOcean 2025-08.
DNS via Cloudflare.

Deploys are `rsync -auvz --exclude-from=website/config/rsync_exclude` from the
local tree, logged to `website/logs/`. There is no CI. Two production-only
divergences are recorded in the notes and will bite if blindly overwritten:

1. `includes/DotAim/Admin/Components/App_Settings/sections/Traffic_Generator.php`
   is **deleted on prod** (puphpeteer/Puppeteer breaks there).
2. In `includes/DotAim/DotAim.php`, `webmasterish_filter_components_directories()`
   has the `Listings/Components` path commented out on prod.

Formalising this into versioned scripts under `ops/` is one of the goals of
this repo.


********************************************************************************

## Planned repo layout


```
.claude/     → this file, agent config
docs/        → notes migrated out of the loose .md files (secrets stripped)
identity/    → brand assets (logos, OG images, banners)
ops/         → deploy, backup, maintenance scripts + rsync excludes
website/     → the WP site, once migrated (core excluded)
```

Directories exist as stubs with their own README.

Current thinking on migration: **copy everything over as a starting point** and
keep `hirement_wp_theme` around as a legacy archive for history lookups, rather
than merging its commits in. Not final — the mechanics still need thinking
through. Until then the theme stays where it is, tracked by its own repo.


********************************************************************************

## Working notes


- Stay inside the repo (see the scope rule above).
- The local site serves from the live dev paths — moving files out of that tree
  breaks it. Only on explicit instruction.
- Don't reformat existing theme code to modern PSR style; match what's there.
- Don't commit `logs/`, `backups/`, `*.sql`, `node_modules/`, `__*`.
- Prefer appending a dated section to the notes files over rewriting them.
