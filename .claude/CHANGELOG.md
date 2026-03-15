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

Created test app
- Added `TestSwiftUIApp/*` files to .gitignore