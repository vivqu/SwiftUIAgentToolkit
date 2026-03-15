# Setup

## Requirements

- Claude Code - recommended coding agent
- Cursor - recommended IDE (optional)
- Xcode 18+
- iOS 18+ deployment target
- Swift 5.9+

If using Cursor, we recommend these extensions:

- Claude Code - use CC in the Cursor IDE
- markdownlint - format Markdown files

## Getting Started

1. Clone the repository:

   ```bash
   git clone https://github.com/vivqu/SwiftUIAgentToolkit.git
   ```

2. Download and install Xcode

3. Open Xcode and create a new project inside this folder:
   - Open Xcode → **File → New → Project**
   - Choose **App** under iOS
   - Set your **Product Name**, **Bundle Identifier**, and **Team**
   - Set **Interface** to SwiftUI and **Language** to Swift
   - Set **Testing System** to Swift Testing with XCTest UI Tests
   - Choose SwiftData for **Storage**
   - When prompted to save, **navigate to your cloned folder** and save the `.xcodeproj` there

4. Set the deployment target:
   - Select your project in the Xcode navigator
   - Under **General → Minimum Deployments**, set iOS to **18.0**

## Agent verification tools

This section describes how to set up the tools
to enable the agent to verify the correctness of
your mobile app.

1. Setup Xcode MCP

Apple ships a built-in MCP bridge starting in Xcode 26.3. It requires no separate installation — just register it with your agent.

> **Note:** The Xcode MCP may be useful for working with SwiftUI Previews, which XcodeBuildMCP does not support.

**Claude Code**:

```bash
claude mcp add --transport stdio xcode -- xcrun mcpbridge
```

Verify the connection:

```bash
claude mcp list
```

**Cursor**:

Add to `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "xcode": {
      "command": "xcrun",
      "args": ["mcpbridge"]
    }
  }
}
```

Restart Cursor to pick it up. Verify the connection in **Cursor → Settings → MCP** — xcode should appear with a green checkmark.

2. Setup XcodeBuildMCP

This is a third-party tool that works with any Xcode version. The skills and plugins for SwiftUIAgentToolkit currently utilize this tool.

[XcodeBuildMCP](https://github.com/cameroncooke/XcodeBuildMCP) lets AI coding agents build and run your app directly.

**Claude Code**:

Add to user config so it's available in all projects:

```bash
claude mcp add XcodeBuildMCP -s user -- $(which node) $(npm root -g)/xcodebuildmcp/build/cli.js mcp
```

Verify the connection:

```bash
claude mcp list
```

**Cursor**:

Install in the Cursor global user config at `~/.cursor/mcp.json`. This will enable XcodeBuildMCP to run on all projects and sessions.

```json
{
  "mcpServers": {
    "XcodeBuildMCP": {
      "command": "/path/to/node",
      "args": ["<npm root -g>/xcodebuildmcp/build/cli.js", "mcp"]
    }
  }
}
```

Restart Cursor to pick it up. Verify the connection in **Cursor → Settings → MCP** — XcodeBuildMCP should appear with a green checkmark.

## Project Structure

After setup your folder should look like:

```none
MyAppProject/
├── YourApp/
|   ├── YourApp.xcodeproj
│   └── (generated Swift source files)
├── CLAUDE.md
├── .claude/
└── docs/
```
