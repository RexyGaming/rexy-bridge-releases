# Rexy Bridge 3.5.0-beta

The safe-limits release: **Soft Stops** ships in full — per-parameter limits with feathered deceleration that hold on absolute *and* velocity moves — alongside a real-world **Camera Box** that can follow the crane base, a **crane height limit** worked out with trig, and the same **signal calibration + Filter Lab** every input now gets, not just the wheels.

**[Install & UE setup guide](GETTING_STARTED.md) · [User guide](USER_GUIDE.md) · [Print / greyscale guide](USER_GUIDE-light.pdf)**

## New

- **Soft Stops — per-parameter limits, now for everything.** Set a Min and Max on any control and the camera eases into the wall instead of hitting it (a per-stop **Feather** sets how gently). Each stop is independent, master-switchable, saved **per camera**, and every stop has a **live** button that captures the parameter's current value, plus **Stop → Min / Max** to snap every enabled limit to where the camera is right now.
  - **Absolute moves** — pan / tilt / roll (absolute wheel mode), focus / iris / zoom, crane yaw / scope / pitch, and crane base X/Y/Z are clamped at the value.
  - **Velocity moves** — continuous ("Relative") wheels and the relative crane base are now walled too. The bridge tracks the accumulating position/angle on a shadow it seeds from the rig, and feathers the *rate* into the limit, so an endless-rotation pan decelerates and stops at your degree limit and reverses straight back out.
  - **At the limit** — the axis being limited flashes a **STOP** on its card and its slider pins to the wall, so the panel always matches the real rig. The internal command stops dead at the limit rather than winding up past it, so the moment you back off the move reverses instantly.
- **Camera Box — a real-world safe volume.** Independent world **X / Y / Z** limits (cm), each with its own feather, enforced live in dolly and drone. New this release:
  - **Zero offset (X/Y/Z)** — shift the whole box away from world zero so it sits wherever your set does.
  - **Follow crane base** — lock the box's zero to the crane base's live position, so the box *travels with the base*: a crane-local safe envelope for free.
- **Crane height limit — pure trig, no lag.** With the box Z axis on in crane mode, the bridge caps the camera's height from `ArmLength × sin(CranePitch)` — it clamps scope and pitch against each other so the camera eases to your ceiling/floor and holds, whichever you push, and the limited axis flashes STOP. One quick auto-calibration on entering crane mode pins it to your exact rig; after that there are no per-frame reads and no dependence on live feedback from Unreal.
- **FPV drone box.** In pure-FPV flight the Camera Box becomes a *local* envelope — how far you've flown from the FPV origin in the camera's own axes — feathered like the rest.
- **Signal calibration + Filter Lab for every input.** The range/response calibration and the Signal Filter Lab that the gamepad axes had now work for **OSC, MIDI and FreeD** too. Each live input in the Alt Inputs panel gets a **C** button (it reads **C·ƒ** when a filter chain is running, and turns cyan once calibrated) that opens the same wizard — capture min/max/rest, shape the response curve, build a live filter chain, and export a tune-scan.
- **Autolevel.** A bindable action that eases the camera's roll back to level over a set time — offset-independent and roll-only, so it never snaps or fights your position.
- **Per-build version badge.** The badge top-left now increments every dev build, so you can tell at a glance exactly which build is running (hard-reload if it doesn't match).
- **Reset button.** Clears stale saved state (bindings/tuning cache) when a build needs a clean slate.

## Fixes

- **Dolly Pedestal rebuilt to be incremental.** Each grip move now adds a camera-relative step to the live world position, so panning re-orients the next move with no orbit, jump, or fling back to origin. Pedestal is solid.
- **Dolly reach raised to ±10 m.** The camera-move default was silently capped at 5 m; full slider travel now reaches ±10 m (and the readout follows your actual range).
- **Zeroing the camera in dolly re-bases the grip**, so it no longer springs back on the next grip move.
- **Scan is reliable after a reconnect or Reset.** The pose poller yields during a scan and the retry cascade stops cleanly on a timeout, so the reconnect burst no longer congests Unreal into an empty scan.
- **Autolevel no longer snaps.** It's driven incrementally from the live roll rather than writing a whole rotation from a stale value.

## UE 5.8 note (unchanged, still important)

UE 5.8 **blocks remote function calls by default**, which stops Scan UE from listing your level.

**Project Settings → Plugins → Remote Control → Security → tick "Allow Any Remote Function Call".** It is **per-project**; it does **not** travel with the app or config; and if it's already ticked but Scan still finds nothing, **untick it, re-tick it**, then Scan again. Full steps in **GETTING_STARTED.md**.

## Updating

Run `RexyBridge-Setup-3.5.0-beta.exe` over your current install, or click **Check for updates** in the top bar.

## Known notes

- **Unsigned installer** — SmartScreen warns on first run: **More info → Run anyway**.
- Requires **Unreal Engine 5.3+** (5.8 supported) with the **Remote Control API** plugin (WebSocket port `30020`).
- **Velocity soft stops** and the **follow-base / crane-height** limits assume the rig isn't repositioned by hand in Unreal mid-take; if it is, re-enter the mode (continuous wheels, relative base, or crane) to re-seed the shadow.
- **Crane height** caps the vertical only; horizontal reach from the base is still best limited with the **Scope** grip soft stop.
- If a move still looks stepped in a render, check the input itself — a low-resolution or slow-reporting control quantises the move before the bridge sees it. The **Signal Filter Lab** and tune-scan export (now on every input) will show you.
- Beta — report anything odd via an **Issue** or **rob@realprogear.com**.
