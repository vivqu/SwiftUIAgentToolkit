# Xcode MCP Bridge — Setup

The Xcode MCP bridge (`xcrun mcpbridge`) is built into Xcode 26.3+ and requires no separate installation. It enables capabilities not available in XcodeBuildMCP, most notably **SwiftUI Preview rendering**.

## Enable in Xcode

Open Xcode → **Settings (⌘,)** → **Intelligence** tab → toggle on **"Allow external agents to use Xcode tools"**

## Add to Claude Code

```bash
claude mcp add --transport stdio -s user xcode -- xcrun mcpbridge
```

Verify the connection:

```bash
claude mcp list
```

## Requirements

- Xcode must be **open and running** before starting Claude Code — the bridge connects at startup and cannot reconnect mid-session
- On the first tool call of each session, Xcode shows **"Allow 'claude-code' to access Xcode?"** — click **Allow** (macOS requires re-approval every session for CLI tools)

## Reducing Per-Session Prompts (Optional)

Because Claude Code CLI has no persistent bundle identifier, macOS cannot save the Automation grant and re-prompts every session. To approve once per machine instead, set up `mcp-proxy` as a long-lived bridge process — see the [Swift Forums thread](https://forums.swift.org/t/reducing-the-friction-of-using-xcode-s-mcp-bridge-from-external-coding-agents/85353) for instructions.
