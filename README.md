![Version](https://img.shields.io/badge/version-1.01-blue)
![B4X](https://img.shields.io/badge/B4X-B4J%20%7C%20B4A%20%7C%20B4i-orange)
![License](https://img.shields.io/badge/license-Apache%202.0-blue)
[![Donate](https://img.shields.io/badge/Donate-PayPal-00457C?logo=paypal)](https://www.paypal.com/paypalme/aeric80)

# myinvois-b4x-sdk

LHDN MyInvois B4X SDK — generate UBL 2.1 compliant e-invoices in XML and JSON format for Malaysia's MyInvois system. Cross-platform (B4J / B4A / B4i).

If you find this project useful, consider [buying me a coffee](https://www.paypal.com/paypalme/aeric80).

## Features

- **UBL 2.1 Invoice generation** — XML via `GenerateInvoiceXML()` and JSON via `GenerateInvoiceJSON()`
- **XAdES signature support** — populate UBLExtensions with digital signature elements (SignedInfo, KeyInfo, QualifyingProperties)
- **Compact or pretty-printed output** — toggle with the `Compact` parameter
- **Cross-platform** — runs on Windows, macOS, Linux (B4J), Android (B4A), iOS (B4i)
- **HTTP server mode** — B4J server project with `IndexHandler` for web-based invoice generation

## Project structure

```
source/
├── Lib/
│   ├── MyInvois.bas             # Core class: UBL type definitions + XML/JSON generation
│   ├── manifest.txt             # Library metadata and dependency declarations
│   └── myinvois-b4x-sdk.b4j    # Library development project
├── B4X/
│   ├── B4XMainPage.bas          # Sample page with CreateDocument() helper
│   ├── B4J/                     # B4J desktop app project
│   ├── B4A/                     # B4A Android app project
│   ├── B4i/                     # B4i iOS app project
│   └── server/                  # B4J server app project
│       ├── server.b4j           # HTTP server entry point
│       └── IndexHandler.bas     # Request handler with full signing pipeline example
release/
└── MyInvois.b4xlib              # Compiled library for B4X
```

## Usage

```b4x
Dim inv As MyInvois
inv.Initialize

Dim doc As Document = CreateDocument("1.1", "INV-001", Null, Null)
Dim xml As String = inv.GenerateInvoiceXML(doc, False)     ' pretty-printed XML
Dim json As String = inv.GenerateInvoiceJSON(doc, True)    ' compact JSON
```

See `B4XMainPage.bas:CreateDocument` for a complete document setup with supplier, customer, delivery, payment, tax, and line items.

## Server app

The `server/` project runs as an HTTP server. Browse to `http://127.0.0.1:8080` to generate sample invoices. It demonstrates the full e-invoice signing pipeline (canonicalization, digest, certificate handling, SHA-256 signing). The `MyInvoisUtils`-dependent code is wrapped in conditional compilation (`#If MYINVOISUTILS`) and activated by building with the `MyInvoisUtils` build configuration.

## Note on MyInvoisUtils

`MyInvoisUtils.bas` is maintained separately — a companion utility for certificate handling, SHA-256 signing, canonicalization, base64 encoding, and linearization. It depends on `JavaObject` and `Encryption` libraries (B4A/B4J only, not B4i). Internal helpers (`GetValue`, `GetValue2`, `GetValue3`, `GetValues`) on `MyInvois` are `Private` and consumed exclusively by the class itself.

## Dependencies

| Platform | Libraries |
|----------|-----------|
| B4J      | `Json`, `Xml2Map` |
| B4A      | `Json`, `Xml2Map` |
| B4i      | `iJSON`, `Xml2Map` |
| Server   | `jcore`, `jserver`, `jstringutils`, `myinvois` |

Additional dependencies (`xmlsec-2.1.8`, `slf4j`, `encryption`, `javaobject`) are required only for the `MyInvoisUtils` build configuration.

## License

See [LICENSE](LICENSE).
