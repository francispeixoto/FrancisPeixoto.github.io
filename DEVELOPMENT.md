# Developer Guide — FrancisPeixoto.github.io

A comprehensive guide for local development, Jekyll configuration, and GitHub Pages best practices.

---

## Table of Contents

1. [Local Development Setup](#local-development-setup)
2. [Configuration Reference](#configuration-reference)
3. [GitHub Pages Best Practices](#github-pages-best-practices)
4. [Customization Guide](#customization-guide)
5. [Troubleshooting](#troubleshooting)

---

## Local Development Setup

### Prerequisites

| Tool | Version | Notes |
|------|---------|-------|
| **Ruby** | ≥ 2.7 | Comes with macOS/Linux. Use [rbenv](https://github.com/rbenv/rbenv) or [rvm](https://rvm.io/) to manage. |
| **Bundler** | ≥ 2.0 | Run `gem install bundler` |
| **Jekyll** | 4.x | Installed via Gemfile |

### Initial Setup

1. **Create a Gemfile** in the repository root:

   ```ruby
   source "https://rubygems.org"
   
   gem "jekyll", "~> 4.4"
   gem "jekyll-remote-theme"
   gem "github-pages", "~> 231"
   ```

2. **Install dependencies**:

   ```bash
   bundle install
   ```

### Development Commands

| Command | Purpose |
|---------|---------|
| `bundle exec jekyll serve` | Start local dev server at `http://localhost:4000` |
| `bundle exec jekyll serve --livereload` | Auto-refresh on file changes |
| `bundle exec jekyll build` | Build static site to `_site/` |
| `bundle exec jekyll clean` | Clear cache and build output |

---

## Configuration Reference

### _config.yml Options

```yaml
# Required
title: "Your Site Title"
description: "Your site description for SEO"
remote_theme: "pages-themes/tactile@v0.2.0"

# Optional — commonly used
url: "https://example.com"           # Production URL
baseurl: "/subdirectory"            # Subdirectory (empty for root)
timezone: "America/New_York"        # IANA timezone
encoding: "utf-8"                   # File encoding

# Files to exclude from build
exclude:
  - DEVELOPMENT.md
  - "*.md"                          # Exclude all markdown files
  - Gemfile
  - Gemfile.lock

# Plugins (GitHub Pages whitelisted only)
plugins:
  - jekyll-remote-theme
  - jekyll-seo-tag
  - jekyll-sitemap
  - jekyll-feed

# Default front matter for pages/posts
defaults:
  - scope:
      path: ""
    values:
      layout: default

# Build options
future: false        # Don't publish future-dated posts
show_drafts: false    # Don't show draft posts
quiet: false         # Verbose output
```

### All Configuration Options

| Setting | Description | Example |
|---------|-------------|---------|
| `title` | Site title | `"Francis Peixoto"` |
| `description` | Site description for SEO | `"Digital Strategy & Tech Leadership"` |
| `url` | Production domain | `"https://francISpeixoto.com"` |
| `baseurl` | Subdirectory path | `"/portfolio"` or `""` |
| `remote_theme` | GitHub-hosted theme | `"pages-themes/tactile@v0.2.0"` |
| `theme` | Supported built-in theme | `"jekyll-theme-minimal"` |
| `plugins` | Enabled plugins (whitelist only) | `[jekyll-seo-tag, jekyll-sitemap]` |
| `exclude` | Files to skip | `["README.md", "DEVELOPMENT.md"]` |
| `include` | Force-include files | `[".htaccess"]` |
| `timezone` | IANA timezone | `"America/New_York"` |
| `encoding` | File encoding | `"utf-8"` |
| `keep_files` | Files to preserve on rebuild | `["CNAME"]` |
| `permalink` | Post URL format | `/blog/:title/` |
| `future` | Publish future posts | `false` |
| `show_drafts` | Show draft posts | `false` |
| `limit_posts` | Max posts to publish | `4` |

---

## GitHub Pages Best Practices

### Supported Built-in Themes

GitHub Pages supports 14 themes out of the box:

| Theme | Config Value |
|-------|--------------|
| Architect | `jekyll-theme-architect` |
| Cayman | `jekyll-theme-cayman` |
| Dinky | `jekyll-theme-dinky` |
| Hacker | `jekyll-theme-hacker` |
| Leap Day | `jekyll-theme-leap-day` |
| Merlot | `jekyll-theme-merlot` |
| Midnight | `jekyll-theme-midnight |
| Minima | `jekyll/minima` |
| Minimal | `jekyll-theme-minimal` |
| Modernist | `jekyll-theme-modernist` |
| Slate | `jekyll-theme-slate` |
| Tactile | `jekyll-theme-tactile` |
| Time Machine | `jekyll-theme-time-machine` |

**Usage**: Set `theme: THEME-NAME` in `_config.yml`

### Remote Themes (Any GitHub Theme)

Use `remote_theme` to load any Jekyll theme hosted on GitHub:

```yaml
remote_theme: "pages-themes/tactile@v0.2.0"
```

Requires `jekyll-remote-theme` plugin.

### Allowed Plugins (GitHub Pages Whitelist)

These 20 plugins are pre-installed and enabled automatically:

| Plugin | Purpose |
|--------|---------|
| `jekyll-coffeescript` | Compile CoffeeScript |
| `jekyll-commonmark-ghpages` | Markdown processor |
| `jekyll-feed` | RSS/Atom feeds |
| `jekyll-gist` | Embed GitHub Gists |
| `jekyll-github-metadata` | Repository metadata |
| `jekyll-paginate` | Pagination |
| `jekyll-redirect-from` | Redirect support |
| `jekyll-seo-tag` | SEO metadata |
| `jekyll-sitemap` | XML sitemap |
| `jekyll-avatar` | GitHub user avatars |
| `jemoji` | GitHub-flavored emoji |
| `jekyll-mentions` | @mention support |
| `jekyll-relative-links` | Relative link processing |
| `jekyll-optional-front-matter` | Optional front matter |
| `jekyll-readme-index` | README as index |
| `jekyll-default-layout` | Default layouts |
| `jekyll-titles-from-headings` | Generate titles |
| `jekyll-include-cache` | Cached includes |
| `jekyll-octicons` | GitHub octicons |
| `jekyll-remote-theme` | Remote themes |

**Note**: Custom plugins are NOT supported on GitHub Pages unless using GitHub Actions.

### Deployment Workflow

1. **Push to `main` branch**:
   ```bash
   git add .
   git commit -m "Update site"
   git push origin main
   ```

2. **GitHub Pages builds automatically**:
   - Go to Settings → Pages
   - Source: `main` branch (or `/docs` folder)
   - Custom domain configured in `CNAME`

3. **Build time**: 1-3 minutes typical

### Custom Domain Setup

1. Create `CNAME` file with your domain:
   ```
   francISpeixoto.com
   ```

2. Configure in GitHub Pages Settings:
   - Custom domain: `francISpeixoto.com`
   - Enforce HTTPS (automatic after DNS propagates)

3. **DNS**: Point `A` records to GitHub IPs or use `ALIAS` record for apex domains.

---

## Customization Guide

### Custom CSS

Create `/assets/css/style.scss`:

```scss
---
---

@import "{{ site.theme }}";

/* Your custom styles here */
.my-custom-class {
  color: #333;
  font-family: "Helvetica Neue", sans-serif;
}
```

### Custom Layouts

Create `/_layouts/default.html` to override theme:

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>{{ page.title }}</title>
  <link rel="stylesheet" href="{{ "/assets/css/style.css" | relative_url }}">
</head>
<body>
  <header>
    <nav>
      <a href="/">Home</a>
      <a href="/about">About</a>
    </nav>
  </header>
  
  <main>
    {{ content }}
  </main>
  
  <footer>
    &copy; 2024 Your Name
  </footer>
</body>
</html>
```

### Adding Pages

Create any `.md` or `.html` file in the root:

```markdown
---
layout: default
title: About Me
---

Your content here.
```

### Adding Posts

Create files in `/_posts/` with format `YYYY-MM-DD-title.md`:

```markdown
---
layout: post
title: "My First Post"
date: 2024-01-01
categories: blog
---

Post content goes here.
```

---

## Troubleshooting

### Common Issues

| Issue | Solution |
|-------|----------|
| **Build fails on GitHub** | Check Gemfile matches GitHub Pages gem version |
| **Theme not loading** | Verify `remote_theme` format: `owner/repo@vX.X.X` |
| **404 on custom domain** | Ensure CNAME file exists and DNS propagates |
| **Plugin not working** | Confirm plugin is in the allowed whitelist |
| **CSS not applied** | Create `/assets/css/style.scss` with proper front matter |

### Debug Commands

```bash
# Check Jekyll version
jekyll --version

# Verbose build output
bundle exec jekyll build --verbose

# Show configuration
bundle exec jekyll config

# Validate front matter
bundle exec jekyll doctor
```

### Useful Links

- [Jekyll Docs](https://jekyllrb.com/docs/)
- [GitHub Pages Docs](https://docs.github.com/en/pages)
- [Jekyll Themes on GitHub](https://github.com/topics/jekyll-theme)
- [pages-gem Repository](https://github.com/github/pages-gem)

---

*Last updated: 2026-04-06*