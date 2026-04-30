# Mariana Jó

Personal website and blog built with Hugo and PaperMod, intended for GitHub Pages.

The repo uses `hugo.yaml` for site configuration and YAML front matter (`---`) in content files.

## Local development

Start the dev server:

```sh
docker compose up
```

Build the site:

```sh
docker compose run --rm hugo build --gc --minify
```

## Multilingual content

- Default language: `pt-br`
- Secondary language: `en`
- Portuguese content lives at the site root
- English content lives under `/en/`

Create translated content by file name suffix:

- `content/about.pt-br.md`
- `content/about.en.md`

- `content/posts/my-post.pt-br.md`
- `content/posts/my-post.en.md`

To create a new post version:

```sh
docker compose run --rm hugo new content posts/my-new-post.pt-br.md
docker compose run --rm hugo new content posts/my-new-post.en.md
```
