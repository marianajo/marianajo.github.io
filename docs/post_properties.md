# Propriedade de posts

Referência rápida de propriedades de post, que vão no frontmatter.

```
title: "Post title"
date: 2026-04-29T10:00:00Z
draft: true
summary: ""
description: ""
tags:
  - list-like
categories:
  - list-like
author: "Mariana Jó"
cover:
  image: "images/hugo-cover.jpg"
featuredImage: "images/hugo-featured.jpg"
slug: "post-slug"
aliases:
  - /posts/intro-hugo/
toc: true
weight: 1
```

## Propriedades essenciais

### `title`
**Tipo:** string

Título do post. Aparece no topo da página individual, nas listagens, no RSS e nos links de navegação.

### `date`
**Tipo:** data (RFC3339 ou `YYYY-MM-DD`)

Data de publicação. Define a ordenação dos posts nas listagens (mais recente primeiro). É a base para paginação e arquivos.

### `draft`
**Tipo:** bool (`true` ou `false`)

Se `true`, o post não aparece no build normal. Para ver posts rascunho no servidor local, rode com `--buildDrafts`. No build de produção, eles são ignorados.

### `summary`
**Tipo:** string

Resumo curto do post. Aparece na listagem de posts e no feed RSS. Se não for definido, o Hugo pega automaticamente os primeiros parágrafos do conteúdo.

## Propriedades opcionais

### `description`
**Tipo:** string

Descrição mais longa para SEO. Usada como meta tag `<meta name="description">` e no opengraph. Se não existir, o Hugo usa `summary`.

### `tags`
**Tipo:** lista de strings

Etiquetas do post. Aparecem no rodapé da página individual e geram uma página `/tags/` com todas as tags disponíveis.

### `categories`
**Tipo:** lista de strings

Categorias do post. Mesma lógica das tags — aparecem no rodapé e geram `/categories/`.

### `author`
**Tipo:** string

Autor do post. Aparece nos metadados junto com a data. Útil se o site tiver múltiplos autores. Se não for definido, usa o autor padrão do site (se houver).

### `cover`
**Tipo:** objeto

Imagem de capa do post. O PaperMod exige o formato:

```yaml
cover:
  image: "images/capa.jpg"
  caption: "Legenda opcional"
  relative: false
  hidden: true
```

- `image` — caminho da imagem (pode ser relativo ao post ou no `static/`)
- `caption` — texto exibido abaixo da imagem
- `relative: true` — trata o caminho como relativo ao diretório do post
- `hidden: true` — esconde a capa na página individual (mas mantém na listagem)

### `featuredImage`
**Tipo:** string

Imagem destacada para opengraph, Twitter cards e RSS. Se não for definida, o Hugo tenta usar `cover.image`.

### `slug`
**Tipo:** string

Define a URL final do post. Ex: `slug: meu-post` gera a URL `/posts/meu-post/` em vez de algo gerado automaticamente a partir do título.

### `aliases`
**Tipo:** lista de strings

URLs alternativas que redirecionam para este post. Útil em migrações ou quando muda-se o slug de um post antigo para que links antigos não quebrem.

### `toc`
**Tipo:** bool (`true` ou `false`)

Se `true`, mostra o sumário lateral com links para os headings do post. No PaperMod, funciona como override da configuração global `ShowToc`.

### `weight`
**Tipo:** inteiro

Define ordenação manual em listagens. Quando presente, sobrescreve a ordenação por data. Valores mais baixos aparecem primeiro. Útil para fixar um post no topo.
