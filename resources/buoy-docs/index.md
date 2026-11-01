---
title: "Native sharing"
summary: "Build typed sharing payloads and present the macOS sharing picker."
category: "Overview"
order: 0
keywords: ["sharing", "picker", "text", "files", "urls"]
related: ["getting-started.md", "api.md", "typed-api.md"]
---

# Native sharing

The `sharing` package wraps `NSSharingServicePicker`. Build a typed payload of text, local files, and HTTP(S) URLs, then present choices beside a visible control. Creating a payload does not transmit anything; the user chooses the native service and destination.

## Platform support

Requires macOS 13 or newer, including the native picker close capability. `SharingSupported()` checks that capability. Other platforms report False, and construction throws.

## Ownership and lifetime

Retain the picker in its owning window. Its payload and presentation anchor stay alive with it. After first presentation the payload freezes: reuse that picker for the same items or create another picker to change them. Call `Close()` when the owner closes; it dismisses the picker and releases references, and repeated calls are safe. Use the UI thread for construction and operations. Worker-thread teardown queues cleanup to the main thread.

## Read next

- [Getting started](getting-started.md)
- [API reference](api.md)
