# Recipe format

How a recipe is written for the recipes site. Each recipe is one MyST
Markdown file; one build turns it into a page of the HTML site and a
printable A5 recipe card (PDF) that the page links to from its
**Download** menu.

This file is the contract for anything that writes recipes, including
the notes-processing threads that turn recipe notes from the Obsidian
vault (`schryer/notes`, `recipes/`) into recipes here. Start a new recipe
by copying [`_template.md`](_template.md).

## Where files go

```
recipes/
├── myst.yml               the site: title, theme, the {recipe} plugin
├── index.md               landing page: one card per recipe, by category
├── FORMAT.md              this file (not a page of the site)
├── _template.md           copy this to start a recipe (not a page either)
├── <category>/<slug>.md   one recipe
└── photos/<slug>.jpg      your own photos, named after the recipe
```

- **Category** is a folder one level below `recipes/`: `mains/`,
  `sauces/`, `sides/`, `desserts/`, `baking/`, `drinks/`. Make a new one
  when none fits. Every recipe sits exactly one folder deep, because the
  card's output path (`../_build/cards/...`) depends on it.
- **Slug** is the title in lowercase ASCII with hyphens:
  `boeuf-bourguignon`, `nuoc-cham`, `pumpkin-pie-filling`. It names the
  recipe file, its photo and its card, and becomes the page's URL.
- The site navigation is built from the folders, so there's nothing to
  register in `myst.yml`. Do add a card for the recipe to `index.md`
  under its category heading (see "The index page" below).

## Frontmatter

```yaml
---
title: Sous vide boeuf bourguignon
subtitle: Beef chuck in reduced red wine, 24 hours at 68 °C
tags: [beef, sous vide, french, stew]
date: 2026-10-19
thumbnail: ../photos/boeuf-bourguignon.jpg
exports:
  - id: card
    format: typst
    template: ../../templates/recipe-card
    output: ../_build/cards/boeuf-bourguignon.pdf
downloads:
  - id: card
    title: Recipe card (A5 PDF)
---
```

| Field | Required | What it holds |
|---|---|---|
| `title` | yes | The recipe's name, in sentence case. No straight double quotes (`"`): they break the card build (see AGENTS.md); use “curly” ones. |
| `subtitle` | yes | One line saying what it is: the main ingredient and method, or why it's good. Shown under the title on the page and the card. Same quote rule as `title`. |
| `tags` | yes | Lowercase: main ingredient, cuisine, technique, course. Used by site search. |
| `date` | yes | The day the recipe was written or last substantially changed, `YYYY-MM-DD`. |
| `thumbnail` | when there's a photo | Path to the recipe's own photo, `../photos/<slug>.jpg`. |
| `exports` | yes | Exactly the block above with only `<slug>` changed. It is what builds the card. |
| `downloads` | yes | Exactly the block above. It puts the card in the page's Download menu. |

Only fields MyST itself knows survive the build: MyST drops any other
frontmatter key with an "extra keys ignored" warning. That's why
servings, times and the source live in the `{recipe}` directive below and
not here.

## Body

The body has a fixed order. Use `##` for section headings, and keep the
section names exactly as written here so every recipe reads alike.

### 1. The facts line (required)

The first thing in the body:

```markdown
:::{recipe}
:serves: 4
:prep: 45 min
:cook: 24 h
:source: https://recipes.anovaculinary.com/recipe/beef-bourguignon
:::
```

It renders as one line on the page and the card: **Serves** 4 · **Prep**
45 min · **Cook** 24 h · Adapted from recipes.anovaculinary.com.

| Option | Meaning |
|---|---|
| `:serves:` | How many it feeds: `4`, `4–6`. |
| `:makes:` | Yield, when servings make no sense: `1 cup`, `one 23 cm (9 in) pie`. A recipe needs `:serves:` or `:makes:`, and the build warns when it has neither. |
| `:prep:` | Hands-on time. |
| `:cook:` | Time on the heat or in the oven or bath. |
| `:rest:` | Waiting: marinating, chilling, proving, cooling. |
| `:total:` | Start to finish, only when it isn't simply prep + cook. |
| `:source:` | The URL this recipe was mainly adapted from. Leave it out for a family recipe. |

Times are written `15 min`, `1 h 30 min`, `24 h`. Leave out any option
that doesn't apply.

### 2. Photo (when there is one)

```markdown
:::{figure} ../photos/boeuf-bourguignon.jpg
:alt: The finished bourguignon over mashed potatoes
:::
```

Only our own photos go in `photos/`: never copy another site's images
into the repository. Link to other sites' photos from "Similar recipes"
instead. Use a landscape JPEG about 1600 px wide, under 500 KB. The card
prints the photo small (32 mm high), so the page is where it shines.
A recipe without a photo leaves this out (keep the commented-out block
from `_template.md` as the slot to fill later) and omits `thumbnail`.

### 3. Introduction (required)

One or two sentences: what makes the recipe work, or the one thing not
to get wrong. No life story.

### 4. `## Ingredients` (required)

A bullet list, one ingredient per line, in the order they're used:
quantity, ingredient, then how it's prepared.

- Metric first, with the original measure in brackets when the source
  used cups or ounces: `500 ml (2 cups) beef stock`, `1.4 kg (3 lb) beef
  chuck`. Spoons stay as spoons (`2 tbsp`, `1 tsp`).
- Temperatures in °C, with °F in brackets in the method: `68 °C (155 °F)`.
- When ingredients fall into groups (a marinade and a sauce), use a
  `### For the marinade` heading over each group's list.

On the card, a list of more than six items is set in two columns.

### 5. `## Method` (required)

A numbered list. Each step starts with a short bold name, then says what
to do, with heat, time and the cue that tells you it's done:

```markdown
1. **Sear the beef.** Pat the beef dry and season well. Over high heat,
   sear it in batches, 1–2 minutes a side, until deeply browned.
```

### 6. `## Notes` (optional)

Substitutions, make-ahead and storage, variations, and a table when one
earns its place (the bourguignon's texture-by-temperature table, for
example). Sections with another name are fine here when the recipe needs
them, like `## Texture by temperature`.

### 7. `## Similar recipes` (optional, recommended)

Links to the best related recipes elsewhere, with their photos, one per
line: `- [Their title](url) (Site name)`. Link to a recipe already on
this site with a relative link: `[Kalbi marinade](../sauces/kalbi-marinade.md)`.

### What to leave out

- Citation markers like `[1, 2, 3]` and numbered reference lists from
  pasted AI answers. Keep the main source in `:source:` and the useful
  extras in "Similar recipes".
- Follow-up questions from a pasted AI answer ("Would you like...?").
- Pairs of literal `$` signs, which MyST reads as maths. Write `\$` for
  a dollar sign.

## The index page

Add one card per recipe to `index.md`, under a `##` heading for its
category, inside that category's grid:

```markdown
## Mains

::::{grid} 1 2 2 3

:::{card} Sous vide boeuf bourguignon
:link: mains/boeuf-bourguignon.md
:header: ![](photos/boeuf-bourguignon.jpg)
Beef chuck in reduced red wine, 24 hours at 68 °C.
:::

::::
```

The card title is the recipe's `title`, the text its `subtitle`. Leave
out `:header:` until the recipe has a photo.

## Building and previewing

Run these from `recipes/`, with Node.js and `typst` installed (`pubdoc setup`
checks both). Use `mystmd`, not `curvenote`, for the site: curvenote's
site build replaces the book theme with its own.

```sh
npx mystmd start                  # live preview of the site while editing
npx mystmd build --typst          # just the cards, into _build/cards/
npx mystmd build --typst --html   # cards, then the static site in _build/html/
```

Build the cards before or together with the site: the site copies each
card into its page's Download menu, and when a card hasn't been built
yet it reports "Could not find static resource" and leaves it out. Everything under `_build/`
is generated and gitignored.

## Publishing

The site lives at https://schryer.eu/recipes/. The *Recipes* workflow
(`.github/workflows/recipes.yml`) builds it on every pull request that
touches `recipes/` or the recipe templates, with `--strict`, so any build
warning (a `{recipe}` without `:serves:` or `:makes:`, a missing photo)
fails the check. Merging to `main` builds it with `BASE_URL=/recipes` and
publishes it to the web server that schryer/schryer-eu-infra manages.
Nothing else is needed to publish a recipe.
