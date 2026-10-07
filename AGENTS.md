# Lukas's Personal Website

Hugo static site deployed to GitHub Pages at `https://lukasrobertson.org/` (repo `marmalade-does/lroberts.github.io`; DNS on Cloudflare, records unproxied).

## Build & Deploy

- **Build:** `hugo` (local Hugo v0.123.7+extended)
- **Deploy:** Push to `main` triggers GitHub Actions (`.github/workflows/`) which builds with `hugo --minify` and deploys to GitHub Pages
- **Dev server:** `hugo server`

## Project Structure

```
content/
  _index.md              # Homepage content
  blog/
    _index.md            # Blog listing page
    test-post.md         # Blog posts go here
layouts/
  index.html             # Homepage template (just renders .Content)
  _default/
    baseof.html          # Base template (nav, styles, footer, CV date script)
    list.html            # Section listing template (blog index)
    single.html          # Single page template (has wikilink regex processing)
    _markup/
      render-link.html   # Markdown link render hook (see gotcha below)
  shortcodes/
    wikilink.html        # [[wikilink]] shortcode for blog cross-references
static/
  images/                # Profile photo etc.
  assets/
    favicon.png
    cvs/                 # CV PDFs and metadata
hugo.toml                # Site config
```

## Key Details

- **No theme** — all templates are in `layouts/`
- **Goldmark unsafe mode** is enabled (`markup.goldmark.renderer.unsafe = true`) so raw HTML in markdown works
- **Wikilinks:** `single.html` post-processes content with regex to convert `[[slug]]` and `[[slug|text]]` into blog links
- **CV date:** `baseof.html` has a script that fetches `assets/cvs/cv-meta.json` for the CV's last-updated date. The JSON is auto-generated during CI from git history

## Internal Links

The site now serves from the domain root, but it previously lived at a subpath (`/lroberts.github.io/`). Keep links base-path-safe so a move back still works.

**Hugo's `relURL` behavior:** `relURL` only prepends the base path when the input does NOT start with `/`.

The render hook in `render-link.html` handles this by stripping the leading `/` before calling `relURL`. If you add new internal links in markdown content, just use standard `[text](/path)` syntax and the hook will fix them.

**In templates** (not markdown), always use `relURL` without a leading slash, or use `.RelPermalink` / `.Site.Home.RelPermalink` which handle the base path correctly.

**Shortcodes inside markdown link destinations do not work** — `[text]({{< shortcode >}})` is not processed by Hugo.
