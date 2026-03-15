# XcodeBuildMCP Session Setup

**Skip this entire section if `session_show_defaults` already shows project/workspace, scheme, and simulator all set.**

Otherwise, run the following steps using `XcodeBuildMCP` tools:

1. Call `list_sims` and confirm at least one iOS 18+ simulator exists. If none, stop and tell the user to install one in Xcode.
2. From the iOS 18+ results, find any with state **Booted**. If exactly one is booted, call `session_set_defaults` to use it. If multiple are booted, show the list and ask the user to pick one, then call `session_set_defaults`. If none are booted, continue — the build tool will boot one.
3. Call `session_show_defaults`. If `projectPath` or `workspacePath` is missing, call `discover_projs` using the workspace root. If exactly one project or workspace is found, call `session_set_defaults` to set it. If multiple are found, show the list and ask the user to pick one. If none are found, stop and tell the user no Xcode project was found.
4. If `scheme` is still missing after setting the project, call `list_schemes` and set the first result via `session_set_defaults`. If multiple schemes exist, show the list and ask the user to pick one.
