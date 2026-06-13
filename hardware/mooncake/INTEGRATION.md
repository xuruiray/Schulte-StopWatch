# Mooncake Integration

These files are the reusable Schulte app module:

```text
main/apps/app_schulte/
main/assets/images/icon_schulte.c
```

To install it into `M5StopWatch-UserDemo`, copy those paths into the firmware
repository and apply the following integration points.

## App Registration

Add the app include to `main/apps/apps.h`:

```cpp
#include "app_schulte/app_schulte.h"
```

Register the app in `main/main.cpp`, for example after `AppRatchet` and before
`AppSetup`:

```cpp
GetMooncake().installApp(std::make_unique<AppSchulte>());
```

## Icon Declaration

Declare the launcher icon in `main/assets/assets.h`:

```cpp
LV_IMG_DECLARE(icon_schulte);
```

## Center-Out Flush Hook

The Schulte app enables a temporary center-out flush mode while it is open:

```cpp
GetHAL().setCenterOutFlushEnabled(true);
```

and disables it on close:

```cpp
GetHAL().setCenterOutFlushEnabled(false);
```

The host firmware must therefore expose this method in `main/hal/hal.h` and
implement it in `main/hal/hal_display.cpp`. In the source project this was added
as a small atomic flag used by `lvgl_flush_cb` to write large refresh areas from
the center band outward. If the host firmware does not need this transition
effect, remove the two calls from `app_schulte.cpp`.

## Dependencies

The app uses existing StopWatch firmware facilities:

- Mooncake app lifecycle.
- `apps/common/key_manager/key_manager.h`.
- `hal/hal.h` for touch, audio, vibration, and LVGL locking.
- `assets/assets.h` for the launcher icon.
- `smooth_lvgl.hpp`, `smooth_ui_toolkit`, and `uitk` wrappers.
- `tools/random/random.hpp`.

It is not a standalone ESP-IDF firmware project by itself.
