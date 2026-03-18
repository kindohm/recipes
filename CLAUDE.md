# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

A static recipe website built with [Eleventy](https://www.11ty.dev/) (v3) and Nunjucks templates. Recipes are authored as Markdown files and compiled to a `_site/` directory.

## Commands

- `npm start` — build and serve with live reload (Eleventy dev server)
- `npm run build` — build once to `_site/`

## Architecture

### Layouts (Nunjucks)

Layouts live in `_includes/` and chain via front matter:

- `base.njk` — outer HTML shell (header, `<main>`, CSS link)
- `recipe.njk` — wraps recipe content in `<article>`, adds back link; sets `layout: base.njk`

### Recipes

Each recipe is a Markdown file in `recipes/`. Directory-level data (`recipes/recipes.json`) applies to all recipes:

- `layout: recipe.njk`
- `tags: recipes` — adds each recipe to the `collections.recipes` collection
- `permalink: /recipes/{{ title | slugify }}/` — generates a readable slug from the recipe title

Recipe front matter only needs `title`. All other settings come from the directory data file.

### Home Page (`index.njk`)

Iterates `collections.recipes` sorted alphabetically by title to render a linked table of contents.

### Styles

`css/style.css` is a passthrough copy (no processing). Referenced from `base.njk`.
