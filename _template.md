---
title: Recipe name
subtitle: One line on what it is and why it's good
tags: [main-ingredient, cuisine, technique]
date: YYYY-MM-DD
# thumbnail: ../photos/SLUG.jpg
exports:
  - id: card
    format: typst
    template: ../../templates/recipe-card
    output: ../_build/cards/SLUG.pdf
downloads:
  - id: card
    title: Recipe card (A5 PDF)
---

:::{recipe}
:serves: 4
:prep: 15 min
:cook: 30 min
:source: https://example.com/the-recipe-this-was-adapted-from
:::

<!-- Once there is a photo:
:::{figure} ../photos/SLUG.jpg
:alt: What the photo shows
:::
-->

One or two sentences: what makes this recipe work, or the one thing not to
get wrong.

## Ingredients

- 500 g (1 lb) something, prepared how

## Method

1. **Short step name.** What to do, with the heat, time and the cue that it's done.

## Notes

Optional: substitutions, make-ahead, storage.

## Similar recipes

- [Their recipe title](https://example.com/recipe) (Site name)
