# Implementation Blueprint

## Goal

Set up a Hugo personal site using `PaperMod`, deployable to GitHub Pages, with:

- site title `Mariana Jó`
- top nav: `Posts`, `About`
- homepage: intro first, recent posts second
- balanced professional/personal tone
- blog-first structure
- no git write actions by the agent

## Phase 1: Repo Guidance

Create or update `AGENTS.md` to include:

- this repo is for a Hugo personal website deployed via GitHub Pages
- `PaperMod` is the chosen base theme
- the repo may be in early setup, so agents must verify config before assuming commands or structure
- prefer Hugo-native layout and config
- never perform git write actions:
  - no commit
  - no push
  - no amend
  - no branch/history-changing operations
- all git state changes are manual by the user

## Phase 2: Hugo Structure

Expected initial structure after setup:

```text
/
  AGENTS.md
  README.md
  hugo.yaml
  archetypes/
  assets/
  content/
    _index.md
    about.md
    posts/
      first-post.md
  layouts/
  static/
  themes/
    PaperMod/
  .github/
    workflows/
      hugo.yml
```

Notes:

- `layouts/` can remain mostly empty at first unless we need a homepage override
- `assets/` and `static/` can start empty
- `themes/PaperMod/` is the simplest mental model if using the theme as a checked-out directory

## Phase 3: Theme Integration

Use `PaperMod` as the base theme.

Recommended approach for simplicity:

- add the theme under `themes/PaperMod`
- set `theme = "PaperMod"` in Hugo config

Why this path:

- easiest to understand while learning Hugo
- avoids extra complexity early
- makes theme overrides straightforward later

Alternative later:

- Hugo Modules, if you want a cleaner dependency approach after the site is stable

## Phase 4: Hugo Config

Use `hugo.yaml`.

Recommended first config shape:

```toml
baseURL = "https://marianajo.github.io/"
languageCode = "en-us"
title = "Mariana Jó"
theme = "PaperMod"

[pagination]
  pagerSize = 10

[params]
  defaultTheme = "auto"
  ShowReadingTime = true
  ShowPostNavLinks = true
  ShowBreadCrumbs = false
  ShowCodeCopyButtons = true
  ShowShareButtons = false
  ShowToc = false

  [params.homeInfoParams]
    Title = "..."
    Content = "..."

[menu]
  [[menu.main]]
    identifier = "posts"
    name = "Posts"
    url = "/posts/"
    weight = 10

  [[menu.main]]
    identifier = "about"
    name = "About"
    url = "/about/"
    weight = 20
```

Recommendations for v1:

- keep `defaultTheme = "auto"` unless you later want forced light
- do not enable every PaperMod feature
- start without search, archives, or tags if they add noise

Optional params for later:

- social icons
- cover images
- RSS prominence
- custom favicon
- search page

## Phase 5: Content Model

Use this content structure:

- `content/_index.md`
- `content/about.md`
- `content/posts/first-post.md`

### Homepage

There are two good PaperMod-compatible ways to do it:

1. Use PaperMod’s `homeInfoParams`
- simplest
- likely enough for v1
- intro block above posts list

2. Override homepage layout later if needed
- only if the built-in homepage structure feels too limiting

Recommendation:

- start with `homeInfoParams`
- only create a custom homepage template if the result feels too generic

Homepage content shape:

- your name or intro line
- 1 to 3 short sentences about who you are
- a sentence about what the site is for
- recent posts list below

Example structure, not final copy:

- headline
- short intro
- short paragraph
- recent posts automatically rendered

### About page

`content/about.md` should cover:

- who you are
- professional background
- what you’re interested in
- some personal context or hobbies
- optionally links/socials later

Keep it as one page, not a CV.

### Posts

Use `content/posts/` for blog entries.

Suggested first sample post:

- a short welcome or “why I’m building this site” post

That helps validate:

- post list
- single post layout
- dates
- reading experience
- markdown rendering

## Phase 6: PaperMod Features to Use or Defer

Use early:

- responsive post layout
- recent posts on homepage
- reading time
- syntax highlighting
- light/dark support
- RSS

Defer until later:

- search
- archives
- tags
- share buttons
- comments
- analytics
- multilingual features

Reason:

- you want a clean first version, not a feature dump

## Phase 7: Visual Direction

Use `lethain.com` as a reference for:

- writing-first structure
- restrained navigation
- clear personal/professional identity
- recent writing prominence

But adapt it through PaperMod toward:

- a lighter feel
- less density
- a bit more warmth
- a simpler early-stage homepage

Practical styling goals for v1:

- calm typography
- generous whitespace
- no cluttered widgets
- strong readability for long-form posts
- no “theme demo” feel

## Phase 8: GitHub Pages Deployment

Add a GitHub Actions workflow in:

- `.github/workflows/hugo.yml`

The workflow should:

- trigger on push to your publishing branch
- install Hugo extended if required by theme compatibility
- build the site
- upload the generated `public/` output
- deploy via GitHub Pages Actions

Important implementation note:

- use current GitHub Pages official Hugo workflow shape
- verify against current docs when implementing rather than relying on memory

Also ensure:

- `baseURL` matches the GitHub Pages URL
- the repo settings point Pages to GitHub Actions deployment

## Phase 9: Optional First Overrides

Only add overrides if the default PaperMod output is too generic.

Best first override candidates:

- homepage intro styling/content structure
- footer content
- social links display
- minor CSS adjustments

Avoid early deep overrides like:

- replacing many theme templates
- redesigning list/single layouts immediately
- forking the theme

## Phase 10: Verification Checklist

After setup, verify:

1. Hugo site builds locally
2. homepage shows intro first, then recent posts
3. `Posts` nav works
4. `About` nav works
5. sample post renders correctly
6. RSS is available if enabled
7. GitHub Pages workflow is valid
8. PaperMod is wired correctly
9. no unnecessary extra pages appear
10. `AGENTS.md` reflects the repo rules, especially the git rule

## What To Keep Deliberately Minimal In V1

- nav: only `Posts`, `About`
- content: one sample post, one about page, one homepage intro
- features: only what supports writing and reading
- theme changes: small, targeted, reversible

## What Comes After V1

Once the scaffold is live, next likely improvements are:

1. refine homepage copy
2. polish the About page
3. add real posts
4. add social/profile links
5. decide on tags or archives
6. add subtle visual customization
7. optionally add search

## Recommended Implementation Order

When execution starts, do it in this order:

1. update `AGENTS.md`
2. scaffold Hugo
3. add `PaperMod`
4. create `hugo.yaml`
5. create `Home`, `About`, `Posts`
6. add one sample post
7. add GitHub Pages workflow
8. run Hugo build verification
9. only then consider small visual tweaks

## Multilingual Plan

### Goal

Support the site in both Brazilian Portuguese and English, with `pt-br` as the default language.

### Approach

Use Hugo multilingual mode with translation by file name.

Examples:

- `content/about.pt-br.md`
- `content/about.en.md`

- `content/posts/my-post.pt-br.md`
- `content/posts/my-post.en.md`

This keeps both language versions of each page or post linked together naturally.

### Default Language

Set:

- `pt-br` as the default language
- Portuguese at the root URL
- English under `/en/`

Expected URLs:

- Portuguese home: `/`
- English home: `/en/`
- Portuguese post: `/posts/my-post/`
- English post: `/en/posts/my-post/`

### Config Changes

Update `hugo.yaml` to:

- set `defaultContentLanguage = "pt-br"`
- set `defaultContentLanguageInSubdir = false`
- define:
  - `languages.pt-br`
  - `languages.en`

Move language-specific values under each language block, especially:

- menu labels
- homepage intro content
- language names/codes

### Content Migration

Rename current content files to explicit Portuguese files:

- `content/_index.md` -> `content/_index.pt-br.md`
- `content/about.md` -> `content/about.pt-br.md`
- `content/posts/first-post.md` -> `content/posts/first-post.pt-br.md`

Create English counterparts:

- `content/_index.en.md`
- `content/about.en.md`
- `content/posts/first-post.en.md`

### Menus

Use language-specific menus.

Portuguese:

- `Posts`
- `Sobre`

English:

- `Posts`
- `About`

### Theme Behavior

PaperMod already has multilingual support and translation-aware header logic.

Once both languages are configured and translated content exists, verify:

- language switcher appears in the header
- translated pages link to their counterparts correctly

### Writing Workflow

For each new post, create two files:

- `slug.pt-br.md`
- `slug.en.md`

Keep the same base filename so Hugo links them as translations.

### Publishing Recommendation

Use a flexible translation workflow:

- a post may be published in one language first
- the second language version can be added later

This reduces friction while preserving Hugo’s translation support when both files exist.

### Implementation Order

1. Convert `hugo.yaml` to multilingual configuration
2. Rename existing content to `.pt-br.md`
3. Create English versions of home, about, and first post
4. Localize menu labels
5. Verify PaperMod language switcher
6. Rebuild and test both language paths
7. Update archetypes and authoring guidance for bilingual posts

### Verification Checklist

- root path serves Portuguese
- `/en/` serves English
- `Posts` / `Sobre` appear in Portuguese
- `Posts` / `About` appear in English
- homepage intro is localized
- about page is localized
- post translations link correctly
- dates/localization render correctly per language
