# Setup

## Requirements

- Xcode 16+
- iOS 18+ deployment target
- Swift 5.9+

## Getting Started

1. Clone the repository:
   ```bash
   git clone https://github.com/vivqu/SwiftUIAgentToolkit.git
   cd SwiftUIAgentToolkit
   ```

2. Open in Xcode:
   ```bash
   open SwiftUIAgentToolkit.xcodeproj
   ```
   Or if using Swift Package Manager:
   ```bash
   open Package.swift
   ```

3. Select a simulator target (iPhone 16 or later) and build with `Cmd+B`.

## Dependencies

Dependencies are managed with Swift Package Manager. Xcode will resolve them automatically on first build.

## Running Tests

In Xcode: `Cmd+U`

Or from the command line:
```bash
xcodebuild test -scheme SwiftUIAgentToolkitTests -destination 'platform=iOS Simulator,name=iPhone 16'
```
