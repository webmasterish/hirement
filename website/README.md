# Website


The WordPress site. **Not migrated yet** — it lives at
`/media/data2/www/localhost/subs/hirement/httpdocs/website/wp` and the local dev
server serves from that exact path.


********************************************************************************

## Target layout


```
website/
	wp/
		content/
			themes/hirement/    ← the theme (own repo today; import method undecided)
			plugins/            ← custom plugins only; third-party stay vendored
		.config/
			*.sample.php        ← templates only, never the real files
		.htaccess
		wp-config.php.sample
```

Excluded by `.gitignore`: `cms/` (WP core), `content/uploads/`, `content/upgrade*/`,
logs, backups, and the real `.config/*.php`.


********************************************************************************

## Open decision — theme history


`content/themes/hirement` is its own git repo
(`webmasterish/hirement_wp_theme`, branch `master`, ~1000 commits).

Leaning towards a **plain copy** as the starting point, with the old repo kept
as a legacy archive for looking up history. Alternatives still on the table:

- **subtree** — full history in the monorepo, one clone, can still push back
- **submodule** — repos stay separate, adds checkout friction

Not settled — the mechanics need thinking through first. Until then, the theme
is worked on in place, in its own repo.


********************************************************************************

## Local dev


- URL: `http://hirement.localhost/website/wp`
- DB : `hirement_website_wp` (root/root)
- Install was bootstrapped with a `wp_install` helper — see the 2022-09-17
	section of the website notes.
