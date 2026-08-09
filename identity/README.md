# Identity


Brand assets for hirement.com — logos, OG images, social banners.


********************************************************************************

## To migrate


Source: `/media/data2/www/sites/Hirement.com/identity`
(currently symlinked into `httpdocs/identity`).

SVG sources plus PNG exports:

- `hirement_logo_mark` — mark only
- `hirement_logo_horizontal`, `_2`, `_3`, `_4` — horizontal lockups, some with slogan
- `hirement_logo_vertical` — vertical lockup
- `hirement_og_image` — 1200x630
- `hirement_twitter_profile_banner` — 1500x500
- `hirement_youtube_banner` — 2048x1152
- `hirement_wp_theme_screenshot` — the theme's `screenshot.png` source


********************************************************************************

## Note


Keep the `.svg` sources alongside every export — the PNGs are generated from
them. When migrating, decide whether the symlink stays (site still reads from
it) or the repo becomes the source of truth and the symlink is repointed here.
