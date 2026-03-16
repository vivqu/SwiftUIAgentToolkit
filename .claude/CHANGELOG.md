# Changelog

Decision history for the SwiftUIAgentToolkit repository.

---

## 2026-03-16

Completed placeholder UI asset library

- Added 6 photo avatars, 10 product images, 6 hero images (3 nature + 3 architecture), and 6 abstract/background images from [Unsplash](https://unsplash.com/)
- Updated `assets/placeholder-images/README.md` with final counts, corrected filenames (no `placeholder-` prefix), and Unsplash source attribution
- Updated `placeholder-ui` skill decision guide to list all categories as bundled (no picsum fallback needed)
- Updated `README.md` with a Prototyping section listing available image categories

Added placeholder UI assets for prototyping

- Created `assets/placeholder-images/` with category subfolders (`avatars/`, `heroes/`, `products/`, `abstract/`)
- Added 6 illustrated avatar images from [Personas by Draftbit](https://personas.draftbit.com/)
- Created `assets/placeholder-images/README.md` with naming convention and sources
- Added `.claude/skills/placeholder-ui/` skill with decision guide, asset import steps, SwiftUI snippets, and SF Symbols reference
- Added `references/imageset-contents.json` template for creating Xcode imagesets
- Updated `CLAUDE.md` with a Prototyping section pointing to the skill
- Updated `docs/SETUP.md` to mention placeholder assets in the setup flow
- Added `TestSwiftUIApp/.claude/CLAUDE.md` explaining the test app is not git-tracked and how to revert changes

---

## 2026-03-15

Initial Setup

- Added `CLAUDE.md` with basic background and defined project purpose
- Updated to use iOS18+ for deployment target
- Created `docs/` and `.claude/` for storing information and tools
- Created `.claude/CHANGELOG.md` to track historical decisions

Decided to make this project a Github Template

- Chose Github template rather than a Swift Package (SPM) library because we are providing top-level agent direction. Also decided not to use `xcodegen` because it may require custom knowledge and prompting, which can be done simply through the Xcode workflow
- Created `docs/SETUP.md` to give installation instructions.

Created test app and internal plans

- Added `TestSwiftUIApp/*` files to .gitignore
- Added `docs/internal-dev/` folder to store agentic development plans

Setup instructions

- Added Xcode project setup information
- Added XcodeBuildMCP tool configuration steps

Added the verification loop

- Cleaned up the `docs/SETUP.md` file to be consistent
- Added `.claude/skills/verify-ui`
- Added `.claude/skills/verify-test`
- Added `.claude/skills/verify` and extracted common setup to a separate shared `xcodebuildmcp-session-setup.md` file

Tested the new skills

- Ran a basic test to verify that adding UI works for `/verify-ui`
- Added `docs/UI_CONVENTIONS.md` to capture common UI issues
- Made plan to migrate to a plugin

Migrated to `ios-verify-ui` plugin

- Published verify skills as a standalone Claude Code plugin at [vivqu/claude-swift-verify-ui-plugin](https://github.com/vivqu/claude-swift-verify-ui-plugin)
- Removed `.claude/skills/` directory (verify-ui, verify-test, verify, and shared session setup)
- Updated `CLAUDE.md` to reference plugin commands (`/ios-verify-ui:verify-ui`, `/ios-verify-ui:verify-test`, `/ios-verify-ui:verify`) and include install instructions
- Added a skill for the Xcode bridge MCP tool

Updated the README
