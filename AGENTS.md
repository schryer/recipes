# Working on the recipes

Read this before adding or changing a recipe, including in a
notes-processing thread that turns a vault recipe note into one.

The format is
[FORMAT.md in schryer/recipe-host](https://github.com/schryer/recipe-host/blob/main/FORMAT.md):
read it first, and copy `recipes/_template.md` to start. It wins over this
file.

## Adding a recipe

1. Write `recipes/<category>/<slug>.md` from the template.
2. Link its ingredients: `recipe-host link recipes/<category>/<slug>.md`
   (install with `npm install -g github:schryer/recipe-host#v0.1.0`). Check
   each link it made, then link or add every line it reports. Before adding
   an ingredient, search `ingredients/` names and aliases, so a new name for
   an existing ingredient becomes an alias instead of a duplicate.
3. `recipe-host check` must report no errors; `recipe-host build` also
   makes the cards when `typst` is installed.
4. Open a pull request. Say in it which ingredients are new.

## House style

- Metric first, original measure in brackets; °C with °F in brackets in the
  method.
- Only our own photos go in `photos/`; link other sites' photos from
  "Similar recipes".
- A method worked out from an ingredient-only note opens with a
  `> [!NOTE]` alert, **Draft method for David to check.**; worked-out
  quantities say **Draft quantities for David to check.**
- Keep unchecked third-party details, like shop addresses, out of the public
  recipe.
