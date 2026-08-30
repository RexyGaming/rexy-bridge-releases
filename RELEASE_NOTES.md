# Rexy Bridge 3.6.0-beta

The many-wheels release: read **every** Rexy device at once, at full **16-bit** resolution, straight into the bridge — past the 4-controller ceiling the browser was imposing.

**[Install & UE setup guide](GETTING_STARTED.md) · [User guide](USER_GUIDE.md) · [Print / greyscale guide](USER_GUIDE-light.pdf)**

## New

- **SDL input mode — 16-bit, many devices.** A new toggle in the Gamepad Debug panel — **"SDL 16-bit · multi"** — switches the bridge from the browser gamepad API to reading joysticks **directly in its main process** via SDL. Two big wins:
  - **Full 16-bit resolution.** The browser gamepad API was quantising the Rexy wheels down to 8-bit (1/127 steps); SDL passes the wheels' true 16-bit values (~65,000 steps) straight through, which is what removes the last of the fine-motion stepping.
  - **More than 4 devices.** The browser Gamepad API caps at 4 controllers; SDL has no such limit, so you can drive the bridge from many Rexy devices at once.

  Calibration, null-drift and the live debug view all read the SDL devices too, so a wheel calibrated in SDL mode captures full resolution. Needs the installed desktop app (SDL runs in the bridge's main process). Device numbering differs from the browser, so **re-bind your axes after switching** sources.
- **SDL / USB axis scan.** A **"⤓ Scan (SDL)"** button reads a wheel via the main-process SDL path and reports true resolution (step size / implied code count) and the real device report rate — bypassing the browser's ~60 fps read-lock — for verifying wheel firmware.
- **Raw 16-bit code in the calibration wizard.** The `raw` readout now shows the normalised value **plus the ~16-bit device code (×32767)**, so you can read the actual code and tell 8-bit from 16-bit at a glance as you move an axis.

## Fixes

- **Signal Filter Lab capture** now draws in the same orientation as the live waveform (newest at the left) — it had been showing the frozen capture mirrored.

## UE 5.8 note (unchanged, still important)

UE 5.8 **blocks remote function calls by default**, which stops Scan UE from listing your level.

**Project Settings → Plugins → Remote Control → Security → tick "Allow Any Remote Function Call".** It is **per-project**; it does **not** travel with the app or config; and if it's already ticked but Scan still finds nothing, **untick it, re-tick it**, then Scan again. Full steps in **GETTING_STARTED.md**.

## Updating

Run `RexyBridge-Setup-3.6.0-beta.exe` over your current install, or click **Check for updates** in the top bar.

## Known notes

- **SDL input mode needs the installed desktop app** — SDL reads USB devices in the bridge's main process, so a remote browser panel on another device can't use the host machine's wheels (it can still drive everything else over the network).
- **Re-bind after switching input source** — Browser and SDL number devices differently, so bindings made under one won't line up under the other.
- **Unsigned installer** — SmartScreen warns on first run: **More info → Run anyway**.
- Requires **Unreal Engine 5.3+** (5.8 supported) with the **Remote Control API** plugin (WebSocket port `30020`).
- If a move still looks stepped in a render on the browser input path, that's the 8-bit quantisation — switch to **SDL input mode** for full 16-bit, or use the **Signal Filter Lab** / tune-scan export to see the raw device signal.
- Beta — report anything odd via an **Issue** or **rob@realprogear.com**.
