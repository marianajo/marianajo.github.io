# AGENTS.md

## Repo Facts
- This repository is intended to become a personal website built with Hugo and deployed to GitHub Pages.
- `PaperMod` is the chosen base theme for the initial build.
- The site is multilingual with Brazilian Portuguese as the default language and English as the secondary language.
- The repo is currently in an early setup stage; do not assume Hugo has already been initialized unless Hugo config and directories are present.

## Working Notes
- Prefer Hugo-native structure as the site is built out: `hugo.yaml`, `content/`, `layouts/`, `static/`, `assets/`, and theme/module config only when they actually exist.
- Local development is Docker-first via `compose.yaml`.
- Run the dev server with `docker compose up`.
- Run a production-style build with `docker compose run --rm hugo build --gc --minify`.
- The Hugo Docker image already uses `hugo` as its entrypoint, so container commands should be subcommands like `build` or `server`, not `hugo build`.
- Check the current repo state before making changes, since early-stage repos may have partial or in-progress setup.
- Keep changes minimal and aligned with Hugo conventions rather than introducing ad hoc site structure.
- Prefer a writing-first structure with top-level `Posts` and `About` navigation; use the site title as the home link.
- Content translations are organized by file name suffix, for example `content/about.pt-br.md` and `content/about.en.md`.
- Brazilian Portuguese is the default language at the site root; English content is served under `/en/`.
- For blog posts, create paired files with the same base name whenever possible, e.g. `content/posts/my-post.pt-br.md` and `content/posts/my-post.en.md`.
- Never perform git write operations in this repo. Do not commit, amend, push, create branches, rebase, merge, reset, or otherwise change git history or state. All git write actions are handled manually by the user.
