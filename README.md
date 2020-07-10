# Readium Mobile

Readium Mobile is an SDK for ebooks, audiobooks and comics written in Swift &amp; Kotlin.

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

Readium Mobile is a modular project, which follows the [Readium Architecture](https://github.com/readium/architecture) recommandations. The different modules are found in the following repositories: 

### Readium Mobile Android

- r2-shared-kotlin: shared models
- r2-streamer-kotlin: streamer module
- r2-navigator-kotlin: navigator module
- r2-opds-kotlin: opds module
- r2-lcp-kotlin: lcp module

A test application is provided in:
- r2-testapp-kotlin

A workspace aimed at easing the install of the project is provided in:
- r2-workspace-kotlin

Here is the full list of ["kotlin" modules](https://github.com/readium?q=kotlin).

### Readium Mobile iOS

- r2-shared-swift: shared models
- r2-streamer-swift: streamer module
- r2-navigator-swift: navigator module
- r2-opds-swift: opds module
- r2-lcp-swift: lcp module

A test application is provided in:
- r2-testapp-swift

A workspace aimed at easing the install of the project is provided in:
- r2-workspace-swift


Here is the full list of ["swift" modules](https://github.com/readium?q=swift).

