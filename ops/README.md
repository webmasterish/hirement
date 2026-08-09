# Ops


Deploy, backup and maintenance tooling.


********************************************************************************

## Current state


All manual. The commands live as shell snippets inside the website notes, kept
outside this repo. The only versioned artifact today is `rsync_exclude`, still
sitting in `website/config/` in the dev tree.


********************************************************************************

## To build


- `deploy/` - rsync deploy to Hostinger, replacing the hand-run commands in the
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


Production: Hostinger, `~/domains/hirement.com/public_html/`, reached with
`ssh u918436082@hostinger`. DNS through Cloudflare. No CI.
