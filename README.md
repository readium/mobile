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
- [x] Text-to-Speech (TTS) support
- [ ] EPUB 3 Media Overlays
- [ ] Divina support

## Codebase

Readium Mobile is a modular project, which follows the [Readium Architecture](https://github.com/readium/architecture).

### Readium Mobile on Android and Chrome OS

The toolkit currently requires Android 5.0+.

* [`kotlin-toolkit`](https://github.com/readium/kotlin-toolkit) – Monorepo for Readium Mobile in Kotlin.

A [Test App](https://github.com/readium/kotlin-toolkit/tree/develop/test-app) demonstrates how to integrate the Kotlin toolkit in your own reading app.

### Readium Mobile on iOS, iPadOS and macOS

The toolkit currently requires iOS 11+.

* [`swift-toolkit`](https://github.com/readium/swift-toolkit) – Monorepo for Readium Mobile in Swift.

A [Test App](https://github.com/readium/swift-toolkit/tree/develop/TestApp) demonstrates how to integrate the Swift toolkit in your own reading app.
