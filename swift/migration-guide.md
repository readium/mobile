# Migration Guide

All migration steps necessary in reading apps to upgrade to major versions of the Swift Readium toolkit will be documented in this file.

## [2.0.0-alpha.2](https://github.com/readium/r2-testapp-swift/compare/2.2.0-alpha.1...2.2.0-alpha.2)

The 2.0.0 introduces numerous new APIs in the Shared Models, Streamer and LCP libraries, which are detailed in the following proposals. We highly recommend skimming over the "Developer Guide" section of each proposal before upgrading to this new major version.

* [Format API](https://readium.org/architecture/proposals/001-format-api)
* [Composite Fetcher API](https://readium.org/architecture/proposals/002-composite-fetcher-api)
* [Publication Encapsulation](https://readium.org/architecture/proposals/003-publication-encapsulation)
* [Publication Helpers and Services](https://readium.org/architecture/proposals/004-publication-helpers-services)
* [Streamer API](https://readium.org/architecture/proposals/005-streamer-api)
* [Content Protection](https://readium.org/architecture/proposals/006-content-protection)

[This `r2-testapp-swift` commit](https://github.com/readium/r2-testapp-swift/commit/f2f7ed059c4159dfde0549968aa3c564b8278a16) showcases all the changes required to upgrade the Test App.

[Please reach out on Slack](http://readium-slack.herokuapp.com/) if you have any issue migrating your app to Readium 2.0.0, after checking the [troubleshooting section](Troubleshooting).

### Replacing the Parsers with `Streamer`

Whether you were using individual `PublicationParser` implementations or `Publication.parse()` to open a publication, you will need to replace them by an instance of `Streamer` instead.

#### Opening a Publication

Call `Streamer::open()` to parse a publication. It will return asynchronously a self-contained `Publication` model which handles metadata, resource access and DRM decryption. This means that `Container`, `PubBox` and `DRM` are not needed anymore, you can remove any reference from your app.

The `allowUserInteraction` parameter should be set to `true` if you intend to render the parsed publication to the user. It will allow the Streamer to display interactive dialogs, for example to enter DRM credentials. You can set it to `false` if you're parsing a publication in a background process, for example during bulk import.

```swift
let streamer = Streamer()

streamer.open(file: File(url: url), allowUserInteraction: true) { result in
    switch result {
    case .success(let publication):
        // ...
    case .failure(let error):
        alert(error.localizedDescription)
    case .cancelled:
        break
    }
}
```

#### Error Feedback

In case of failure, a `Publication.OpeningError` is returned. It implements `LocalizedError` and can be used directly to present an error message to the user.

If you wish to customize the error messages or add translations, you can override the strings declared in `r2-shared-swift/Resources/Localizable.strings` in your own app bundle. This goes for LCP errors as well, which are declared in `readium-lcp-swift/Resources/Localizable.strings`.

#### Advanced Usage

`Streamer` offers other useful APIs to extend the capabilities of the Readium toolkit. Take a look at its documentation for more details, but here's an overview:

* Add new custom parsers.
* Integrated DRM support, such as LCP.
* Provide different implementations for third-party tools, e.g. ZIP, PDF and XML.
* Customize the `Publication`'s metadata or `Fetcher` upon creation.
* Collect authoring warnings from parsers.

### Extracting Publication Covers

Extracting the cover of a publication for caching purposes can be done with a single call to `publication.cover`, instead of reaching for a `Link` with `cover` relation. You can use `publication.coverFitting(maxSize:)` to select the best resolution without exceeding a given size. It can be useful to avoid saving very large cover images.

```diff
-let cover = publication.coverLink
-    .flatMap { try? container.data(relativePath: $0.href) }
-    .flatMap { UIImage(data: $0) }

+let cover = publication.coverFitting(maxSize: CGSize(width: 100, height: 100))
```

### LCP and Other DRMs

#### Opening an LCP Protected Publication

Support for LCP is now fully integrated with the `Streamer`, which means that you don't need to retrieve the LCP license and fill `container.drm` yourself after opening a `Publication` anymore.

To enable the support for LCP in the `Streamer`, you need to initialize it with a `ContentProtection` implementation provided by `r2-lcp-swift`.

```swift
let lcpService = LCPService()
let streamer = Streamer(
    contentProtections: [
        lcpService.contentProtection()
    ]
)
```

Then, to prompt the user for their passphrase, you need to set `allowUserInteraction` to `true` and provide the instance of the hosting `UIViewController` with the `sender` parameter when opening the publication.

```swift
streamer.open(file: File(url: url), allowUserInteraction: true, sender: hostViewController)
```

Alternatively, if you already have the passphrase, you can pass it directly to the `credentials` parameter. If it's valid, the user won't be prompted.

#### Customizing the Passphrase Dialog

The LCP Service now ships with a default passphrase dialog. You can remove the former implementation from your app if you copied it from the test app. But if you still want to use a custom implementation of `LCPAuthenticating`, for example to have a different layout, you can pass it when creating the `ContentProtection`.

```swift
lcpService.contentProtection(with: CustomLCPAuthentication())
```

#### Presenting a Protected Publication with a Navigator

In case the credentials were incorrect or missing, the `Streamer` will still return a `Publication`, but in a "restricted" state. This allows reading apps importing publications by accessing their metadata without having the passphrase.

But if you need to present the publication with a Navigator, you will need to first check if the `Publication` is not restricted.

Besides missing credentials, a publication can be restricted if the Content Protection returned an error, for example when the publication is expired. In which case, you must display the error to the user by checking the presence of a `publication.protectionError`.

```swift
if !publication.isRestricted {
    presentNavigator(publication)

} else if let error = publication.protectionError {
    // A status error occurred, for example the publication expired
    alert(error)

} else {
    // User cancelled the unlocking, for example by dismissing a passphrase dialog.
}
```

#### Accessing an LCP License Information

To check if a publication is protected with a DRM, you can use `publication.isProtected`.

If you need to access an LCP license's information, you can use the helper `publication.lcpLicense`, which will return the `LCPLicense` if the publication is protected with LCP. Alternatively, you can use `LCPService::retrieveLicense()` as before.

#### Acquiring a Publication from an LCPL

`LCPService.importPublication()` was replaced with `acquirePublication()`, which returns a cancellable task. It doesn't require the user to enter its passphrase anymore to download the publication.

```swift
let acquisition = lcpService.acquirePublication(
    from: lcpl,
    onProgress: { progress in ... },
    completion: { result in ... }
)
acquisition.cancel()
```

#### Supporting Other DRMs

You can integrate additional DRMs, such as Adobe ACS, by implementing the `ContentProtection` protocol. This will provide first-class support for this DRM in the Streamer and Navigator.

Take a look at the [Content Protection](https://readium.org/architecture/proposals/006-content-protection) proposal for more details. [An example implementation can be found in `r2-lcp-swift`](https://github.com/readium/r2-lcp-swift/tree/develop/readium-lcp-swift/Content%20Protection).

### Troubleshooting

#### Tried to present the LCP dialog without providing a `UIViewController` as `sender`

To be able to present the LCP passphrase dialog, the default `LCPDialogAuthentication` needs a hosting view controller as context. You must provide it to the `sender` parameter of `Streamer::open()`, if `allowUserInteraction` is true.

```swift
streamer.open(file: File(url: url), allowUserInteraction: true, sender: hostViewController)
```

#### Assertion failed: The provided publication is restricted. Check that any DRM was properly unlocked using a Content Protection.

Navigators will refuse to be opened if a publication is protected and not unlocked. You must check if a publication is not restricted by following [these instructions](#presenting-a-protected-publication-with-a-navigator).