# macOS Sharing picker from a typed payload

Build a typed payload and let the user choose a macOS sharing service.
`Import sharing`. Requires **macOS 13+**, which provides the native picker's
explicit `close` method. `SharingSupported()` checks that capability; other
platforms report false and construction throws.

Construction, methods and final release belong on the UI thread. Showing the
picker does not choose a recipient/destination; the package never sends anything
by itself. **Choosing a native service can perform a share**, so present it only
for an explicit user request. Selection, cancellation and delivery-completion
callbacks are not exposed in this first version; do not treat presentation as
successful delivery. File access/sandbox grants must remain valid through the
native service's handoff.

## Install

From a Buoy consumer project with BPM installed:

```sh
bpm add sharing --git https://github.com/BuoyBay/sharing.git --rev refs/heads/main
```

BPM records the resolved commit in its lockfile. Keep that lockfile with the
consumer project for reproducible installs.

## Example

```basic
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

## Platform and scope

Native sharing services require macOS and an appropriate application/UI context.

## Build from source

With the native `build-packages` driver from [devtools](https://github.com/BuoyBay/devtools)
on your `PATH`, run from this checkout:

```sh
build-packages --root "$PWD" --compile-consumer sharing
```

The driver checks source targets and compiles an import consumer. See the
[API guide](docs/API.md) for behavior, limits and any host prerequisites.

## Local Buoy setup

On your own machine, install Buoy and run:

```sh
buoy ai init --both
```

## Contributing

[Contributing](CONTRIBUTING.md) · [License](LICENSE)
