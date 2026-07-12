---
layout: post
title: "Mac and Jekyll Local Setup 101"
date: 2026-07-12 12:00:00 +0300
categories: jekyll setup
tags: macos homebrew ruby bundler
---

My public blog lives on GitHub Pages, but not every note belongs on the internet. This guide prepares an Apple Silicon Mac to run a completely private Jekyll site — no GitHub, no remote repository, no hosting. Just Markdown files that become a website on `localhost`.

Truth be told, an AI agent could run this entire setup for you in a few minutes. But if you would rather get your hands dirty and actually understand what lands on your machine — read on.

![Editorial sticker flow showing Apple developer tools, Homebrew, Ruby, RubyGems, Bundler, and Jekyll leading to a private website on localhost](/assets/images/mac-jekyll-local-setup-101/setup-flow.png)

*The complete local toolchain: Apple developer tools support Homebrew, Homebrew installs Ruby, RubyGems installs Jekyll, Bundler pins its dependencies, and Jekyll serves the site at `localhost:4000`.*

## The mental model

Six tools stack on top of each other. Each one has a familiar equivalent:

| Tool | What it does | Think of it as |
|------|--------------|----------------|
| **Apple developer tools** | Provide compilers, `git`, and build tools through Xcode or Command Line Tools | The workshop everything else is built in |
| **Homebrew** | Installs command-line software on macOS | An app store for the terminal |
| **Ruby** | The language Jekyll is written in | The engine |
| **RubyGems** (`gem`) | Installs Ruby packages | `pip`, but for Ruby |
| **Bundler** | Resolves and pins a project's dependency versions | `requirements.txt` with exact versions, but for Ruby |
| **Jekyll** | Turns Markdown files into a static website | The actual site generator |

The chain is short: Apple's developer tools provide the build foundation, Homebrew installs Ruby, RubyGems installs Jekyll, Bundler keeps its dependencies consistent, and Jekyll builds and serves the site.

## 1. Install Apple developer tools

Everything in this guide depends on Apple's developer tooling being present first. Why? Two reasons:

- **Compilers.** Homebrew sometimes builds software from source code, and several of Jekyll's dependencies are gems with native C extensions that must be compiled during installation. No compiler, no install.
- **Git.** The tools provide Apple's supported `git` command for common development workflows.

Apple ships this tooling in two forms:

| | Full Xcode | Command Line Tools |
|---|---|---|
| **Contains** | Full IDE, iOS/macOS simulators, app signing, SDKs — plus everything on the right | Compilers (`clang`), `git`, `make`, system headers |
| **Good for** | Building Mac and iOS apps, and any terminal workflow | Terminal workflows only |

My choice is the full Xcode, installed from the App Store. It is a larger download, but it includes everything the Command Line Tools provide and keeps the door open for building native Mac and iOS apps later. After installing, open Xcode once so it can finish setting up and accept the license.

If the full IDE is not appealing, the lighter alternative is the Command Line Tools alone:

```bash
xcode-select --install
```

macOS opens a dialog, downloads the tools, and installs them. If the tools are already present, the command simply says so — running it twice does no harm. (The Homebrew installer in the next step also offers to install them automatically if they are missing.)

## 2. Install Homebrew

### What is Homebrew, and why have it?

On a Mac, graphical apps come from the App Store or a downloaded installer. But most developer tools — programming languages, databases, command-line utilities — are not in the App Store at all. Without help, installing them means visiting each project's website, finding the right download, and repeating the whole hunt every time an update comes out.

Homebrew is a **package manager**: one program whose job is to install, update, and remove other programs. Instead of searching the web, you ask Homebrew:

```bash
brew install ruby     # install something
brew upgrade          # update everything it installed
brew uninstall ruby   # remove it cleanly
```

Three things make it worth having:

- **One command instead of a treasure hunt.** Homebrew knows where thousands of tools live and fetches them from a trusted, community-maintained catalog.
- **Dependencies come along automatically.** If a tool needs three other libraries to work, Homebrew installs those too — you never see the problem.
- **Everything stays in one place.** Homebrew keeps what it installs under its own prefix, separate from macOS-managed software. This makes tools easier to update or remove without modifying the system-provided copies.

Nearly every Mac developer setup guide starts with Homebrew for exactly these reasons. This one is no different: Ruby, the language Jekyll runs on, will arrive through it.

### Installing it

Homebrew has an official installation script:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

On Apple Silicon, Homebrew lives under `/opt/homebrew`. The shell does not know about it yet, so three commands wire it up:

```bash
echo >> ~/.zprofile
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```

Line by line:

1. Makes sure `.zprofile` exists and ends with a newline.
2. Saves Homebrew's environment settings for every future terminal session.
3. Activates the same settings in the current session, so there is no need to open a new terminal.

Homebrew collects anonymous usage analytics by default. One command turns that off:

```bash
brew analytics off
```

## 3. Install Ruby

### What is Ruby, and why is it needed here?

Ruby is a general-purpose programming language, in the same family as Python: readable, friendly, and popular for building tools and web applications. It matters for this guide for one simple reason — **Jekyll is a program written in Ruby**. Just as running a Python script requires Python on the machine, running Jekyll requires Ruby.

That is the entire relationship. Building a Jekyll blog never requires *writing* a line of Ruby — the language sits quietly underneath, running Jekyll on your behalf. It also brings along its package installer, RubyGems (the `gem` command), which is how Jekyll itself will be installed in the next step — the same role `pip` plays for Python.

### Why not the system Ruby?

macOS includes a system-managed Ruby on many versions, but it is not intended as a development environment. Installing gems into it can cause permission problems, and a macOS update can change it underneath you. A separate Ruby stays out of the system's way:

```bash
brew install ruby
echo 'export PATH="/opt/homebrew/opt/ruby/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

`PATH` is the ordered list of directories the shell searches when you type a command. Putting Homebrew Ruby at the front means the shell finds it *before* the system Ruby — the system copy is still there, just never picked.

This guide uses Homebrew's current Ruby because it is a simple fit for one local setup. [Jekyll's official macOS guide](https://jekyllrb.com/docs/installation/macos/) recommends a Ruby version manager such as `chruby`, which is the better option when projects require different Ruby versions. A future `brew upgrade` may move Ruby to a new gem directory; if `jekyll` then disappears, reinstall Bundler and Jekyll with `gem install bundler jekyll`.

Verify which Ruby is now active:

```bash
which ruby
ruby -v
which gem
```

Expect output along these lines:

```text
/opt/homebrew/opt/ruby/bin/ruby
ruby 4.x.x (...) [arm64-darwin...]
/opt/homebrew/opt/ruby/bin/gem
```

The exact version number will vary — what matters is that both paths start with `/opt/homebrew`. That confirms the shell is picking up the Homebrew Ruby, not the system one. If a path starts with `/usr/bin` instead, the system Ruby is still winning: open a new terminal window, or re-check that the `PATH` line made it into `~/.zshrc`.

## 4. Install Bundler and Jekyll

### Gems, Bundler, Jekyll — what is what?

A **gem** is a package of Ruby code that someone wrote and shared, ready to be installed with one command. Python calls these packages and installs them with `pip`; Ruby calls them gems and installs them with `gem`. Anything from a tiny helper library to a complete application can be a gem.

The two gems this guide needs are complete applications:

- **Jekyll** is the star of the show — the static site generator itself. It reads Markdown files, wraps them in templates, and produces plain HTML pages. "Static" means the published result needs no application server or database, leaving fewer runtime components to maintain.
- **Bundler** solves a quieter problem: version drift. Jekyll depends on dozens of other gems, and each of those has versions of its own. Bundler records the resolved versions in `Gemfile.lock`, helping compatible environments use a consistent dependency set.

In short: `gem` fetches the tools, Jekyll builds the site, Bundler makes sure the build is repeatable.

### Installing them

```bash
gem install bundler
gem install jekyll
```

There is one catch. Gems that provide commands (like `jekyll`) install their executables into a separate directory, and that directory is not on `PATH` yet. RubyGems can report its full environment:

```bash
gem env
```

This prints a list of settings. The line to look for is `EXECUTABLE DIRECTORY`:

```text
  - EXECUTABLE DIRECTORY: /opt/homebrew/lib/ruby/gems/4.x.x/bin
```

The version segment tracks the installed Ruby's series; the important part is that this is the directory about to go on `PATH`.

Add it to `PATH` the same way as before:

```bash
echo 'export PATH="$(gem env home)/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

Why `$(gem env home)/bin` and not the path typed out? `gem env home` prints one thing: the gem home directory — the `EXECUTABLE DIRECTORY` above is simply its `bin` subfolder. The `$(...)` wrapper runs that command and substitutes its output in place, so the line always resolves to the right directory, even after a Ruby upgrade changes the version segment.

Now the `jekyll` command works anywhere:

```bash
jekyll -v
```

## 5. Create the site

Create a new site and enter its directory:

```bash
jekyll new private-knowledge-base
cd private-knowledge-base
```

`jekyll new` creates the named directory and scaffolds the site inside it. This is safer than using `--force`, which can overwrite matching files in a non-empty directory. To use an existing empty directory instead, enter it and run `jekyll new .`.

### What just got created

The command scaffolds a small, complete website. A tour of the pieces:

| File / folder | Role |
|---|---|
| `_config.yml` | The site's settings: title, description, theme. Read once at startup. |
| `Gemfile` and `Gemfile.lock` | The dependency list and the exact locked versions — Bundler's territory. |
| `_posts/` | The heart of the site. Every Markdown file here becomes a blog post. |
| `index.markdown` | The home page, which lists the posts. |
| `about.markdown` | An example standalone page. |
| `404.html` | The "page not found" page. |

`_posts` deserves a closer look, because it has two conventions that trip up newcomers:

- **The filename carries the date.** Posts must be named `YYYY-MM-DD-some-title.markdown`. Jekyll reads the date from the filename and uses it to order the posts — a file that does not match this pattern silently does not appear.
- **Every post starts with front matter.** The block between two `---` lines at the top of the file holds the post's metadata — title, date, categories — in YAML. Jekyll reads it, strips it, and renders only the Markdown below it.

Jekyll also generates a sample post inside `_posts`, which doubles as a template: copy it, rename it with today's date, and start writing.

### Install the project's dependencies

The `Gemfile` created above declares the project's dependencies — the default theme (`minima`) and a few plugins. `jekyll new` normally asks Bundler to install them automatically. The following command is useful for verifying the installation, recovering from an interrupted setup, or applying later `Gemfile` changes:

```bash
bundle install
```

This reads the `Gemfile`, fetches the required gems, and records the resolved versions in `Gemfile.lock`. If setup was interrupted, an error such as `Could not find gem 'minima' in locally installed gems` is usually resolved by running `bundle install` again.

## 6. Run the website

Start the local development server:

```bash
bundle exec jekyll serve --livereload
```

### What this command actually does

Three things happen, in order:

1. **Build.** Jekyll reads `_config.yml`, converts every file in `_posts` to HTML, applies the theme's layout and styling, and writes the finished pages into a `_site` folder. That folder *is* the website — plain HTML and CSS. It is entirely generated, safe to delete, and rebuilt on every run, so it is never edited by hand.
2. **Serve.** A small web server starts and hands out the files in `_site` to any browser that asks.
3. **Watch.** Jekyll keeps monitoring the project. Save any file, and the affected pages are rebuilt automatically — usually in a fraction of a second.

The command around it, piece by piece:

- `bundle exec` runs Jekyll with the dependency versions selected by the project's bundle instead of whichever compatible gems happen to be available globally. It is a good habit even when it seems unnecessary — it makes builds boring and predictable.
- `--livereload` closes the loop on the watch step: after each rebuild, the browser tab refreshes itself. Without the flag the rebuild still happens, but seeing it requires a manual refresh.

### Where the site lives

The terminal output ends with a line like `Server address: http://127.0.0.1:4000/`, and the site appears at:

```text
http://localhost:4000
```

Two parts of that address are worth decoding:

- `localhost` always means "this computer." With Jekyll's default host setting, the site is accessible only from the Mac and exists only while the server runs. It is not published to the internet.
- `4000` is the port — one of thousands of numbered channels a computer uses to keep network programs from talking over each other. Jekyll picks 4000 by default; it has no special meaning beyond being Jekyll's habit.

To stop the server, return to the terminal where it is running and press `Control + C`. The terminal comes back to a prompt, the site goes dark, and `_site` stays on disk until the next run rebuilds it.

## Supplementary: the everyday commands

Steps 1–4 prepare the machine for normal day-to-day use. Major Ruby upgrades can require Bundler and Jekyll to be installed again; otherwise, everything from here is just two short recipes.

### Starting a brand-new blog

Each blog lives in its own folder, and the toolchain never needs reinstalling:

```bash
jekyll new another-blog
cd another-blog
bundle install
bundle exec jekyll serve --livereload
```

Scaffold, install the project's gems, serve — the same pattern as steps 5 and 6.

### Returning to an existing blog

After a restart — or simply the next morning — only the server normally needs starting. Run `bundle install` first if Ruby changed or the project's `Gemfile` was updated:

```bash
cd my-blog
bundle exec jekyll serve --livereload
```

Open `http://localhost:4000`, write, save, and let the browser refresh itself. `Control + C` when done.

## The takeaway

The stack looks long — Apple developer tools, Homebrew, Ruby, RubyGems, Bundler, Jekyll — but each layer does one job, and after the initial setup the daily workflow collapses to a single loop: write Markdown, save, glance at the browser. A private knowledge base with the ergonomics of a real website, and an audience of exactly one.

*Note: This hobby project and article were created with AI assistance and verified by running the commands. These are working notes, not authoritative documentation.*
