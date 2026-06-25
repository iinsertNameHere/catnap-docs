# Contributing to Catnap Docs

Thanks for helping improve the documentation. This is an mdBook project. Source files are Markdown and the site builds automatically on every push to `main`.

## Editing a page

All source files live in `docs/src/`. Find the relevant `.md` file and edit it directly.

## Adding a new page

1. Create the `.md` file in `docs/src/`
2. Add an entry for it in `docs/src/SUMMARY.md`

Every page must be listed in `SUMMARY.md` or it will not appear in the built site.

## Building locally

You need [mdBook](https://github.com/rust-lang/mdbook) installed.

```sh
cd docs && mdbook build   # build to docs/book/
cd docs && mdbook serve   # serve at http://localhost:3000 with live reload
```

## Writing style

* Write for everyone, not just developers. If you use a technical term, briefly explain it.
* No em-dashes or dashes in prose text. Use a comma, a period, or restructure the sentence.
* Keep examples concrete and something readers can copy and paste directly.
* When showing catnap config syntax, double check it against the actual config files in the catnap repository.

## Submitting changes

Open a pull request against `main`. The site deploys automatically once merged.
