# Hirement

Monorepo for everything related to [hirement.com](https://hirement.com)


********************************************************************************

## Status


Scaffold. Structure, config and docs only. The website has not been migrated in
yet, it still lives at
`/media/data2/www/localhost/subs/hirement/httpdocs/website/wp`.


********************************************************************************

## Layout


| Dir | Contents |
| --- | --- |
| `.claude/` | Agent context, start with `CLAUDE.md` |
| `docs/` | Project notes and runbooks |
| `identity/` | Brand assets: logos, OG images, banners |
| `ops/` | Deploy, backup and maintenance scripts |
| `website/` | The WordPress site once migrated, core excluded |


********************************************************************************

## Secrets


No credentials belong in this repo. DB passwords, WP salts and API keys live in
`wp/.config/` and in the notes under `/media/data2/www/sites/Hirement.com/`,
both outside version control. See `.claude/CLAUDE.md`.
