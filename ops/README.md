# Ops


Deploy, backup and maintenance tooling.


********************************************************************************

## Current state


All manual. The commands live as shell snippets inside the website notes, kept
outside this repo. The only versioned artifact today is `rsync_exclude`, still
sitting in `website/config/` in the dev tree.


********************************************************************************

## To build


- `deploy/` - rsync deploy to Hetzner, replacing the hand-run commands in the
	notes. Has to preserve the two production-only divergences documented in
	`.claude/CLAUDE.md`: `Traffic_Generator.php` removed, and `Listings/Components`
	commented out in `DotAim.php`.
- `backup/` - DB dump plus files tarball, both ends.
- `maintenance/` - transient cleanup, trash purge, table optimize. The SQL for
	these is already written down in the notes, under 2022-10-17.
- `rsync_exclude` - move it in from `website/config/`.

Once `deploy/` exists, wire it into step 5 of the `/done` skill.


********************************************************************************

## Target


Production: the owner's Hetzner server since 2026-07-30,
`/var/www/vhosts/dotaim/hirement.com`, reached with `ssh webmasterish@hetzner-dotaim`.
DNS through Cloudflare. No CI.

Hosting history is DigitalOcean, then Hostinger in 2025-08, then Hetzner. Both
older hosts are dead references. The two production divergences noted in
`.claude/CLAUDE.md` date from Hostinger and need re-checking on Hetzner before
anything is built around them.
