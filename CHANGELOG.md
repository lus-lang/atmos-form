# Changelog

## 1.0.0

**Release date:** TBD

Version 1.0.0 is the first release of `form`.

- Added the `form` package.
  - `form.decode`: Decodes an `application/x-www-form-urlencoded` string into a table, with nested keys.
  - `form.encode`: Encodes a table as an `application/x-www-form-urlencoded` string.
  - `form.multipart`: Parses a `multipart/form-data` body into fields and files.
  - `form.encode_multipart`: Builds a `multipart/form-data` body and its content type.
  - `form.is_error`: Returns `true` for an error object that `form` raised.
  - `form.register`: Registers the body parser on a `web` scope.
