# Identity


Brand assets for hirement.com: logos, OG images, social banners.


********************************************************************************

## To migrate


Source: `/media/data2/www/sites/Hirement.com/identity`, currently symlinked into
the dev tree as `httpdocs/identity`. Outside this repo, so don't touch it
without being asked.

SVG sources with PNG exports alongside:

- `hirement_logo_mark` - mark only
- `hirement_logo_horizontal`, `_2`, `_3`, `_4` - horizontal lockups, some with
	the slogan
- `hirement_logo_vertical` - vertical lockup
- `hirement_og_image` - 1200x630
- `hirement_twitter_profile_banner` - 1500x500
- `hirement_youtube_banner` - 2048x1152
- `hirement_wp_theme_screenshot` - source for the theme's `screenshot.png`


********************************************************************************

## Note


Keep the `.svg` source next to every export, since the PNGs are generated from
them. When migrating, decide whether the symlink stays, with the site still
reading from the old location, or the repo becomes the source of truth and the
symlink points here.
