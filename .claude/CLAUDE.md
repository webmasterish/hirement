# Hirement monorepo

Monorepo for everything related to hirement.com, a curated directory of
hiring/recruitment resources built on WordPress. Owned and run by Webmasterish
(Bassam Mardini / DotAim).

Status: scaffold only. The repo holds structure, config and docs so far. The
website has not been migrated in yet; it still lives at the external paths
listed below. Don't assume a path exists in this repo without checking.


********************************************************************************

## Working rules


--------------------------------------------------------------------------------

### Stay inside the repo


Do not read, write, or run anything outside this repo directory unless
explicitly asked to. That covers the whole surrounding `httpdocs/` tree, the
live dev site, and above all `httpdocs/notes/`, which is the owner's personal
scratchpad and not project input.

The paths further down are recorded for orientation. They are not yours to touch
until asked, file by file.


--------------------------------------------------------------------------------

### Nothing gets deleted


Never delete or overwrite a file unless explicitly told to. Move it to a backup
under a `__`-prefixed dir instead (gitignored):

```
__/backups/<YYYY-MM-DD>/<original/relative/path>
```

Same when replacing a file: back up the old version first, then write. Say what
was backed up and where. Keeping or deleting it later is the owner's call.


--------------------------------------------------------------------------------

### Be concise


Clear and to the point. No preamble, no restating the question, no explaining
work that speaks for itself. Report what changed and anything that needs a
decision. Expand only when asked for detail.


--------------------------------------------------------------------------------

### Write like a person, not a model


Applies to everything: chat replies, code comments, docs, commit messages.

- ASCII only. No em dash, en dash, curly quotes, ellipsis character, arrows, or
  any other character that isn't on a normal keyboard. Use a plain hyphen, a
  comma, or start a new sentence. Exception: when the character is part of the
  actual content, such as a filename or a quoted string.
- Skip the tells: "it's not just X, it's Y", "let's dive in", "comprehensive",
  "robust", "seamless", "leverage", a bolded lead-in on every bullet, a closing
  paragraph that restates what was just said.
- Vary sentence length. Say the thing directly. Where a fact is uncertain, say
  so plainly rather than hedging around it.


********************************************************************************

## Where things live today


| What | Path |
| --- | --- |
| This repo | `/media/data2/www/localhost/subs/hirement/httpdocs/repo` |
| Local dev WP install | `/media/data2/www/localhost/subs/hirement/httpdocs/website/wp` |
| WP theme (own git repo) | `<dev>/website/wp/content/themes/hirement` |
| Website notes (3k+ lines) | `<dev>/website/Hirement_website_notes.md` |
| Dev notes | `<dev>/notes/Hirement_Dev_Notes.md` |
| Business notes (secrets) | `/media/data2/www/sites/Hirement.com/Hirement_notes.md` |
| Brand identity assets | `/media/data2/www/sites/Hirement.com/identity` |

`Hirement_website_notes.md` is the project's real history: hosting setup, Apache
vhosts, SSL, DB migrations, the 2025-08 DigitalOcean to Hostinger move, deploy
commands, MCP setup. Chronological, newest at the bottom. Good background for
infra work, but ask before opening it.


--------------------------------------------------------------------------------

### Remotes

- Monorepo: `git@webmasterish.github.com:webmasterish/hirement.git` (branch `main`)
- Theme: `git@webmasterish.github.com:webmasterish/hirement_wp_theme.git` (branch `master`)

The SSH host alias `webmasterish.github.com` maps to a specific key in
`~/.ssh/config`. Keep it. A plain `github.com` remote picks the wrong identity.


********************************************************************************

## Secrets, hard rule


The notes files and `wp/.config/*` hold live plaintext credentials: DB
passwords, WP salts, Cloudflare / Twitter / Adzuna API keys, Mailchimp,
Google/GitHub/social account passwords, Hostinger SSH and MCP app passwords.

- Never commit any of it, private repo or not.
- When migrating notes into `docs/`, strip the credentials and leave a pointer
  to where they live outside the repo.
- `wp/.config/master_config.php`, `config.php` and `api_keys.php` are
  environment files. Commit `*.sample.php` templates only.
- Check the diff for keys and passwords before any `git add`.
- Never paste these values into commit messages, PR bodies, or issues.


********************************************************************************

## WordPress install layout (non-standard)


Core and content dirs are relocated:

```
website/wp/
	cms/          # WordPress core, vendored, upgraded via WP admin, not ours
	content/      # wp-content: themes/, plugins/, uploads/, logs/
	.config/      # master_config.php, config.php, api_keys.php (env, secrets)
	wp-config.php # loads .config/
	.htaccess
```

- Local URL `http://hirement.localhost/website/wp`, local DB
  `hirement_website_wp` (root/root).
- `cms/` is not versioned here and stays excluded.
- Third-party plugins, none of them ours: wp-job-manager, contact-form-7 (plus
  conditional fields, flamingo), mailster, newsletter (plus extensions),
  wp-super-cache, wp-crontrol, advanced-cron-manager, wp-extended-search,
  wp-term-order, mailgun, mcp-adapter.


********************************************************************************

## The theme, `content/themes/hirement`


Around 920 PHP files and 290k LOC. It carries a homegrown framework under
`includes/DotAim/` (namespace `DotAim`, custom autoloader in `NS.php`) providing
an admin panel/component/field system, listings, jargon, upvotes, shortcodes,
meta boxes and a REST API.

- `includes/DotAim/Admin/` is the Panel/Component/Field builder behind every
  settings screen.
- `includes/DotAim/Admin/__/` and any `__*` path is scratch or experimental,
  gitignored.
- `assets/css/compiled_styles.css` and `assets/js/compiled_scripts.js` are
  generated and gitignored. Edit the sources.
- `style.css` holds the WP theme header only, no styles.
- Releases: `npm version patch|minor|major -m "msg"`, which runs `git add --all`
  and pushes with tags through npm hooks.


--------------------------------------------------------------------------------

### Code conventions

The codebase is very consistent. Match it.

- Tabs for indent, LF, UTF-8, final newline, around 80 columns (`.editorconfig`).
- Allman braces everywhere, opening brace on its own line.
- Aligned `=` in assignment blocks, aligned `:` in doc and property lists.
- Every function and method closes with a `// function_name()` comment.
- `@since 1.0.0` docblocks on classes, methods and properties.
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
- `@consider` and `@todo` mark deferred work. Leave them in place.
- Early returns and guard clauses over nesting.
- `_debug_log( $val, $title )` in `functions.php` writes to `logs/debug.log`.


********************************************************************************

## Environment


PHP 8.5 CLI. The theme was patched for 8.3 compat and `style.css` still claims
7.4 minimum, so treat that header as stale. WP-CLI 2.12, Node 24, npm 11. Local
stack is Apache and MySQL under `/media/data2/www/localhost`.


********************************************************************************

## Deployment (current, manual)


Production runs on Hostinger (`ssh u918436082@hostinger`,
`~/domains/hirement.com/public_html/`), moved off DigitalOcean in 2025-08. DNS
through Cloudflare.

Deploys are `rsync -auvz --exclude-from=website/config/rsync_exclude` from the
local tree, logged to `website/logs/`. No CI. Two production-only divergences
are recorded in the notes and will bite if blindly overwritten:

1. `includes/DotAim/Admin/Components/App_Settings/sections/Traffic_Generator.php`
   is deleted on prod, because puphpeteer/Puppeteer breaks there.
2. In `includes/DotAim/DotAim.php`,
   `webmasterish_filter_components_directories()` has the `Listings/Components`
   path commented out on prod.

Turning this into versioned scripts under `ops/` is one of the goals of the
repo.


********************************************************************************

## Planned repo layout


```
.claude/     # this file, skills, agent config
docs/        # notes migrated out of the loose .md files, secrets stripped
identity/    # brand assets: logos, OG images, banners
ops/         # deploy, backup, maintenance scripts, rsync excludes
website/     # the WP site once migrated, core excluded
```

Each dir exists as a stub with its own README.

Migration plan so far: copy everything over as a starting point and keep
`hirement_wp_theme` as a legacy archive for history lookups, rather than merging
its commits in. Not final, the mechanics still need thinking through. The theme
stays where it is until then, tracked by its own repo.


********************************************************************************

## Working notes


- The local site serves from the live dev paths, so moving files out of that
  tree breaks it. Only on explicit instruction.
- Don't reformat existing theme code to modern PSR style.
- Don't commit `logs/`, `backups/`, `*.sql`, `node_modules/`, `__*`.
- Commits go on `main`, no branches or PRs unless asked. Message style is a
  short scope prefix plus an imperative summary, e.g. `ops: add rsync deploy
  script`. Inside the theme, follow its own convention:
  `Admin/Panel/field_url(): fix escaping`.
- Push only when asked. `/done` counts as the ask.


********************************************************************************

## Skills


- `/done` (`.claude/skills/done/`): end-of-session wrap-up. Persists memory and
  docs, runs pre-flight checks, commits this session's files only, pushes,
  deploys once a deploy exists, then writes a session file to `__/sessions/`.
