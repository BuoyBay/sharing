---
title: "sharing typed API"
summary: "Source-derived public signatures, properties, parameters, defaults, and return values."
category: "Reference"
order: 21
types: ["SharingPicker", "SharingRectangle"]
dependencies: []
symbols: ["SharingPicker", "SharingRectangle"]
related: ["api.md", "getting-started.md", "index.md"]
---

# sharing typed API

Generated from the package source declarations. Platform guards are shown where present; inherited members are documented on the base type. See the [API contracts](api.md) for behavior and limitations.

## Sharing functions

### SharingSupported

`Public Function SharingSupported() As Boolean`

No parameters.

#### Returns

| Type |
| --- |
| `Boolean` |

## SharingRectangle

`Sequential Structure SharingRectangle`

### Fields

| Name | Type | Value / Default | Description |
| --- | --- | --- | --- |
| `X` | `Double` | — | — |
| `Y` | `Double` | — | — |
| `Width` | `Double` | — | — |
| `Height` | `Double` | — | — |

## SharingPicker

`Public Class SharingPicker`

Retain this object in the owning window while the native picker/service is in use.

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `Count` | `Integer` | Yes | No | — | — |

### Constructor

`Public Sub Constructor()`

No parameters.

Returns: no value.

### AddText

`Public Sub AddText(value As String)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `value` | `String` | `ByVal` | Required |

Returns: no value.

### AddFile

`Public Sub AddFile(file As FileSystemItem)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `file` | `FileSystemItem` | `ByVal` | Required |

Returns: no value.

### AddWebURL

`Public Sub AddWebURL(value As String)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `value` | `String` | `ByVal` | Required |

Returns: no value.

### Show

`Public Sub Show(anchor As UIControl, x As Double = 0.0, y As Double = 0.0, width As Double = 1.0, height As Double = 1.0)`

Only presents choices; never chooses a destination or claims delivery completion.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `anchor` | `UIControl` | `ByVal` | Required |
| `x` | `Double` | `ByVal` | `0.0` |
| `y` | `Double` | `ByVal` | `0.0` |
| `width` | `Double` | `ByVal` | `1.0` |
| `height` | `Double` | `ByVal` | `1.0` |

Returns: no value.

### Close

`Public Sub Close()`

Dismiss the picker and release its payload. Delivery completion is not reported.

No parameters.

Returns: no value.

### Destructor

`Public Sub Destructor()`

No parameters.

Returns: no value.
