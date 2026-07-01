# Contributing

## Reporting issues

- Check existing issues before opening a new one.
- Include the B4X platform (B4J/B4A/B4i), the version from the `.bas` header, and a minimal reproduction.

## Pull requests

- Keep changes focused — one feature or fix per PR.
- Match the existing code style (B4X conventions, no extra comments).
- Test XML and JSON output against the MyInvois validation portal before submitting.
- If adding a new UBL field, mirror the existing type pattern (define a Type in `Class_Globals`, wire it into `GenerateInvoice`, `GenerateInvoice2`, and `GetValues`).

## Development setup

The SDK is built with B4X (Anywhere Software IDE). Open `source/B4X/B4J/B4J.b4j` or the server project to get started. The library source is at `source/Lib/MyInvois.bas`.

## Optional utilities

`MyInvoisUtils.bas` (certificate handling, signing, canonicalization) is maintained separately. Public helpers in `MyInvois.bas` that appear unused are exposed for that companion library.
