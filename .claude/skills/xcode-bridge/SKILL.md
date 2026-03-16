---
name: xcode-bridge
description: Guide for using the Xcode MCP bridge (xcrun mcpbridge) tools, including RenderPreview for SwiftUI previews.
disable-model-invocation: true
---

# Xcode MCP Bridge

Use the Xcode MCP bridge (`mcp__xcode__*` tools) when you need to render SwiftUI Previews or interact with Xcode's IDE directly.

## Prerequisites

Before calling any xcode bridge tool, verify:

1. Xcode is open and running
2. The `xcode` MCP server is connected — if tools are unavailable, tell the user to open Xcode and restart Claude Code

## Permission Prompt — Required Before Every Session

**Xcode will show an "Allow 'claude-code' to access Xcode?" dialog on the first tool call of every Claude Code session.** This is a macOS TCC (privacy) restriction: because Claude Code CLI has no persistent bundle identifier, the grant cannot be saved and must be re-approved each session.

Before making any xcode bridge tool call, use `AskUserQuestion` to warn the user:

```text
AskUserQuestion:
  question: "Xcode will show an 'Allow claude-code to access Xcode?' dialog on the next step.
             Please click Allow when it appears, then confirm here."
  options:
    - "I'm watching Xcode and will click Allow"
    - "I already clicked Allow this session"
```

Only proceed with tool calls after the user confirms. If a tool call hangs or returns an error after this, ask the user to check Xcode for a pending Allow dialog.

> **Tip for reducing prompts**: Set up `mcp-proxy` as a long-lived bridge process. This lets macOS grant permission once to the proxy rather than re-prompting on every session. See the [Swift Forums thread](https://forums.swift.org/t/reducing-the-friction-of-using-xcode-s-mcp-bridge-from-external-coding-agents/85353) for setup instructions.

## Standard Workflow

Every xcode bridge tool requires a `tabIdentifier`. Always start by calling `XcodeListWindows`:

```text
1. XcodeListWindows
   → returns tabIdentifier (e.g. "windowtab1") and workspacePath (e.g. ".../MyApp/MyApp.xcodeproj")

2. Derive sourceFilePath (project-relative, NOT absolute)
   → strip everything up to and including the .xcodeproj parent directory
   → e.g. workspacePath = "/Users/me/code/MyApp/MyApp.xcodeproj"
        file at        = "/Users/me/code/MyApp/MyApp/ContentView.swift"
        sourceFilePath = "MyApp/ContentView.swift"

3. Call the tool with tabIdentifier + sourceFilePath
```

## RenderPreview — Rendering SwiftUI Previews

The primary reason to use the xcode bridge. Renders a `#Preview` macro to a PNG snapshot.

```text
RenderPreview(
  tabIdentifier: "windowtab1",
  sourceFilePath: "MyApp/ContentView.swift",
  previewDefinitionIndexInFile: 0   // 0-indexed; omit for first preview
)
→ returns { previewSnapshotPath: "/var/folders/.../snapshot.png" }
```

After calling RenderPreview, **always Read the returned PNG path** to display the image inline for the user.

If a file has multiple `#Preview` blocks, increment `previewDefinitionIndexInFile` (0, 1, 2…) to target each one.

## Other Useful Tools

| Tool | When to use |
| ---- | ----------- |
| `BuildProject` | Build via Xcode IDE (alternative to XcodeBuildMCP) |
| `GetBuildLog` | Fetch Xcode build output after a failure |
| `GetTestList` | Enumerate all tests before running a subset |
| `RunAllTests` | Run the full test suite via Xcode |
| `RunSomeTests` | Run specific tests by name |
| `XcodeListNavigatorIssues` | List errors/warnings shown in Xcode's Issue Navigator |

### File I/O and Search

Prefer the native `Read`, `Write`, `Edit`, `Grep`, and `Glob` tools over `XcodeRead`, `XcodeWrite`, `XcodeGrep`, etc. — they are faster and don't require a `tabIdentifier`. Only use the Xcode variants if you specifically need Xcode's project-aware file handling.

## xcode Bridge vs XcodeBuildMCP

| Task | Tool |
| ---- | ---- |
| Render SwiftUI Preview | xcode bridge — `RenderPreview` |
| Build & run on simulator | XcodeBuildMCP — `build_run_sim` |
| Run unit/UI tests | XcodeBuildMCP — `test_sim` (works without Xcode open) |
| Take simulator screenshot | XcodeBuildMCP — `screenshot` |
| Get build errors from Xcode navigator | xcode bridge — `XcodeListNavigatorIssues` |
