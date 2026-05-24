# Theme portability notes

This site uses [`mmistakes/jekyll-theme-basically-basic`](https://github.com/mmistakes/jekyll-theme-basically-basic) via `remote_theme`. The bulk of the site is theme-agnostic, but a handful of files are coupled to Basically Basic and will need to be redone if you switch themes.

## What's portable (no rework on theme switch)

- `_posts/*` — all posts use only standard Jekyll front matter, `{{site.baseurl}}` for asset paths, and the gallery include below.
- `assets/*` — images, CSS, profile pic.
- `_config.yml` — almost everything except the `remote_theme:` line and `search:` (which is a Basically Basic feature).
- `_data/social.yml`, `_data/navigation.yml` — the YAML data is portable. The keys (`title`, `url`, `icon`, `rel`) match what most Jekyll themes consume, but a new theme may want a different shape.
- `_includes/gallery.html` + `assets/css/gallery.css` — self-contained photo-gallery feature, opted into per post via `{% include gallery.html %}`. Uses the WordPress-imported `<figure><ul>...</ul></figure>` markup. No theme dependencies.
- `index.md`, `about.md`, `blog.md` — rewritten to use only `layout: page` and `layout: posts` (the latter is universal among themes that paginate posts).

## What's theme-specific (needs porting on theme switch)

| File | Coupled to | What happens on theme switch |
|---|---|---|
| `_includes/contact-list.html` | Basically Basic's sidebar; references `icon-{{ name }}.svg` files in the theme | Silently ignored — sidebar contact list disappears |
| `_includes/navigation.html` | Basically Basic's sidebar nav; references `site.data.theme.t.*` localization | Silently ignored |
| `_includes/icon-mastodon.svg` | Only useful for themes that follow the `icon-{name}.svg` lookup pattern | Silently ignored |
| `_layouts/posts.html` | References Basically Basic's `posts-paginated.html` and `page-intro.html` includes | **Build error** if the new theme doesn't have those includes — delete or rewrite |
| `_data/theme.yml` | All keys (`skin`, `t:` strings, `google_fonts`) are Basically Basic's vocabulary | Silently ignored |
| `_config.yml`: `search: true` and `search_provider:` | Basically Basic's lunr search | Silently ignored |
| `blog.md`: `entries_layout: list` | Basically Basic's posts-paginated convention | Silently ignored — page may render differently |

## Procedure for switching themes

1. Change `remote_theme:` in `_config.yml` to the new theme.
2. Delete `_layouts/posts.html` (otherwise it'll error on missing includes).
3. Rewrite `_includes/contact-list.html` and `_includes/navigation.html` against the new theme's expected hooks (or delete them and use whatever the new theme provides out of the box).
4. Check `blog.md`'s `layout:` and `entries_layout:` against the new theme's docs.
5. Update `_data/theme.yml` to whatever shape the new theme expects (or delete if unused).
6. `bundle update` and `bundle exec jekyll serve` to verify.

Posts, assets, and `index.md` / `about.md` should not require any changes.
