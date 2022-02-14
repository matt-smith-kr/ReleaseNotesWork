# Change Log

All notable changes to this project will be documented in this file.
`Cuckoo` adheres to [Semantic Versioning](https://semver.org/).

## master

### Added

### Breaking Changes

### Updated

### Fixed

## 3.0.0

### Breaking Changes
- Updated Bedrock dependency to require 1.0.0

## 2.0.0

### Added
- Display configuration loading errors in the UI. These will appear at the top of the mock list and show descriptions for all errors encountered when loading configurations.
- Add an "Enable All" or "Disable All" button to conditional mock groups with more than one mock. This button will allow you to easily enable or disable the entire group with a single tap.
- Add `httpMethod`, `expectedBody` and `strcitBodyMatching` properties to `RepathMock` and `ConditionalMock`. These properties are optional or have a default, and will retain backwards compatibility with existing configuration JSON and direct initialization.
- New `RequestParameters` type that provides the details used to match mock responses to requests.
- New `MockRepository` function `mockResponse(for: URLRequest, ...)`, which is the primary function used to look up mock responses.

### Breaking Changes
- Changed the `url: URL` property on `MockResponse` to `request: RequestParameters`.
- Event and Error types have been updated to have `RequestParameters` instead of a `URL` where appropriate.
- Updated to use `Combine.Cancellable` instead of `Bedrock.Cancellable`.
- The `MockRepository` function `mockResponse(for: URL, ...)` has been removed.

## 1.0.1

### Updated
- Updated `CuckooView` to no longer be wrapped in a `NavigationView`. This allows the view to be wrapped in, or pushed on to, a navigation view by the calling code, and allows adding custom navigation buttons to the view as needed.

### Fixed
- Fixed a crash in the UI that would occur when filtering the list.

## 1.0.0

### Added
- `PersistentDataSource` is a concrete `MutableRepsoitoryDataSource` implementation that supports saving its state to disk and launch arguments.
- A new UI, built with SwiftUI. Create a `CuckooView` instance providing a repository and mutable data source.
- Launch argument support for configuring/enabling cuckoo at launch. This will override any saved settings and not be updatable by the UI.

### Breaking Changes
- Renamed `ConditionalMockDataSource` to `RepositoryDataSource`.
- Moved the `isEnabled` property from the `MockRepository` to the `RepositoryDataSource`. This unifies the mutable runtime state under the data source domain instead of being spread around.
    - As part of this change the default enabled status of the repository is delegated to the data source. When using a `PersistentDataSource` that defaults to disabled unless overridden in the initializer.
- The `RepositoryDataSource` provided to the `MockConfiguration` is no longer optional.
- Updated directory structure used for Cuckoo mock responses and configuration, removed customization of directory structure from public API.
    - A new root directory `cuckoo` is expected that will contain all other directories.
    - Repath and Conditional mock configuration directories have been renamed to `conditional-mock-configuration` and `repath-mock-configuration`
    - Mock responses are now expected in directories based on the type of mock: `automatic-mock-responses`, `conditional-mock-responses`, `repath-mock-responses`

## 0.1.0
Initial Release of Cuckoo.
