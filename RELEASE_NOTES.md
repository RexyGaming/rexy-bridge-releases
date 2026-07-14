# Rexy Bridge 3.0.0-beta.1

First public beta of Rexy Bridge v3. Windows installer, driving Unreal Engine 5 cine cameras and crane rigs live.

**[Install & UE setup guide](GETTING_STARTED.md) · [Full user guide](USER_GUIDE.md)**

## Highlights

- **One-click Windows installer** — the app, the UE bridge, and the gamepad reader are all bundled. No Node or Python to install.
- **Auto camera discovery** — hit **⌕ Scan UE** to find every Cine Camera Actor and crane in your level. No RexyControl preset, no `mappings.json` editing.
- **Lens boxes & favourites** — build named lens kits, cycle them with bindable **Wider / Tighter** buttons, and jump to favourite lenses from bound keys. Boxes export/import on their own.
- **Focus / Iris / Zoom tuning** — full sensitivity / curve / deadband / feather control, matching the head and grip axes. Custom-lens min-focus follows your ft/in ↔ m/cm preference.
- **Virtual MoCo upgrades** — bindable transport (Rec / Stop / Play / Home / Mark), a bindable **jog shuttle** to scrub the playhead from hardware, **mark all tracks** at once, S-curve editing on marked-but-unrecorded tracks, and auto-erase of marks when you record over a track. Stop now holds the playhead in place.
- **More input sources** — MIDI (knobs, faders, notes, pitch-bend) and configurable OSC input, both bindable exactly like gamepads. A 10-second OSC capture tool exports a JSON log for diagnosing devices.
- **Per-axis calibration wizard** — capture an axis's true min/max/rest and shape its response curve, plus the quick 5-second null-drift for resting stick/wheel drift.
- **Speed control on keys** — the **S** value now works for keyboard/button bindings too, so key-driven moves have adjustable speed, curve, and feather.

## Known notes

- **Unsigned installer.** Windows SmartScreen will warn on first run — **More info → Run anyway**. Code signing comes later.
- Requires **Unreal Engine 5.3+** with the **Remote Control API** plugin enabled (WebSocket port `30020`).
- This is a beta — please report anything odd via an **Issue** or to **rob@realprogear.com**.
