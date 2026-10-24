# iOS / Swift / Apple platforms

Prefer Swift and Apple-platform examples. Be precise about API availability and Swift version. Swift Evolution proposals are the best source for the "why it's this way" part of the theory.

## Practice workspace: one Swift package with tests

Most topics fit in a single package, which serves as the "one playground" for the topic:

```
~/Learning/ios/<topic-slug>/
├── README.md
├── Package.swift
├── Sources/<Module>/
│   ├── Playground.swift          # free exploration via #Playground blocks
│   └── Exercises/01_<Name>.swift # one file per task, stub + task description
└── Tests/<Module>Tests/
    └── 01_<Name>Tests.swift      # Swift Testing (`import Testing`, `@Test`, `#expect`)
```

- `Package.swift`: `// swift-tools-version: 6.2`, `platforms: [.iOS(.v26), .macOS(.v26)]` so `swift test` runs on the Mac and SwiftUI previews work in Xcode.
- `Playground.swift`: `import Playgrounds` and a few `#Playground { ... }` blocks with the theory snippets, so the user can poke at them in Xcode's canvas.
- Each exercise file starts with a doc comment: the task, the constraints, and what concept it trains. Below it, a **compiling stub** that fails the tests. Stubs must return a placeholder value or throw, never `fatalError()`, because a crash kills the whole test run and hides the other results.
- Tests check behavior, not implementation details. Name them so a failing test name tells the user what's wrong.
- "Predict / explain" answers go in the README or a comment in the exercise file.
- Before handing over, run `swift build --build-tests` and fix anything that fails. The user should get a project that compiles, with failing tests as the only "errors".

Good "find the defect" material: a data race, a retain cycle, wrong actor isolation, a view that re-renders too much. Good "build" tasks: a cache, a rate limiter, a view model, a small async pipeline.

### When a package isn't enough

Some topics need a running app: app/scene lifecycle, UIKit view controller lifecycle, push notifications, background tasks, entitlements, App Intents. For those:

1. Check for `xcodegen` or `tuist`. If either is available, generate an iOS app project in the topic folder.
2. Otherwise, ask the user to create the project in Xcode (File → New → Project → App, saved into the topic folder). Then add files to its folders directly: Xcode 16+ projects use synchronized folders, so new files are picked up without editing `project.pbxproj`.

Pure SwiftUI topics usually don't need an app: SwiftUI views with `#Preview` work inside the package.

For iOS-adjacent topics that aren't a Swift API (networking, app architecture, build system, code signing), still prefer runnable practice in Swift where it fits; otherwise use written scenarios and design tasks in the README.

## Review

Run `swift test`, then read the code. Check idiom against the global Swift/SwiftUI guidelines as well as correctness.

## Sources

- **Official:** Apple Developer Documentation, The Swift Programming Language book (docs.swift.org), Swift Evolution proposals (github.com/swiftlang/swift-evolution), WWDC sessions (developer.apple.com/videos), Apple sample code.
- **Further reading:** Swift by Sundell, SwiftLee (Antoine van der Lee), Hacking with Swift, Donny Wals, Point-Free, objc.io, swift.org forums threads, and books where relevant.

Verifying Apple links:
- If the Xcode MCP is connected, use `DocumentationSearch` for Apple APIs.
- Apple docs are JS-rendered and fetch badly; to read them, replace `developer.apple.com` with `sosumi.ai` in the URL (e.g. `https://sosumi.ai/documentation/swift/actor`). Give the user the regular `developer.apple.com` link.
