# a11ychecker — accessibility test fixtures

This repository contains a small **static site** in the `docs/` folder: HTML pages with **intentional accessibility issues**, plus an index that lists them. Use them to exercise accessibility checkers, browser extensions, or manual audits.

## GitHub Pages

1. Push this repository to GitHub.
2. Open the repository **Settings → Pages**.
3. Under **Build and deployment**, set **Source** to **Deploy from a branch**.
4. Choose branch **main** (or your default branch) and folder **`/docs`**, then save.

The site will be available at `https://<username>.github.io/<repo>/` (or your custom domain). The home page is `index.html` in `docs/`.

## Test pages

| Page | File | Issues (summary) |
|------|------|------------------|
| 01 | `docs/01-missing-image-alt.html` | Missing `alt`, decorative image with misleading `alt` |
| 02 | `docs/02-low-contrast.html` | Text and links with insufficient contrast |
| 03 | `docs/03-unlabeled-inputs.html` | Inputs/select/textarea without labels; checkbox without proper association |
| 04 | `docs/04-heading-skips.html` | Skipped heading levels; visual “heading” as plain paragraph |
| 05 | `docs/05-vague-links.html` | “Click here”, “read more”, empty link, image link with empty `alt` |
| 06 | `docs/06-no-html-lang.html` | No `lang` on `<html>` |
| 07 | `docs/07-duplicate-ids.html` | Duplicate `id` values |
| 08 | `docs/08-focus-and-aria.html` | `tabindex` misuse, `aria-hidden` on focusable descendant, positive `tabindex` |
| 09 | `docs/09-table-without-headers.html` | Data table using only `<td>`, no `<th>` |
| 10 | `docs/10-nonsemantic-button.html` | Non-interactive element styled as button; vague link |
| 11 | `docs/11-video-youtube.html` | Real YouTube watch/short/embed URLs; oEmbed API links; iframes without `title` |
| 12 | `docs/12-document-links.html` | Links to PDF / `.doc` / `.docx` / `.xlsx` fixtures in `docs/fixtures/` (intentionally poor document accessibility) |

The **index** (`docs/index.html`) is meant to be navigable and is not part of the “broken” set.

## Document fixtures

Binary samples under `docs/fixtures/` are small generated files (minimal PDF without tags, Word Open XML without proper headings/metadata, Excel without explicit table/header semantics, legacy Word HTML as `.doc`). Use them only for testing.

## Local preview

From the repository root:

```bash
cd docs && python3 -m http.server 8080
```

Then open `http://127.0.0.1:8080/`.

## License

Use freely for testing and education. These patterns are **not** recommendations for production sites.
