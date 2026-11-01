---
title: "Native sharing API"
summary: "Public symbols and contracts for the sharing package."
category: "Reference"
order: 20
keywords: ["sharing", "picker", "text", "files", "urls"]
symbols: ["SharingSupported", "SharingPicker", "SharingPicker.AddText", "SharingPicker.AddFile", "SharingPicker.AddWebURL", "SharingPicker.Show", "SharingPicker.Count", "SharingPicker.Close"]
related: ["index.md", "getting-started.md", "typed-api.md"]
---

# API reference

Import `sharing` from the sealed package. The signatures below describe its public surface.

| Symbol | Contract |
| --- | --- |
| `SharingSupported() As Boolean` | Check platform and native close capability. |
| `New SharingPicker()` | Create an empty editable payload. |
| `Count As Integer` | Read-only number of payload items. |
| `AddText(value As String)` | Append nonempty text before first presentation. |
| `AddFile(file As FileSystemItem)` | Append an existing local file. |
| `AddWebURL(value As String)` | Append a validated HTTP(S) URL. |
| `Show(anchor As UIControl, x = 0.0, y = 0.0, width = 1.0, height = 1.0)` | Present choices relative to the anchor control; Double rectangle arguments. |
| `Close()` | Dismiss and release the picker; permanently close this object. |

## Errors and lifecycle

Empty text, Nil/missing files, and invalid web URLs are rejected. Web URLs must have an HTTP(S) scheme and host, with no credentials or control characters. `Show` requires a nonempty payload, a visible anchor in a visible window, positive dimensions, and finite bounded coordinates in the anchor’s local space. Presentation is not delivery confirmation: selection, cancellation, and completion callbacks are not exposed. Keep file access grants valid through the service handoff.

Retain the picker in its owning window. Its payload and presentation anchor stay alive with it. After first presentation the payload freezes: reuse that picker for the same items or create another picker to change them. Call `Close()` when the owner closes; it dismisses the picker and releases references, and repeated calls are safe. Use the UI thread for construction and operations. Worker-thread teardown queues cleanup to the main thread.

## Platform support

Requires macOS 13 or newer, including the native picker close capability. `SharingSupported()` checks that capability. Other platforms report False, and construction throws.

[Getting started](getting-started.md) · [Package overview](index.md)


[Full typed API: properties, parameters, defaults, and returns](typed-api.md)
