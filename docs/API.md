# Native sharing picker · 0.1.0

Build a typed payload and let the user choose a macOS sharing service.
`Import sharing`. Requires **macOS 13+**, which provides the native picker's
explicit `close` method. `SharingSupported()` checks that capability; other
platforms report false and construction throws.

- `New SharingPicker()` creates an empty payload.
- `AddText(value)`, `AddWebURL(value)` and `AddFile(file)` add text, HTTP(S) URLs or existing local files. `Count` is read-only. Web URLs reject credentials, control characters and missing hosts.
- `Show(anchor As UIControl, x = 0.0, y = 0.0, width = 1.0, height = 1.0)` presents the native picker relative to a visible control in a visible window. Rectangle values are in that control's local coordinate system. Use a direct user gesture, such as a button's Action handler.
- Retain the picker in the owning window. Its native payload and anchor stay alive with it. Do not construct a temporary picker and immediately discard it.
- The payload freezes after first presentation. Reuse the same picker for the same payload, or create a new one to change items.
- `Close()` dismisses the picker and releases native references; it is idempotent and also runs from the destructor. Close explicitly when the owning window closes.

Construction, methods and final release belong on the UI thread. Showing the
picker does not choose a recipient/destination; the package never sends anything
by itself. **Choosing a native service can perform a share**, so present it only
for an explicit user request. Selection, cancellation and delivery-completion
callbacks are not exposed in this first version; do not treat presentation as
successful delivery. File access/sandbox grants must remain valid through the
native service's handoff.

The sealed-package native test verifies payload construction, URL rejection and
idempotent close without presenting UI or invoking a service. Actual picker
presentation and delivery require manual app-level QA.

Apple API: [NSSharingServicePicker](https://developer.apple.com/documentation/appkit/nssharingservicepicker).

Implicit teardown from a worker transfers native pointers and the anchor reference to a main-thread cleanup queue. Keep the application run loop alive until cleanup drains; ordinary picker operations remain main-thread-only.
