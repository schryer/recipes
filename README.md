# Recipes

Family recipes, served at **[schryer.eu/recipes](https://schryer.eu/recipes/)**
by [recipe-host](https://github.com/schryer/recipe-host). Each recipe has a
printable A5 card, and every ingredient is on a master list with the recipes
it's used in and what can replace it.

- `recipes/<category>/<slug>.md`: one recipe
- `ingredients/<id>.md`: one ingredient, with its notes and substitutions
- `photos/<slug>.jpg`: our own photos
- `recipe-host.yml`: site settings

[FORMAT.md in recipe-host](https://github.com/schryer/recipe-host/blob/main/FORMAT.md)
is the format, and [AGENTS.md](AGENTS.md) is how recipes get added here.

## Changing things

Every change is a pull request. The `Recipes` check builds the site and the
cards for each one, and merging to `main` publishes it.

On the site, the ingredient list's buttons (add an ingredient, merge two,
add a substitution note) open a prefilled issue; submitting it opens the pull
request for you.

To work locally:

```sh
npm install -g github:schryer/recipe-host#v0.1.0
recipe-host link recipes/sauces/new-sauce.md
recipe-host check
recipe-host serve
```

## History

The recipes started in [schryer/docs](https://github.com/schryer/docs) as a
MyST site and moved here, with their history, in October 2026.
