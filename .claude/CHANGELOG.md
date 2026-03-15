# Changelog

Decision history for the SwiftUIAgentToolkit repository.

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

Tested the new skills

- Ran a basic test to verify that adding UI works for `/verify-ui`
- Added `docs/UI_CONVENTIONS.md` to capture common UI issues
