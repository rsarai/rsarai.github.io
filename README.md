# rsarai.xyz

Personal blog and website of Rebeca Sarai, live at [https://rsarai.xyz](https://www.rsarai.xyz/).

Built with **Jekyll 4.4** and deployed via **GitHub Actions** to **GitHub Pages**. Based on the [Reverie](https://github.com/amitmerchant1990/reverie) theme.

---

## Prerequisites

You need **Ruby** and **Bundler** installed. Check with:

```bash
ruby --version
bundle --version
```

If Bundler is missing, install it:

```bash
gem install bundler
```

---

## Getting Started

### 1. Install dependencies

From the project root, run:

```bash
bundle install
```

This reads the `Gemfile` and installs all required gems (Jekyll, plugins, etc.).

### 2. Run the site locally

```bash
bundle exec jekyll serve
```

This will:
- Build the site into a `_site/` directory
- Start a local server at **http://localhost:4000**
- Watch for file changes and rebuild automatically

To also preview **draft** posts (files in `_drafts/`):

```bash
bundle exec jekyll serve --drafts
```

To enable **live reload** in the browser (auto-refresh on changes):

```bash
bundle exec jekyll serve --livereload
```

### 3. Build (without serving)

To generate the static site into `_site/` without starting a server:

```bash
bundle exec jekyll build
```

---

## Writing a New Blog Post

### Step-by-step

1. Create a new Markdown file inside `_posts/`
2. Name it using the format: **`YYYY-MM-DD-your-post-title.md`** (the date is required)
3. Add the front matter at the top of the file
4. Write your content in Markdown below the front matter

### Post front matter template

```yaml
---
layout: post
title: Your Post Title Here
categories: [category1, category2]
excerpt: A short description shown in the blog listing page
last_modified_at:
---

Your content goes here. Write in Markdown.
```

| Field              | Required | Description                                                       |
|--------------------|----------|-------------------------------------------------------------------|
| `layout`           | Yes      | Always use `post`                                                 |
| `title`            | Yes      | The title displayed on the page and blog listing                  |
| `categories`       | No       | Array of categories, e.g. `[software, open source]`               |
| `excerpt`          | No       | Short summary shown on the blog listing page                      |
| `last_modified_at` | No       | Date of last update; if set, shows "(Updated: ...)" on the post   |

### Example

```yaml
---
layout: post
title: The architecture of open source applications [Audacity]
categories: [software, open source]
excerpt: This post summarizes Chapter 2 of the book The architecture of open source applications - Vol I
last_modified_at:
---

Your post body in Markdown...
```

---

## Working with Drafts

Drafts are posts you're still working on. They live in the `_drafts/` folder and **do not** require a date in the filename.

```
_drafts/
  my-upcoming-post.md
```

Drafts are **not included** in the normal build. To preview them locally:

```bash
bundle exec jekyll serve --drafts
```

When the draft is ready, move the file to `_posts/` and add the date prefix to the filename:

```bash
mv _drafts/my-upcoming-post.md _posts/2026-02-14-my-upcoming-post.md
```

---

## Adding Images

1. Create a folder inside `images/` matching your post (convention used in this blog):

   ```
   images/2026-02-14-my-post-title/
   ```

2. Place your image files there

3. Reference them in your post with:

   ```html
   <img
     src="/images/2026-02-14-my-post-title/my-image.png"
     alt="Description of the image"
     title="Tooltip text"
   />
   ```

   Or using Markdown syntax:

   ```markdown
   ![Description](/images/2026-02-14-my-post-title/my-image.png)
   ```

---

## Creating a New Page

Pages (non-blog content like About, Ideas, Links) live in `_pages/`. To create one:

1. Add a Markdown file in `_pages/`, e.g. `_pages/my-page.md`
2. Use the `page` layout:

```yaml
---
layout: page
title: My Page
permalink: /my-page/
---

Page content here...
```

3. Optionally add a link to it in the sidebar navigation by editing `_layouts/default.html`

---

## Project Structure

```
.
├── .github/workflows/
│   └── jekyll.yml       # GitHub Actions deployment workflow
├── _config.yml          # Site configuration (name, URL, plugins, etc.)
├── _drafts/             # Unpublished draft posts (no date in filename)
├── _includes/           # Reusable HTML partials (analytics, disqus, icons)
├── _layouts/            # Page templates (default, post, page)
├── _pages/              # Standalone pages (about, books, ideas, links, etc.)
├── _posts/              # Published blog posts (YYYY-MM-DD-title.md)
├── _sass/               # SCSS partials (variables, highlights, layout)
├── assets/
│   └── style.scss       # Main stylesheet (imports _sass partials)
├── blog/
│   └── index.html       # Blog listing page with pagination
├── fonts/               # Custom fonts
├── images/              # Post images, organized by post name
├── index.html           # Homepage
├── search.json          # JSON feed for search functionality
├── 404.md               # Custom 404 page
├── CNAME                # Custom domain: www.rsarai.xyz
├── Gemfile              # Ruby dependencies
├── Gemfile.lock         # Locked dependency versions
└── README.md            # This file
```

---

## Configuration

All site settings are in `_config.yml`. Key settings:

| Setting             | Value / Description                                    |
|---------------------|--------------------------------------------------------|
| `name`              | `Rebeca Sarai`                                         |
| `url`               | `https://rsarai.xyz`                                   |
| `permalink`         | `/:title/` (clean URLs based on post title)            |
| `paginate`          | `50` (posts per page on the blog listing)              |
| `paginate_path`     | `/blog/page:num/`                                      |
| `kramdown`          | GitHub Flavored Markdown with Rouge syntax highlighting|
| `google_analytics`  | `UA-158115790-1`                                       |

**Important:** Changes to `_config.yml` require restarting the Jekyll server (Ctrl+C and re-run `bundle exec jekyll serve`).

---

## Styling

- Main stylesheet: `assets/style.scss` (imports all partials)
- Variables (colors, fonts, breakpoints): `_sass/_variables.scss`
- Syntax highlighting: `_sass/_darcula.scss`
- Homepage styles: `_sass/_home.scss`
- Icon styles: `_sass/_svg-icons.scss`

---

## Deploying

This blog is deployed via **GitHub Actions** to **GitHub Pages**. The workflow file lives at `.github/workflows/jekyll.yml`.

**How it works:**

1. Write or edit content locally
2. Preview it with `bundle exec jekyll serve`
3. Commit and push to the `master` branch:

   ```bash
   git add .
   git commit -m "Add new post: your post title"
   git push origin master
   ```

4. GitHub Actions automatically builds (with Jekyll 4) and deploys the site to [https://rsarai.xyz](https://rsarai.xyz)

The custom domain `www.rsarai.xyz` is configured via the `CNAME` file in the repo root.

**One-time setup (already done if you're reading this):**

In your GitHub repository, go to **Settings > Pages > Source** and select **GitHub Actions** (instead of "Deploy from a branch").

---

## Quick Reference

| Task                              | Command                                        |
|-----------------------------------|-------------------------------------------------|
| Install dependencies              | `bundle install`                                |
| Run locally                       | `bundle exec jekyll serve`                      |
| Run with drafts                   | `bundle exec jekyll serve --drafts`             |
| Run with live reload              | `bundle exec jekyll serve --livereload`          |
| Build only (no server)            | `bundle exec jekyll build`                      |
| Create a new post                 | Add `_posts/YYYY-MM-DD-title.md` with front matter |
| Create a draft                    | Add `_drafts/title.md` with front matter        |
| Publish a draft                   | Move from `_drafts/` to `_posts/` with date prefix |
| Deploy                            | `git push origin master`                        |

---

## Credits

Theme based on [Reverie](https://github.com/amitmerchant1990/reverie) by Amit Merchant.
