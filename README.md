# SmalltalkPro

> A Smalltalk IDE from Linkuistics -- professional tools for programming language ecosystems.

---

**Status: Pre-development.** This project is in the planning stage. No code has been written yet. The design and feature list below describe the intended product.

---

SmalltalkPro will be a native macOS IDE for Pharo Smalltalk, written in Pharo Smalltalk, using [APIAnyware-MacOS](https://github.com/linkuistics/APIAnyware-MacOS) bindings for native macOS APIs, with WebKit as a UI layer and Monaco as the code editor.

## Why a Dedicated Smalltalk IDE?

Smalltalk is unlike every other language in this family. There are no source files -- the entire program lives in a mutable image, and the IDE *is* the runtime. Pharo ships with its own IDE, but it runs in a custom VM with its own windowing system. SmalltalkPro aims to bring Smalltalk's live programming model to macOS as a first-class native application, with modern editor features and full platform integration.

## Planned Features

### Live Object Environment

- **Image browser** -- navigate and edit the live class hierarchy, methods, and categories
- **Object inspector** -- inspect any live object, traverse instance variables, evaluate expressions in context
- **Workspace** -- evaluate Smalltalk expressions with immediate feedback: print-it, inspect-it, do-it
- **Message-passing visualization** -- trace message sends through the system

### Class & Method Tools

- **System browser** -- hierarchical navigation of packages, classes, protocols, and methods
- **Method finder** -- search by name, by example (input/output pairs), or by selector
- **Senders and implementors** -- find all senders of a message or all classes implementing a method
- **Refactoring tools** -- rename, extract method, push up/down, inline, with live image updates

### Debugging

- **Live debugger** -- inspect and modify stack frames, restart methods, hot-swap code mid-execution
- **Condition system integration** -- handle errors interactively without unwinding the stack

### Native macOS Integration

- Built entirely on APIAnyware-MacOS bindings -- message-passing OO API style
- Direct WebKit access from Smalltalk (no Tauri or Electron -- APIAnyware provides everything)
- Native menus, window management, system integration

## Planned Architecture

```
Frontend (Lit Web Components + Monaco)
    ↕ WebKit bridge (via APIAnyware bindings)
Pharo Smalltalk (live image, class browser, inspector, debugger)
    ↕ APIAnyware-MacOS bindings
macOS platform APIs (AppKit, WebKit, Foundation)
```

The Pharo image will be the source of truth. The frontend renders views of the live image state, and user actions are sent back to Pharo for execution.

Each *Pro IDE is itself a proof that APIAnyware bindings are complete enough to build a real native application -- no FFI escape hatches or platform-specific shims required.

## Related Projects

- **[APIAnyware-MacOS](https://github.com/linkuistics/APIAnyware-MacOS)** -- provides the native macOS API bindings (message-passing OO style)
- **[TestAnyware](https://github.com/linkuistics/TestAnyware)** -- GUI testing in macOS VMs

### Sibling IDEs

Each language in the APIAnyware family has its own dedicated IDE, purpose-built for that language's paradigm:

[RacketPro](https://github.com/linkuistics/RacketPro) ·
[ChezPro](https://github.com/linkuistics/ChezPro) ·
[GerbilPro](https://github.com/linkuistics/GerbilPro) ·
[ClozurePro](https://github.com/linkuistics/ClozurePro) ·
[SteelBankPro](https://github.com/linkuistics/SteelBankPro) ·
[HaskellPro](https://github.com/linkuistics/HaskellPro) ·
[IdrisPro](https://github.com/linkuistics/IdrisPro) ·
[MercuryPro](https://github.com/linkuistics/MercuryPro) ·
[PrologPro](https://github.com/linkuistics/PrologPro)

## License

Apache-2.0
