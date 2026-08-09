# Website


The WordPress site. Not migrated yet. It lives at
`/media/data2/www/localhost/subs/hirement/httpdocs/website/wp` and the local dev
server serves from that exact path.


********************************************************************************

## Target layout


```
website/
	wp/
		content/
			themes/hirement/    # the theme, own repo today, import method undecided
			plugins/            # custom plugins only, third-party stay vendored
		.config/
			*.sample.php        # templates only, never the real files
		.htaccess
		wp-config.php.sample
```

Excluded by `.gitignore`: `cms/` (WP core), `content/uploads/`,
`content/upgrade*/`, logs, backups, and the real `.config/*.php`.


********************************************************************************

## Open decision, theme history


`content/themes/hirement` is its own git repo,
`webmasterish/hirement_wp_theme`, branch `master`, around 1000 commits.

Leaning towards a plain copy as the starting point, keeping the old repo as a
legacy archive for looking up history. Still on the table:

- subtree: full history in the monorepo, one clone, can still push back
- submodule: repos stay separate, adds checkout friction

Not settled. The mechanics need thinking through first. The theme is worked on
in place, in its own repo, until then.


********************************************************************************

## Local dev


- URL: `http://hirement.localhost/website/wp`
- DB: `hirement_website_wp` (root/root)
- The install was bootstrapped with a `wp_install` helper, recorded in the
	website notes under 2022-09-17.
