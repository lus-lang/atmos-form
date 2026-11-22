# AGENTS.md

This repository, `lus-lang/atmos-form`, is the `form` package of the atmosphere registry. Programs load it with `require("https://atmosp.here/2.0/form.lus")`.

## Scope

Decodes and encodes HTML form bodies. It reads and writes `application/x-www-form-urlencoded` text with nested keys, parses and builds `multipart/form-data` bodies with file uploads, and adds a body parser for both to `web` applications. The public API is every function that `form.lus` returns in its module table. A change to that API needs a new entry in `CHANGELOG.md` and a version change in the header.

## Layout

- `form.lus` is the whole package. Its header doc comment carries the package metadata and the declared permissions.
- `tests/*_test.lus` are the tests. They load the package from the parent directory through `TEST_DIR`.

The tests load `web` from a checkout of `lus-lang/atmos-web` next to this repository, so clone it into the same parent directory first.

## Commands

```sh
lus test tests          # run the tests
lus check form.lus     # lint, including the package codes
lus doc form.lus       # print the reference
```

## Rules

- Every public function has a doc comment that states each result and each error, following `spec/design/style.md` of the Lus repository.
- The package never calls `pledge`. A new permission is declared in the header and in the README.
- Prose has no dashes and no semicolons, and never names the Roblox Lua dialect.
- Every bug fix comes with a test that fails without it.
