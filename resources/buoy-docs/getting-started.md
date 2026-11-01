---
title: "Native sharing getting started"
summary: "Install sharing and use its native API with explicit ownership."
category: "Guides"
order: 10
keywords: ["sharing", "picker", "text", "files", "urls"]
related: ["index.md", "api.md", "typed-api.md"]
---

# Getting started

Copy the sealed package into `packages/` and import `sharing`. Build and retain a payload on the UI thread, as in this helper. In a button action, call `picker.Show(button)` using a visible control inside a visible window. Keep the returned picker in a window property and close it when the window closes. The helper itself presents no UI and sends nothing.

```buoy
Import sharing

Function CreateTextShare(text As String) As SharingPicker
    If Not SharingSupported() Then Throw New UnsupportedOperationException("Sharing needs macOS 13 or newer")
    Dim picker As New SharingPicker()
    Try
        picker.AddText(text)
        Return picker
    Catch e As Exception
        picker.Close()
        Throw e
    End Try
End Function
```

## Handle native constraints

Empty text, Nil/missing files, and invalid web URLs are rejected. Web URLs must have an HTTP(S) scheme and host, with no credentials or control characters. `Show` requires a nonempty payload, a visible anchor in a visible window, positive dimensions, and finite bounded coordinates in the anchor’s local space. Presentation is not delivery confirmation: selection, cancellation, and completion callbacks are not exposed. Keep file access grants valid through the service handoff.

[Package overview](index.md) · [API reference](api.md)
