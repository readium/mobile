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
- [ ] Search in EPUB
- [ ] Highlights/annotations
- [ ] TTS

## Codebase

Readium Mobile is a modular project, which follows the [Readium Architecture](https://github.com/readium/architecture). The different modules are found in the following repositories: 

### Readium Mobile Android

The test app are set to SDK 29 (Q4 2020) but you should be able to support down to SDK 21.

- [r2-shared-kotlin](https://github.com/readium/r2-shared-kotlin): shared models
- [r2-streamer-kotlin](https://github.com/readium/r2-streamer-kotlin): streamer module
- [r2-navigator-kotlin](https://github.com/readium/r2-navigator-kotlin): navigator module
- [r2-opds-kotlin](https://github.com/readium/r2-opds-kotlin): OPDS module
- [r2-lcp-kotlin](https://github.com/readium/r2-lcp-kotlin): LCP module

A test application is provided in:
- [r2-testapp-kotlin](https://github.com/readium/r2-testapp-kotlin)

A workspace aimed at easing the install of the project is provided in:
- [r2-workspace-kotlin](https://github.com/readium/r2-workspace-kotlin)

### Readium Mobile iOS

The toolkit is currently compliant with iOS 9 (Q4 2020); it will soon be upgraded to iOS 10+. 

- [r2-shared-swift](https://github.com/readium/r2-shared-swift): shared models
- [r2-streamer-swift](https://github.com/readium/r2-streamer-swift): streamer module
- [r2-navigator-swift](https://github.com/readium/r2-navigator-swift): navigator module
- [r2-opds-swift](https://github.com/readium/r2-opds-swift): OPDS module
- [r2-lcp-swift](https://github.com/readium/r2-lcp-swift): LCP module

A test application is provided in:
- [r2-testapp-swift](https://github.com/readium/r2-testapp-swift)

A workspace aimed at easing the install of the project is provided in:
- [r2-workspace-swift](https://github.com/readium/r2-workspace-swift)
