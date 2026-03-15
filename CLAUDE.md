# SwiftUIAgentToolkit

A toolkit for bootstrapping SwiftUI mobile apps — designed for rapid, vibe-coded development.

## Project Purpose

A cloneable template for quickly starting new iOS apps with SwiftUI. See [docs/SETUP.md](docs/SETUP.md) for how to create an Xcode project inside this template.

## Architecture

- **Swift 5.9+ / SwiftUI** — No UIKit unless absolutely necessary
- **Minimum deployment target**: iOS 18+
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

In Xcode: `Cmd+B` to build, `Cmd+U` to run tests.

## Reserved Names

- **`TestSwiftUIApp`** is reserved and must not be used as a new app name. It is listed in `.gitignore` and is used internally to validate the correctness of the SwiftUIAgentToolkit project itself.
