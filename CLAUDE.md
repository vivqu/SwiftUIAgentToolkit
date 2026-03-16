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

Three commands are available for verifying app correctness after code changes. They are provided by the [ios-verify-ui plugin](https://github.com/vivqu/claude-swift-verify-ui-plugin) — install it with:

```bash
claude plugin add https://github.com/vivqu/claude-swift-verify-ui-plugin
```

- `/ios-verify-ui:verify-ui` — Build and run the app on a simulator, take a screenshot, and confirm UI changes look correct. Use after any visual change.
- `/ios-verify-ui:verify-test` — Run the unit and UI test suite and report pass/fail results. Use after adding or changing logic with tests.
- `/ios-verify-ui:verify` — Full verification: runs both UI and test checks in sequence and reports a combined summary. Use when you want to confirm everything is working end to end.

## Prototyping

When building prototype screens that need images, use the `/placeholder-ui` skill. It provides:

- Bundled placeholder images in `assets/placeholder-images/` (avatars, heroes, products, abstracts)
- Step-by-step instructions for importing images into `Assets.xcassets`
- SwiftUI snippets for common patterns (avatar, card image, skeleton state)
- SF Symbol reference for prototype icons

Prefer bundled images over network calls (`AsyncImage` + picsum) — they work offline and are semantically appropriate.

## Internal Development

- **`docs/internal-dev/` is used for storing plans for improvement of the SwiftUIAgentToolkit. It is not tracked by git and will not be published to the template.
- **`TestSwiftUIApp`** is reserved and must not be used as a new app name. It is used internally to validate the correctness of the SwiftUIAgentToolkit project itself.
