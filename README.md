# 📱 Readium Mobile

Readium Mobile is a toolkit for ebooks, audiobooks and comics written in Swift &amp; Kotlin.

[With 60+ applications](https://github.com/readium/awesome-readium?tab=readme-ov-file#apps-based-on-readium-mobile), it's the most popular toolkit for building reading applications on smartphones and tablets.

## Formats

The following formats are supported with optional [Readium LCP support](https://www.edrlab.org/readium-lcp/) for protection:

- EPUB 2.x and 3.x support
- EPUB Fixed Layout (FXL) support
- PDF support
- Audiobook support ([streamed](https://readium.org/webpub-manifest/profiles/audiobook) or [packaged](https://readium.org/lcp-specs/notes/lcp-for-audiobooks.html))

## Features

- Support for user preferences
- Night & sepia modes
- Search in EPUB
- Highlights/annotations
- Text-to-Speech (TTS) support
- Pagination and scrolling
- Support for right-to-left (RTL) and vertical scrolling


## Roadmap

- [EPUB 3 Media Overlays](https://www.w3.org/TR/epub/#sec-media-overlays)
- [Divina support](https://readium.org/webpub-manifest/profiles/divina) for comics/manga/webtoons

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

## License

Readium Mobile is available under a [BSD-3 license](https://github.com/readium/mobile/blob/main/LICENSE).
