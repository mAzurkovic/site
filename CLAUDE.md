# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

- `hugo server -D` — local dev w/ drafts at http://localhost:1313
- `hugo --gc --minify` — production build into `public/`
- `./build.sh` — full Vercel build (installs Dart Sass, Go, Hugo, Node at pinned versions, then runs hugo); rarely needed locally

Hugo version pinned to 0.154.4 in `build.sh`.

## Architecture

Personal Hugo site deployed on Vercel. `vercel.json` runs `build.sh`; output dir is `public/`.

- `content/` — page content (markdown). `_index.md` is the homepage body; `experience.md` and `projects.md` are top-level pages.
- `layouts/index.html` — site-root override that injects the intro/headshot block above `{{ .Content }}` from `_index.md`. Theme layouts handle everything else.
- `themes/hugo-bearblog/` — vendored theme (formerly a submodule, now committed flat so local edits stick — see commit 3cac3e8). Edit here for theme-level changes; otherwise override the specific file under `layouts/`.
- `static/images/` — served at site root (e.g. `/images/headshot.png`).
- `public/` — generated output, committed. Will show as modified after any local `hugo` run.

`hugo.toml` `baseURL` is a placeholder; the real baseURL is injected at build time from `VERCEL_PROJECT_PRODUCTION_URL`.
