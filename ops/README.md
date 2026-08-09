# Ops


Deploy, backup and maintenance tooling.


********************************************************************************

## Current state


Everything is manual and lives in shell snippets inside
`../../website/Hirement_website_notes.md`. The only versioned artifact today is
`../../website/config/rsync_exclude`.


********************************************************************************

## To build


- `deploy/` — rsync deploy to Hostinger, replacing the hand-run commands in the
	notes. Must preserve the two production-only divergences documented in
	`.claude/CLAUDE.md` (Traffic_Generator.php removed; `Listings/Components`
	commented out in `DotAim.php`).
- `backup/` — DB dump + files tarball, both ends.
- `maintenance/` — transient cleanup, trash purge, table optimize. The SQL for
	these is already in the notes under the 2022-10-17 section.
- `rsync_exclude` — move from `website/config/`.


********************************************************************************

## Target


Production: Hostinger, `~/domains/hirement.com/public_html/`
(`ssh u918436082@hostinger`). DNS via Cloudflare. No CI.
