# Rexy Bridge 3.2.0-beta

Camera-discovery and drone-control improvements, plus a fix for the sluggishness some setups saw before Scan → Apply.

**[Install & UE setup guide](GETTING_STARTED.md) · [User guide](USER_GUIDE.md) · [Print / greyscale guide](USER_GUIDE-light.pdf)**

## New

- **Rename-safe camera scan** — Scan UE now finds Cine Camera Actors and CameraRig_Crane rigs by their **class**, not their name. If you'd renamed a camera or crane in the Outliner, the old scan could miss it; now it's found whatever it's called. (Default-named actors still use the fast path, so there's no slowdown.)
- **Drone World / Camera frame** — in Drone mode a **World / Camera** toggle appears by the mode buttons. **World** flies along the world grid (like Dolly); **Camera** makes left/right and forward/back follow where the camera is pointing, staying level with the ground, while up/down stays vertical — classic FPV-drone feel.

## Fixes

- **No more requests to unresolved template paths.** Before a Scan → Apply, the bridge used to keep firing Remote Control writes at the placeholder `<YOUR_…>` actors from the first-run template. Every one failed, which showed up as log spam in UE and occasional sluggishness (settings slow to change, crane not driving). The bridge now skips any unresolved path, so those symptoms are gone.

## Updating

Run `RexyBridge-Setup-3.2.0-beta.exe` over your current install, or just click **Check for updates** in the top bar if you're already on 3.1.0-beta or newer.

## Known notes

- **Unsigned installer** — SmartScreen warns on first run: **More info → Run anyway**.
- Requires **Unreal Engine 5.3+** with the **Remote Control API** plugin (WebSocket port `30020`).
- **Drone dimension limits** (floor/ceiling + bounds) are still in progress — the up/down limit shown in Drone mode is not yet a distance clamp.
- Beta — report anything odd via an **Issue** or **rob@realprogear.com**.
