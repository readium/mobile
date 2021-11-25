# Readium Mobile

Readium Mobile is a toolkit for ebooks, audiobooks and comics written in Swift &amp; Kotlin.

## Features

- [x] EPUB 2.x and 3.x support
- [x] Audiobook support
- [x] PDF support
- [x] Readium LCP support
- [x] CBZ support
- [x] Custom styles
- [x] Night & sepia modes
- [x] Pagination and scrolling
- [x] Table of contents
- [x] OPDS 1.x and 2.0 support
- [x] FXL support
- [x] RTL support
- [x] Search in EPUB
- [x] Highlights/annotations
- [ ] TTS
- [ ] EPUB 3 Media Overlays
- [ ] Divina support

## Codebase

Readium Mobile is a modular project, which follows the [Readium Architecture](https://github.com/readium/architecture). The different modules are found in the following repositories.

### Readium Mobile Android

The modules are set to SDK 29 (Q4 2020) but you should be able to support down to SDK 21.

* [`kotlin-toolkit`](https://github.com/readium/kotlin-toolkit) – New monorepo for Readium Mobile Android.

Previous versions are still available, split in different repositories:

* [`r2-shared-kotlin`](https://github.com/readium/r2-shared-kotlin) – Shared `Publication` models and utilities
* [`r2-streamer-kotlin`](https://github.com/readium/r2-streamer-kotlin) – Publication parsers and local HTTP server
* [`r2-navigator-kotlin`](https://github.com/readium/r2-navigator-kotlin) – Plain view controllers rendering publications
* [`r2-opds-kotlin`](https://github.com/readium/r2-opds-kotlin) – Parsers for OPDS catalog feeds
* [`r2-lcp-kotlin`](https://github.com/readium/r2-lcp-kotlin) – Service and models for Readium LCP

The [Test App](https://github.com/readium/r2-testapp-kotlin) demonstrates how to integrate the Readium 2 Kotlin toolkit in your own reading app.

A workspace aimed at easing the install of the project is provided in [`r2-workspace-kotlin`](https://github.com/readium/r2-workspace-kotlin).

### Readium Mobile iOS

The toolkit currently requires iOS 10+ (Q3 2021).

* [`swift-toolkit`](https://github.com/readium/swift-toolkit) – New monorepo for Readium Mobile iOS.

Previous versions are still available, split in different repositories:

* [`r2-shared-swift`](https://github.com/readium/r2-shared-swift) – Shared `Publication` models and utilities
* [`r2-streamer-swift`](https://github.com/readium/r2-streamer-swift) – Publication parsers and local HTTP server
* [`r2-navigator-swift`](https://github.com/readium/r2-navigator-swift) – Plain view controllers rendering publications
* [`r2-opds-swift`](https://github.com/readium/r2-opds-swift) – Parsers for OPDS catalog feeds
* [`r2-lcp-swift`](https://github.com/readium/r2-lcp-swift) – Service and models for Readium LCP

The [Test App](https://github.com/readium/r2-testapp-swift) demonstrates how to integrate the Readium 2 Swift toolkit in your own reading app.
