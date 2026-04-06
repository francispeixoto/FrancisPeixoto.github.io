# AGENTS.md

## Site Overview
- Personal portfolio/ résumé site built with Jekyll
- Deployed via GitHub Pages from the `main` branch
- Custom domain: `francISpeixoto.com` (see `CNAME`)

## Commands
- **Preview locally**: `bundle exec jekyll serve` (requires Ruby + Bundler)
- **Build**: `bundle exec jekyll build`
- **Deploy**: Push to `main` — GitHub Pages builds automatically

## Key Files
- `README.md` — Main content (French)
- `_config.yml` — Jekyll config (theme: `pages-themes/tactile@v0.2.0`)
- `CNAME` — Custom domain

## Notes
- This is a static site; no tests or linting needed
- Theme is loaded remotely via `jekyll-remote-theme` plugin
- Edit `README.md` to update portfolio content
- `DEVELOPMENT.md` — Full developer guide (excluded from build)