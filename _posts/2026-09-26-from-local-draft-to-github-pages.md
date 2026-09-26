---
layout: post
date: 2026-09-26 12:00:00 +0300
title: "From Local Draft to GitHub Pages"
categories: [jekyll, workflow]
tags: [macos, jekyll, github-pages, git, writing]
description: "Preview an existing GitHub Pages blog on a Mac, keep unfinished drafts local, and publish approved articles with Git."
---

<img src="/assets/images/from-local-draft-to-github-pages/hero.webp" alt="Sticker illustration of an iPad and Apple Pencil beside a laptop, with a paper airplane carrying the article toward a globe." width="540" height="180" style="display: block; max-width: 100%; height: auto; margin: 0 auto 1.5rem;">

A blog can begin on a laptop: write an article, preview it in the actual website layout, and publish it only when it is ready. Jekyll and GitHub Pages provide a straightforward way to follow this workflow.

This guide explains how to prepare an existing blog repository for local previews, keep unfinished drafts on the computer, and publish selected articles through Git.

The [local setup guide]({% post_url 2026-07-12-mac-jekyll-local-setup-101 %}) covers the tools and how to create a separate local site. This time, the starting point is an existing GitHub Pages blog.

## One repository, two versions of the website

The same Markdown files can produce a preview on a laptop and the public website on GitHub Pages.

The local preview is available at `http://127.0.0.1:4000` while Jekyll is running. Saving a file rebuilds that preview. It does not update the public blog.

<style>
.blog-workflow { margin: 2rem 0; }
.blog-workflow .workflow-heading { margin-bottom: 1rem; font-size: 1.25rem; font-weight: 600; letter-spacing: -0.02em; }
.blog-workflow ol { display: grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap: 0.8rem; margin: 0; padding: 0; list-style: none; }
.blog-workflow li { position: relative; padding: 1rem; border: 1px solid #cddbd3; border-radius: 14px; background: #f3f7f4; }
.blog-workflow li:nth-child(n+4) { background: #f1f5fa; border-color: #cbd7e5; }
.blog-workflow .step-number { display: inline-flex; align-items: center; justify-content: center; width: 2rem; height: 2rem; margin-bottom: 0.85rem; border-radius: 50%; background: #dce9df; color: #294f3d; font-size: 0.8rem; font-weight: 700; }
.blog-workflow li:nth-child(n+4) .step-number { background: #dce6f2; color: #324f72; }
.blog-workflow .step-arrow { position: absolute; top: 1rem; right: 1rem; color: #536b60; font-size: 1.2rem; }
.blog-workflow strong { display: block; margin-bottom: 0.35rem; color: #263b33; font-size: 1rem; }
.blog-workflow .step-detail { display: block; color: #46544e; font-size: 0.9rem; line-height: 1.5; }
.blog-workflow .workflow-note { margin: 0.85rem 0 0; color: #526058; font-size: 0.85rem; }
@media (max-width: 600px) {
  .blog-workflow ol { grid-template-columns: 1fr; gap: 0.6rem; }
  .blog-workflow li { padding: 0.85rem 2.5rem 0.85rem 4rem; min-height: 3rem; }
  .blog-workflow .step-number { position: absolute; top: 0.85rem; left: 1rem; margin: 0; }
  .blog-workflow .step-arrow { transform: rotate(90deg); }
}
</style>

<section class="blog-workflow" aria-labelledby="workflow-heading">
  <h3 id="workflow-heading" class="workflow-heading">From first draft to live post</h3>
  <ol role="list">
    <li><span class="step-number" aria-hidden="true">01</span><span class="step-arrow" aria-hidden="true">→</span><strong>Write</strong><span class="step-detail">Start with a local draft.</span></li>
    <li><span class="step-number" aria-hidden="true">02</span><span class="step-arrow" aria-hidden="true">→</span><strong>Preview</strong><span class="step-detail">See it in the browser.</span></li>
    <li><span class="step-number" aria-hidden="true">03</span><span class="step-arrow" aria-hidden="true">↻</span><strong>Refine</strong><span class="step-detail">Edit and check again until ready.</span></li>
    <li><span class="step-number" aria-hidden="true">04</span><span class="step-arrow" aria-hidden="true">→</span><strong>Prepare</strong><span class="step-detail">Prepare the post and its final images.</span></li>
    <li><span class="step-number" aria-hidden="true">05</span><span class="step-arrow" aria-hidden="true">→</span><strong>Publish</strong><span class="step-detail">Review, commit, and push.</span></li>
    <li><span class="step-number" aria-hidden="true">06</span><strong>Verify</strong><span class="step-detail">Check the GitHub Pages deployment and live page.</span></li>
  </ol>
  <p class="workflow-note">Repeat the preview-and-edit loop as often as needed. Pushing to the publishing branch starts deployment.</p>
</section>

There are three separate actions to remember:

| Action | What changes |
|---|---|
| Save a file | The working copy on the computer and, while Jekyll is running, the local preview |
| Commit | The local Git history |
| Push | The remote repository; pushing to the configured publishing branch triggers deployment |

## Prepare the existing blog

The following steps assume an Apple Silicon Mac with Homebrew and Apple Command Line Tools installed, plus a local copy of an existing GitHub Pages blog. The companion setup guide covers the prerequisites. A separate Ruby installation provides the development environment; this example uses Ruby 3.3, the series listed in the [GitHub Pages dependency table](https://pages.github.com/versions/) at the time of writing.

Install Ruby through Homebrew:

```bash
brew install ruby@3.3
```

Add this line to `~/.zshrc`:

```bash
export PATH="/opt/homebrew/opt/ruby@3.3/bin:/opt/homebrew/lib/ruby/gems/3.3.0/bin:$PATH"
```

Reload the shell configuration, check the active Ruby, and install Bundler:

```bash
source ~/.zshrc
which ruby
ruby -v
gem install bundler
```

`which ruby` should point into `/opt/homebrew`, rather than `/usr/bin`. These paths are specific to this Homebrew setup; Intel Macs use a different prefix.

Inside the existing blog repository, create a `Gemfile`, or update its existing dependencies:

```ruby
source "https://rubygems.org"

gem "github-pages", "~> 232", group: :jekyll_plugins
gem "webrick"
```

The `github-pages` gem supplies the Pages-compatible Jekyll dependencies. `webrick` supplies the local HTTP server dependency. This example uses the Pages gem version listed at the time of setup; check the dependency table when repeating it later.

Enter the repository and install its dependencies. Replace `/path/to/blog` with the location of the blog folder:

```bash
cd /path/to/blog
bundle install
```

Bundler creates `Gemfile.lock`, recording the resolved versions. Keeping it with the project gives future local installs a consistent starting point. GitHub's managed build environment still determines the versions used by its branch-based Pages build.

There is no `jekyll new` step here: the blog already exists.

## Keep unfinished work local

Jekyll supports a [`_drafts` folder](https://jekyllrb.com/docs/posts/#drafts). Drafts have the same Markdown and front matter as posts, but do not need a date in their filenames.

A simple folder structure is:

```text
_drafts/
  example-post.md
_posts/
  YYYY-MM-DD-example-post.md
assets/
  drafts/
    example-post/
      hero-source.png
  images/
    example-post/
      hero.webp
```

Use one image folder per post, named after its slug. Keep filenames lowercase with hyphens: `hero.webp`, `setup-terminal.png`, or `ranking-pipeline.svg`. The draft folder holds originals and alternatives; the published folder holds only selected assets.

Add these entries to `.gitignore`:

```gitignore
.DS_Store
_site/
.jekyll-cache/
.jekyll-metadata
.sass-cache/
.bundle/
vendor/
_drafts/
assets/drafts/
```

**A Jekyll draft is not automatically private.** A normal build leaves drafts out of the website, but anyone can read them if their source files are pushed to a public repository. Ignoring the draft folders keeps new files out of normal Git staging. It does not untrack files already committed, and it can be bypassed with `git add -f`.

Create a draft image folder with `mkdir -p assets/drafts/example-post` and place the original image there. Reference it locally with:

```markdown
![Illustration of the blogging workflow](/assets/drafts/example-post/hero-source.png)
```

Git's ignore rules are not Jekyll build exclusions. Draft images can still be copied into the local `_site` output. This workflow publishes tracked source through GitHub Pages. The local `_site` folder is preview output and should not be uploaded as part of this workflow.

Because Git does not track these drafts, they also need a separate private backup, such as Time Machine.

## Write and preview

A draft starts with:

```markdown
---
layout: post
title: "Example Post"
---

Describe the project, its results, and the lessons learned.
```

From the repository folder, start the preview:

```bash
bundle exec jekyll serve --drafts --livereload --host 127.0.0.1
```

Then open `http://127.0.0.1:4000` in the browser.

- `--drafts` includes unfinished posts in the preview.
- `--livereload` refreshes the browser after changes.
- `--host 127.0.0.1` keeps the preview bound to this computer.

Keep the Terminal window running during the writing session. `Control+C` stops the server. Changes to `_config.yml` require a restart.

Check the rendered article: paragraphs, headings, code blocks, links, and images. Narrowing the browser window also helps reveal awkward tables or images before publishing.

## When an article is ready

The next step is to move the draft into `_posts` with the intended publication date:

```bash
mv _drafts/example-post.md _posts/YYYY-MM-DD-example-post.md
```

Replace `YYYY-MM-DD` with the publication date: a four-digit year, two-digit month, and two-digit day. Replace `example-post` with the article slug. Future-dated posts are normally excluded until their date arrives and the site is rebuilt.

### Prepare the final images

WebP is an image format, like PNG or JPEG, designed for efficient delivery on the web. It supports transparent backgrounds and both lossy and lossless compression. For illustrations, a WebP copy can often reduce download size while keeping the image visually close to the original. Modern major browsers support it. See the [WebP overview](https://developers.google.com/speed/webp).

Conversion creates a new file from the original; changing the filename extension alone does not convert an image. Keep the original in the draft folder and create a publication copy in the post's image folder.

On a Mac, install the converter once:

```bash
brew install webp
```

For an illustration intended to display at 540 pixels wide, a 1080-pixel-wide export provides twice the display resolution for sharper rendering on high-density screens. From the repository folder:

```bash
mkdir -p assets/images/example-post
cwebp -q 85 -resize 1080 0 \
  assets/drafts/example-post/hero-source.png \
  -o assets/images/example-post/hero.webp
```

The `-q 85` option is a starting quality setting, not a percentage of retained detail. `-resize 1080 0` sets the width and calculates the height to preserve the aspect ratio. Transparency is retained. Use a different width for other layouts, and avoid enlarging a smaller source image. The [cwebp documentation](https://developers.google.com/speed/webp/docs/cwebp) explains these options.

Compare file sizes and inspect the result in the local preview before accepting it:

```bash
ls -lh assets/drafts/example-post/hero-source.png assets/images/example-post/hero.webp
```

For screenshots or diagrams with fine text, PNG or lossless WebP may be a better choice. An existing SVG diagram can stay as SVG. WebP is an optimization option, not a requirement for publishing.

Update the article to reference the final asset. For a 3:1 illustration displayed at 540 × 180 pixels:

```html
<img src="/assets/images/example-post/hero.webp"
     alt="Illustration of the blogging workflow"
     width="540" height="180"
     style="max-width: 100%; height: auto;">
```

Set the dimensions and alternative text to match the actual image. Explicit dimensions reserve space while the image loads. Original images, rejected versions, and generation prompts stay in the ignored draft folder.

### Preview and publish together

Ordinary pages, such as an About page, can be edited locally and reviewed before being staged in the same way.

For a final check, stop the server and restart it without drafts:

```bash
bundle exec jekyll serve --livereload --host 127.0.0.1
```

Once the article looks right, stage the specific files in a second Terminal window:

```bash
git status --short
git add _posts/YYYY-MM-DD-example-post.md
git add assets/images/example-post/hero.webp
# Stage each additional approved image explicitly.
git diff --cached
git commit -m "Publish example post"
```

Before pushing, check **Settings → Pages** in the GitHub repository to confirm the publishing branch and folder. If the source is `main`, the publishing command is:

```bash
git push origin main
```

A push sends all unpushed commits on that branch, not just the latest article. Check the deployment in GitHub's **Actions** tab, then open the public page and verify it.

## The everyday routine

The installation is a one-time setup. Most writing sessions start with these commands, using the actual blog folder in place of `/path/to/blog`:

```bash
cd /path/to/blog
bundle exec jekyll serve --drafts --livereload --host 127.0.0.1
```

The local preview provides a place to refine each article in the real blog layout. Publishing remains a separate step, taken when the article is ready.
