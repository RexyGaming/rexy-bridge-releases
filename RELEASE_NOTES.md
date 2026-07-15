# Rexy Bridge 3.1.0-beta

The 3.1 beta — a big step up from the first public beta. Adds in-app updating, a full signal-filter workbench, a light theme, and a print edition of the manual, plus a batch of fixes.

**[Install & UE setup guide](GETTING_STARTED.md) · [User guide](USER_GUIDE.md) · [Print / greyscale guide](USER_GUIDE-light.pdf)**

## New

- **Check for updates** — a button in the top bar checks the release server on demand, downloads a newer build in the background, and offers **Restart to update**. It never checks automatically on launch, so it can't interrupt a session. (From this version on, future updates are one click — no reinstalling.)
- **Signal Filter Lab** (in the calibration wizard) — capture a live axis waveform, audition nine filters (median, moving-average, EMA, double-EMA, Kalman, 1-Euro, Hampel, deadband, slew) on a 3×3 preview grid, and **chain them live** so the cleaned signal drives UE in real time. Every filter has editable parameters and an ⓘ explainer. Save/load named **filter sets** to reuse across axes and machines.
- **Live input + output waveforms** on the tuning page — raw device signal and the filtered-and-curved output (in calibrated cyan) side by side, in sync.
- **Axis scan tools** — a raw-axis capture in Gamepad Debug and a tuning-page scan that logs raw + filtered + output to JSON with a noise-reduction figure, for diagnosing input devices.
- **Light theme** — a Dark / Light toggle in the top bar (pale blue-grey background, dark text, accent colours preserved).
- **Print / greyscale user guide** — `USER_GUIDE-light.pdf`, a light-background, mono-friendly edition of the manual for printing.

## Fixes

- FreeD / UE output toggle switches correctly.
- Rebuilt the per-axis calibration wizard (min/max/rest capture + response curve); the min marker is now Rexy pink so it's easy to tell from the blue max marker.
- Light theme: Filter Lab parameter boxes no longer render dark-on-dark.
- MIDI input re-enabled; OSC-in port/prefix/range settings apply.
- Stopping a MoCo recording no longer errors; STOP holds the playhead in place.
- Various smaller fixes across input handling.

## Updating

Run the new `RexyBridge-Setup-3.1.0-beta.exe` over the top of your current install — no need to uninstall. Bindings, filter sets, lens boxes and theme are kept (they live in `%AppData%\Roaming\RexyBridge`). After this build, use the in-app **Check for updates** button instead.

## Known notes

- **Unsigned installer** — Windows SmartScreen warns on first run: **More info → Run anyway**. Code signing comes later; auto-update works unsigned but shows the same warning.
- Requires **Unreal Engine 5.3+** with the **Remote Control API** plugin (WebSocket port `30020`).
- **Camera scan** currently matches Cine Camera Actors / cranes by name; if a scan finds nothing, check the actor is a Cine Camera Actor and (for cranes) that the camera is parented to it. A class-based scan that ignores names is coming next.
- Beta — please report anything odd via an **Issue** or to **rob@realprogear.com**.
