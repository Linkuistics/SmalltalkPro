# SmalltalkPro TODO

This project is pre-development. The following steps outline how to bootstrap SmalltalkPro as a native macOS Pharo Smalltalk IDE. Each item is an actionable prompt for Claude Code.

## Project Scaffolding

- [ ] Set up the project directory structure: `src/` for Pharo Smalltalk source (Tonel format), `frontend/` for Lit Web Components and Monaco editor, and a top-level build script. Follow the same conventions as RacketPro where applicable.

- [ ] Create a minimal Pharo Smalltalk image setup script that installs base packages, configures a headless Pharo VM, and starts a JSON message loop on stdin/stdout for communication with the frontend.

- [ ] Set up the frontend scaffold: create `frontend/index.html` with an import map for Lit and Monaco ESM bundles (vendored, no build step), and a minimal `frontend/core/bridge.js` that can send/receive JSON messages via a WebKit message handler.

## APIAnyware Integration

- [ ] Add APIAnyware-MacOS as a dependency. Write a minimal Pharo Smalltalk program that uses APIAnyware bindings to create a native macOS window with an embedded WKWebView loading `frontend/index.html`.

- [ ] Implement the WebKit bridge layer: Pharo sends JSON messages to the frontend via `WKWebView evaluateJavaScript:`, and the frontend sends messages back via `window.webkit.messageHandlers`. Confirm bidirectional communication works with a ping/pong test.

## Core Editor

- [ ] Integrate Monaco editor into the frontend. Create a `frontend/core/primitives/editor.js` Lit Web Component that wraps Monaco with Smalltalk syntax highlighting and basic keybindings (print-it, inspect-it, do-it).

- [ ] Implement method open/save: the frontend sends `editor:open` and `editor:save` messages to Pharo, which reads/writes methods in the live image and returns source text.

## Workspace and REPL

- [ ] Implement a Workspace panel as a Lit Web Component (`frontend/core/primitives/workspace.js`). It should send `workspace:doIt`, `workspace:printIt`, and `workspace:inspectIt` messages to the Pharo backend and display results.

- [ ] Add auto-completion for the Workspace by querying Pharo's `SystemNavigation` for class names, selectors, and instance variable names in the current context.

## Live Object Environment

- [ ] Implement the image browser: query Pharo's `SystemNavigation` for packages, classes, protocols, and methods. Display a hierarchical browser (system browser layout) as a Lit Web Component with four-pane navigation.

- [ ] Implement the object inspector: send an `inspector:inspect` message with an object reference to Pharo, use `instVarNames` and `instVarAt:` to return instance variable names and values, and render a navigable tree view in the frontend.

- [ ] Implement the class hierarchy viewer: query Pharo's `Behavior` hierarchy (`subclasses`, `superclass`) and display an interactive tree showing the full inheritance chain for any selected class.

## Senders, Implementors, and Method Finder

- [ ] Implement senders/implementors search: send `search:senders` or `search:implementors` messages with a selector to Pharo, use `SystemNavigation allSendersOf:` and `allImplementorsOf:`, and display results in a navigable list panel.

- [ ] Implement the method finder: accept input/output example pairs in the frontend, send them to Pharo's `MethodFinder`, and display matching selectors with their implementing classes.

## Debugging

- [ ] Implement the live debugger: when Pharo raises an exception, serialize the stack frames (method name, receiver, arguments, temporaries, source location) as JSON. Display an interactive stack view in the frontend that supports frame inspection, expression evaluation in context, and method restart.

- [ ] Implement hot-swap code editing in the debugger: allow the user to edit a method in the debugger panel, send the updated source to Pharo for recompilation via `compile:classified:`, and restart the method from the modified frame.

## Message Tracing

- [ ] Implement message-passing visualization: use Pharo's `MessageTally` or `MethodWrappers` to trace message sends for a given expression. Serialize the call tree as JSON and render it as an interactive sequence diagram or call graph in the frontend.

## Refactoring

- [ ] Implement basic refactoring operations: rename class, rename method, extract method, inline method, push up, push down. Use Pharo's built-in `RBRefactoring` framework, send refactoring requests from the frontend, execute them in the image, and report changed methods back to the frontend for display.

## Native App Packaging

- [ ] Create a macOS .app bundle for SmalltalkPro using APIAnyware's packaging support. Include the Pharo VM and base image, frontend assets, and an Info.plist with appropriate metadata.
