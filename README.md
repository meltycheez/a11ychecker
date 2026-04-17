# a11ychecker — accessibility test fixtures

This repository is a **Jekyll** site: HTML fixture pages live in **`_specimens/`** (Jekyll collection `specimens`). The name avoids calling a collection `pages`, which **conflicts with Jekyll’s built-in `site.pages`** and can break GitHub Pages builds. The home page is `index.html` (layout `default` lists every specimen via Liquid), and **`jekyll-sitemap`** generates `sitemap.xml` on build.

## GitHub Pages

1. Push this repository to GitHub.
2. Open the repository **Settings → Pages**.
3. Under **Build and deployment**, set **Source** to **Deploy from a branch**.
4. Choose branch **main** (or your default branch) and folder **`/` (root)**, then save.

Jekyll runs on GitHub Pages automatically. The site will be available at `https://<username>.github.io/<repo>/` (or your custom domain).

## Adding a new fixture page

1. Add `_specimens/NN-short-name.html` (use the next number in the series).
2. Start the file with front matter, for example:

```yaml
---
layout: null
title: "14 — Short description for the index"
order: 14
---

<!DOCTYPE html>
<html lang="en">
...
```

3. Use `href="{{ '/' | relative_url }}"` for “back to index” links.
4. Optional: set `permalink: /some/path.html` in front matter when the default `/:name.html` URL is not enough (e.g. nested paths for template-matching fixtures).
5. Commit and push — the **index** and **sitemap** update on the next build (no manual edits).

## Test pages

| Page | File | Issues (summary) |
|------|------|------------------|
| 01 | `_specimens/01-missing-image-alt.html` | Missing `alt`, decorative image with misleading `alt` |
| 02 | `_specimens/02-low-contrast.html` | Text and links with insufficient contrast |
| 03 | `_specimens/03-unlabeled-inputs.html` | Inputs/select/textarea without labels; checkbox without proper association |
| 04 | `_specimens/04-heading-skips.html` | Skipped heading levels; visual “heading” as plain paragraph |
| 05 | `_specimens/05-vague-links.html` | “Click here”, “read more”, empty link, image link with empty `alt` |
| 06 | `_specimens/06-no-html-lang.html` | No `lang` on `<html>` |
| 07 | `_specimens/07-duplicate-ids.html` | Duplicate `id` values |
| 08 | `_specimens/08-focus-and-aria.html` | `tabindex` misuse, `aria-hidden` on focusable descendant, positive `tabindex` |
| 09 | `_specimens/09-table-without-headers.html` | Data table using only `<td>`, no `<th>` |
| 10 | `_specimens/10-nonsemantic-button.html` | Non-interactive element styled as button; vague link |
| 11 | `_specimens/11-video-youtube.html` | Real YouTube watch/short/embed URLs; oEmbed API links; iframes without `title` |
| 12 | `_specimens/12-document-links.html` | Links to document fixtures in `fixtures/` |
| 13 | `_specimens/13-video-oembed.html` | YouTube oEmbed examples and embed HTML |
| 14 | `_specimens/14-youtube.html` | YouTube embed variations |
| 15 | `_specimens/15-oembed-test.html` | oEmbed / iframe test links |
| 16 | `_specimens/16-template-match-blog.html` | **URL fixture:** `/blog.html` — P0 wide `/blog` pattern |
| 17 | `_specimens/17-template-match-blog-post.html` | **URL fixture:** `/blog/post-1.html` — P0 only wide template |
| 18 | `_specimens/18-template-match-blog-2024-summary.html` | **URL fixture:** `/blog/2024/summary.html` — P0 narrow `/blog/2024` wins |
| 19 | `_specimens/19-template-match-courses.html` | **URL fixture:** `/courses.html` — P1 exact vs pattern |
| 20 | `_specimens/20-template-match-courses-list.html` | **URL fixture:** `/courses/list.html` — P1 pattern-only sibling |

The **index** (`index.html` with layout `default`) is meant to be navigable and is not part of the “broken” set.

### Template matching (Dinolytics / crawl QA)

Specimens **16–20** use explicit `permalink` values so the **built paths** match typical static-site URLs (including `.html`). After deploy or `jekyll build`, crawl these URLs and configure templates as follows to exercise **P0/P1** cases from QA:

| Goal | Example matchers (adjust to match stored URIs in your environment) | Pages to crawl |
|------|-------------------------------------------------------------------|----------------|
| **P0** — wide vs narrow prefix | Template A: `pattern` `/blog` · Template B: `pattern` `/blog/2024` | `/blog.html`, `/blog/post-1.html`, `/blog/2024/summary.html` |
| **P1** — exact vs pattern + clear | Template A: `exact` `/courses.html` · Template B: `pattern` `/courses` | `/courses.html`, `/courses/list.html` |

If your crawler stores paths **without** `.html`, normalize matchers accordingly (or align crawler settings) so `TemplateMatcher` sees the same strings as `website_pages.uri`.

## Document fixtures

Binary samples under `fixtures/` are small generated files (minimal PDF without tags, Word Open XML without proper headings/metadata, Excel without explicit table/header semantics, legacy Word HTML as `.doc`). Use them only for testing.

## Local preview

With Ruby and Bundler:

```bash
bundle install
bundle exec jekyll serve
```

Then open `http://127.0.0.1:4000/a11ychecker/` (path includes `baseurl` from `_config.yml`).

To preview the built site as static files only:

```bash
bundle exec jekyll build && python3 -m http.server 8080 --directory _site
```

## License

Use freely for testing and education. These patterns are **not** recommendations for production sites.
