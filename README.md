# SwiftUIAgentToolkit

A cloneable template for bootstrapping SwiftUI iOS apps — designed for rapid, AI-assisted development.

## What's included

- **`CLAUDE.md`** — Coding standards, architecture rules, and naming conventions baked in as agent instructions. Any AI coding agent (Claude Code, Cursor, etc.) will follow these automatically.
- **`docs/SETUP.md`** — Step-by-step guide to create a new Xcode project inside this template and configure the agent verification tools.
- **`ios-verify-ui` plugin** — Claude Code skills to build, screenshot, and test your app directly from the agent. See [Build & Verify](#build--verify) below.

## Requirements

- [Claude Code](https://claude.ai/code)
- Xcode 16+ (Xcode 26+ for built-in MCP bridge)
- iOS 18+ deployment target
- Swift 5.9+
- Node.js (for XcodeBuildMCP)

## Quick start

1. Clone this repo:

   ```bash
   git clone https://github.com/vivqu/SwiftUIAgentToolkit.git my-app
   cd my-app
   ```

2. Create an Xcode project inside the folder (see [docs/SETUP.md](docs/SETUP.md) for details).

3. Install the agent verification tools (see [docs/SETUP.md § Agent verification tools](docs/SETUP.md#agent-verification-tools)):
   - Adds the **Xcode** MCP bridge tool for Xcode 26.3
   - Register **XcodeBuildMCP** as a Claude Code MCP server
   - Install the **ios-verify-ui** plugin

4. Open Claude Code and start building.

## Build & Verify

Three slash commands are available once the `ios-verify-ui` plugin is installed:

```bash
claude plugin add https://github.com/vivqu/claude-swift-verify-ui-plugin
```

| Command | When to use |
| --- | --- |
| `/ios-verify-ui:verify-ui` | After any visual change — builds, launches on simulator, takes a screenshot, checks layout and contrast |
| `/ios-verify-ui:verify-test` | After adding or changing logic with tests — runs the full unit and UI test suite |
| `/ios-verify-ui:verify` | Full check — runs both UI and test verification in sequence |

## Architecture

This template enforces a consistent SwiftUI architecture:

- **MVVM** with `@Observable` macro (not `ObservableObject`)
- **SwiftUI-first** — no UIKit unless absolutely necessary
- **Async/await** for all async work
- **Safe areas respected** — content never underlaps the status bar or Dynamic Island
- Accessibility identifiers on all interactive and visible UI elements

See [CLAUDE.md](CLAUDE.md) for the full set of coding standards and conventions.
