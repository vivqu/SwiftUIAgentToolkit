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
