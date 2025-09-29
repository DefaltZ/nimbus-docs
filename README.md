## Nimbus e‑resources

This repository contains the source for the Nimbus e‑resources site, built with MkDocs and the Material theme. It serves as an internal documentation and content hub. There is no installation guide here by design; the focus is on how to work with content, structure, theming, and deployment within this workspace.

### At a glance

- **Site generator**: MkDocs with Material theme
- **Theme overrides**: `overrides/` (Jinja2 templates) and `docs/stylesheets/extra.css`
- **Content root**: `docs/`
- **Navigation**: defined in `mkdocs.yml`
- **Plugins**: `mkdocs-video`
- **CI/CD**: GitHub Actions deploys to GitHub Pages on push to `master`/`main`

---

## Repository layout

```
docs/
  index.md                    # Home page
  about/
    Nimbus.md
    announcements.md
  resources/
    articles/
      -
      - ...
    guides/
      - ...
    videos/
      videos.md
      extras.md
    MUN/
      - ...
  sponsors/
    sponsors.md
  assets/                     # Images and media
  stylesheets/
    extra.css                 # Site-specific CSS

overrides/                    # Theme template overrides (Material custom_dir)
  main.html                   # Extends/overrides base theme blocks
  partials/
    page-announcements.html   # Optional announcements partial

mkdocs.yml                    # Site configuration (theme, nav, plugins, extras)
.github/workflows/ci.yml      # GitHub Actions workflow for deployment
```

## How content is organized

The navigation menu is declared in `mkdocs.yml` under `nav:`. Pages listed there determine the sidebar/top‑nav order and hierarchy.

- **Add a page**: create a Markdown file under `docs/` and reference it in `mkdocs.yml` `nav:`.
- **Group content**: organize related pages in subfolders (e.g., `docs/resources/articles/`). Use clear, concise filenames.
- **Assets**: place images and media in `docs/assets/` and reference them with relative paths, e.g. `![Alt text](../assets/logo.png)`.

## Writing guidelines

- **Headings**: Start each page with a single H1 that matches the nav title. Use sentence case for headings.
- **Tone**: Clear, concise, and instructional. Prefer examples over prose when possible.
- **Admonitions**: Material supports admonitions for callouts like notes, tips, etc.

```markdown
!!! note "Sources"
    Primary references are linked at the end of each article.
```

- **Details/expanders**: For optional sections.

```markdown
???+ info "Background"
    Additional context for interested readers.
```

- **Code fences and superfences**: Use triple backticks with language tags when applicable.

### Videos

The `mkdocs-video` plugin enables embedding from common platforms (e.g., YouTube, Vimeo). Linking to supported video URLs in content will render embedded players. Keep links on their own line for clarity, and provide a brief caption where useful.

## Theming and customization

Theme configuration in `mkdocs.yml`:

- **Theme**: Material (`theme.name: material`), with a custom palette and `logo` at `docs/assets/logo.png`.
- **Features**: Tabs and sticky tab navigation are enabled.
- **Custom directory**: `overrides/` provides Jinja2 template overrides (e.g., `main.html`, partials under `overrides/partials/`).
- **Extra CSS**: `docs/stylesheets/extra.css` for site‑specific styling.

When editing templates, prefer extending base blocks rather than wholesale replacements. Keep overrides minimal and documented at the top of each file.

## Local preview (no installation steps required)

This repository includes a checked‑in virtual environment with MkDocs tooling available under `bin/`. You can run common tasks directly:

```bash
./bin/mkdocs serve
```

This starts a local preview server with live reload. By default it serves at `http://127.0.0.1:8000/`.

Other useful commands:

```bash
./bin/mkdocs build           # Build the static site into the 'site/' directory
./bin/mkdocs gh-deploy --force  # Manually deploy to GitHub Pages (rarely needed)
```

## CI/CD and deployment

GitHub Actions (`.github/workflows/ci.yml`) builds and deploys the site to GitHub Pages on every push to `master` or `main`:

- Checks out the repo and sets up Python
- Caches dependencies for faster builds
- Installs `mkdocs-material` and `mkdocs-video`
- Runs `mkdocs gh-deploy --force`

To trigger a deploy, merge your content changes to the default branch and push.

## Configuration reference

Key parts of `mkdocs.yml` you may need to touch:

- `site_name`: Display name in the header
- `theme`: Material configuration, palette, features, and `custom_dir: overrides`
- `nav`: Structure and order of pages
- `extra_css`: Additional stylesheets (e.g., `stylesheets/extra.css`)
- `plugins`: Currently `mkdocs-video`
- `markdown_extensions`: Admonitions, details/expanders, superfences, and attribute lists are enabled

## Conventions for contributions

- Keep PRs focused: one topic or article per pull request.
- Use meaningful commit messages describing the content change.
- Link sources and references at the end of articles when applicable.
- Run a local preview before pushing to ensure formatting and links render correctly.

---

© 2025 Priyongshu Paul. Content licensed to the organization for internal use unless otherwise noted.


