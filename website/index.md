---
title: SmalltalkPro
---

SmalltalkPro will be a native macOS IDE for Pharo Smalltalk, written in Pharo Smalltalk,
using [APIAnyware-MacOS](https://github.com/linkuistics/APIAnyware-MacOS) bindings for
native macOS APIs, with WebKit as a UI layer and Monaco as the code editor.

Smalltalk is unlike every other language in this family. There are no source files — the
entire program lives in a mutable image, and the IDE *is* the runtime. SmalltalkPro aims
to bring Smalltalk's live programming model to macOS as a first-class native application,
with modern editor features and full platform integration.

Planned tools include a system browser, live debugger with hot-swap support, object
inspector, workspace, method finder, and refactoring tools — all running against the live
Pharo image via APIAnyware-MacOS bindings. No Electron, no Tauri; native macOS throughout.
