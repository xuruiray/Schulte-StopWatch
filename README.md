# Schulte-StopWatch

Circular Schulte grid app extracted from the M5Stack StopWatch firmware work.

This repository contains two related parts:

- `web/`: standalone HTML prototype for interaction and visual iteration.
- `hardware/mooncake/`: Mooncake/LVGL Schulte app source and launcher icon asset.

## Web Prototype

Open the page directly in a browser:

```bash
open web/index.html
```

The prototype mirrors the device interaction model:

- Idle: empty circular grid with the selected grid count in the center.
- Left key: start, or clear while running/result is shown.
- Right key: switch grid count in idle state.
- Running: tap numbers in order; correct and incorrect taps use different feedback.
- Result: only elapsed time is shown.

## Hardware App

The hardware app source is stored under the same path shape used by the
StopWatch firmware:

```text
hardware/mooncake/main/apps/app_schulte/
hardware/mooncake/main/assets/images/icon_schulte.c
```

It is intended to be copied into `M5StopWatch-UserDemo` and registered in the
Mooncake app list. See `hardware/mooncake/INTEGRATION.md` for the integration
points that are required outside the app folder.

## Source

Extracted from commit `6963aab` in `xuruiray/M5StopWatch-UserDemo`.

## License

MIT. See `LICENSE`.
