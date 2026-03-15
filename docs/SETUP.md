# Setup

## Requirements

- Xcode 16+
- iOS 18+ deployment target
- Swift 5.9+

## Getting Started

1. Clone the repository:
   ```bash
   git clone https://github.com/vivqu/SwiftUIAgentToolkit.git MyAppName
   cd MyAppName
   ```

2. Open Xcode and create a new project inside this folder:
   - Open Xcode → **File → New → Project**
   - Choose **App** under iOS
   - Set your **Product Name**, **Bundle Identifier**, and **Team**
   - Set **Interface** to SwiftUI and **Language** to Swift
   - When prompted to save, **navigate to your cloned folder** and save the `.xcodeproj` there

3. Set the deployment target:
   - Select your project in the Xcode navigator
   - Under **General → Minimum Deployments**, set iOS to **18.0**

4. Open the project:
   ```bash
   open YourApp.xcodeproj
   ```

## Project Structure

After setup your folder should look like:
```
MyAppName/
├── YourApp.xcodeproj
├── YourApp/
│   └── (generated Swift source files)
├── CLAUDE.md
├── .claude/
└── docs/
```

## Running Tests

In Xcode: `Cmd+U`
