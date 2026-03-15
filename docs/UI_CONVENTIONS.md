# UI Conventions

Guidelines for building correct, accessible, and visually coherent SwiftUI views in this toolkit.

## Layout

- Always respect safe areas — never underlap the status bar, Dynamic Island, or home indicator.
- Use `.safeAreaInset` or `.ignoresSafeArea` only when intentional (e.g., full-bleed backgrounds), and ensure interactive content stays within safe bounds.
- Prefer `maxWidth: .infinity` / `maxHeight: .infinity` with appropriate padding over hardcoded frame sizes.

## Accessibility

- Every interactive element (buttons, toggles, links) must have an `.accessibilityIdentifier` set.
- Visible, meaningful UI elements (labels, images, cards) should also have `.accessibilityIdentifier` so they can be targeted by UI tests and automation tools.
- Use `.accessibilityLabel` for elements whose visual representation doesn't clearly describe their purpose.

## Visual Distinction

- Never place white text on a white background or dark text on a dark background — always verify sufficient contrast.
- When building or reviewing UI, use the simulator screenshot to confirm elements are actually visible, not just present in the view hierarchy.
- Avoid relying solely on color to convey meaning; pair with iconography or labels for accessibility.
- **Exception**: If the user explicitly requests a color combination that results in low or no contrast (e.g. white text on white background), implement it as asked but emit a warning: e.g. `⚠️ Warning: this text will be invisible on a white background — intentional per your request.`

## Light/Dark Mode

- Use adaptive semantic colors instead of hardcoded `Color.white` or `Color.black` — prefer SwiftUI's `.primary`, `.secondary`, `Color(.systemBackground)`, `Color(.label)`, etc.
- Adaptive colors automatically adjust for light/dark mode and high-contrast accessibility settings.
- When building custom color assets, always define both light and dark variants in the asset catalog.

## When to Write a UI Test

Use `verify-ui` (screenshot) for appearance — layout, spacing, contrast, typography. Write a UI test when correctness matters:

- An element **must be present** for the feature to function (buttons, banners, empty states)
- UI visibility **depends on state or data** (logged in/out, empty vs. populated list)
- A **user interaction produces a result** that needs to be verified (tap → navigate, tap → change)
- An accessibility identifier is already set — if presence matters, assert it
