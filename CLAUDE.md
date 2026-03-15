# SwiftUIAgentToolkit

A toolkit for bootstrapping SwiftUI mobile apps — designed for rapid, vibe-coded development.

## Project Purpose

Provides reusable components, patterns, and utilities to quickly scaffold production-quality iOS apps with SwiftUI.

## Architecture

- **Swift 5.9+ / SwiftUI** — No UIKit unless absolutely necessary
- **Minimum deployment target**: iOS 18+
- **Package management**: Swift Package Manager (no CocoaPods)
- **Architecture pattern**: MVVM with `@Observable` macro (not `ObservableObject`)

## Coding Standards

- Use `@Observable` instead of `ObservableObject` / `@StateObject`
- Prefer `@State` for local view state, `@Environment` for dependency injection
- Extract reusable views into their own files — one view per file
- Use `#Preview` macro for previews, not `PreviewProvider`
- No force unwraps (`!`) — use `guard let`, `if let`, or provide defaults
- Async/await for all async work; no callbacks or Combine unless integrating external APIs

## Naming Conventions

- Views: `FooView.swift` (e.g., `HomeView`, `ProfileView`)
- ViewModels: `FooViewModel.swift`
- Models: `Foo.swift` (plain struct/class names)
- Extensions: `Foo+Bar.swift` (e.g., `Color+Brand.swift`)

## Build & Test

```bash
# Build via Xcode or:
xcodebuild -scheme SwiftUIAgentToolkit -destination 'platform=iOS Simulator,name=iPhone 16'

# Run tests:
xcodebuild test -scheme SwiftUIAgentToolkitTests -destination 'platform=iOS Simulator,name=iPhone 16'
```

