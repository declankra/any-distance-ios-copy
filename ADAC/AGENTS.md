# Repository Guidelines

## Project Scope & Intent
This directory mirrors the production Any Distance iOS app. It is open-sourced, but we do **not** contribute code or build it; our sole purpose is to inspect its patterns for inspiration while we design our own running app. Treat the contents as read-only reference material.

## Project Structure & Module Organization
The main app target lives in `ADAC/`, with feature areas grouped by domain (`Screens/`, `Activity Designs/`, `Data Stores/`, `Route Rendering/`, etc.) plus shared helpers in `SwiftUI Utilities/` and `View - UIKit/`. Companion targets sit at the repo root: `Any Distance WatchKit Extension/`, `Widget/`, and `OneSignalNotificationServiceExtension/`. Tests live in `ADACTests/`, mirroring production modules. Assets, storyboards, and entitlements stay under `ADAC/Assets.xcassets`, `Storyboards/`, and `ADAC.entitlements`.

## Build, Test, and Development Commands
We do not run builds or tests here. Use the commands below strictly for context when studying how the original team works:
- `pod install` — sync CocoaPods after `Podfile` or `Pods/` changes.
- `open ADAC.xcworkspace` — launch Xcode with all targets configured.
- `xcodebuild -workspace ADAC.xcworkspace -scheme ADAC -destination 'platform=iOS Simulator,name=iPhone 15' build` — verify the iOS app compiles from the CLI.
- `xcodebuild -workspace ADAC.xcworkspace -scheme ADAC -destination 'platform=iOS Simulator,name=iPhone 15' test` — run the XCTest bundles in `ADACTests/`.

## Coding Style & Naming Conventions
Swift 5 code uses 4-space indentation, `final` classes where possible, and `// MARK:` dividers (see `AppDelegate.swift`). Favor structs or enums for models in `Model/`, keep view logic under `Screens/`, suffix UIKit types with `ViewController`, and end SwiftUI components with `View`. Match file names to type names, centralize resources in `Resources/`, and reference asset catalog constants rather than raw strings.

## Testing Guidelines
XCTest powers the suite; every new feature touching Activities, Collectibles, or Edge APIs needs a matching `*Tests.swift` class with functions prefixed by `test`. Mock dependencies with the fixtures in `ADACTests/Resources`. Cover asynchronous flows (migrations, networking) before merging and run `xcodebuild … test` locally; CI assumes the same simulator destination.

## Commit & Pull Request Guidelines
Use short, present-tense commit subjects (“Add weather overlay renderer”) and include context in the body when touching multiple modules. Pull requests should describe the feature, list impacted targets, link Linear/GitHub issues, and supply screenshots or clips whenever UI in `Screens/` or `Activity Designs/` changes. Call out new pods or migrations so reviewers can re-run `pod install` or migrate stores.

## Security & Configuration Tips
Secrets are injected through `cocoapods-keys`; never commit raw API keys or `.xcconfig` overrides. When configuring OAuth providers, update Keychain access via `External Service Auth/` and test sandbox and production entries. Avoid logging user identifiers outside analytics and scrub device tokens before sharing logs.
