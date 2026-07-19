# Rexy Bridge 3.4.0-beta

The grip modes release: proper flight frames for Drone, Crab/Pedestal for Dolly, crane pan-stabilise, and an invisible crane — plus two long-standing control-feel bugs fixed.

**[Install & UE setup guide](GETTING_STARTED.md) · [User guide](USER_GUIDE.md) · [Print / greyscale guide](USER_GUIDE-light.pdf)**

## New

- **Drone flight frames — Cine / Cine-FPV / FPV.** Replaces the old World/Camera toggle with three distinct feels:
  - **Cine** — flies on the world grid; aim the camera independently.
  - **Cine/FPV** — left/right and forward/back follow where the camera is *panned*, but stay **parallel to the ground** whatever the tilt or roll, and up/down is a **true vertical** jib. Tilt 45° down and forward still travels flat; roll the camera and left/right still tracks level.
  - **FPV** — everything relative to the camera body, so up/down rides the roll and tilt.
- **⟳ Reset grid** — re-snaps the Cine/FPV ground grid to the camera's current pan heading if it ever drifts out of sync.
- **Dolly Crab / Pedestal.** **Crab** moves the camera on the world grid (the previous behaviour). **Pedestal** makes left/right and forward/back follow where the camera is pointing, with vertical staying true. Needs absolute pan mode.
- **Crane pan-stabilise.** A **Pan Stab** toggle in the Grip header (and a bindable *Crane · Pan Stab* action in the Functions panel). **On** — the camera holds its heading as the arm swings, giving a pure arc/parallax move. **Off** — the camera rides the arm and pans with it. Driven by the crane's own mount-yaw lock, so it's handled inside Unreal at render rate with no extra remote-control traffic.
- **Invisi-crane.** A **Hide Crane** toggle (Crane Base header, and bindable as *Crane · Hide / Show*) vanishes the rig from both the render and the editor viewport, so the arm never appears in shot.
- **Bigger font options** — the S / M / L selector now runs a notch larger across the board.
- **Two new guide sections** — **Remote viewing** (drive the panel from a phone, tablet or second laptop on the same network) and **Rendering your move out of Unreal** (Take Recorder, Movie Render Queue, and why Temporal Sample Count is the setting that matters).

## Fixes

- **Sensitivity no longer shrinks your limits.** S was being applied twice — once to the wheel input and again to the output range — so dropping crane yaw to S=0.2 silently gave you only 20% of your Min/Max travel. Feel (S) and travel (Min/Max) are now independent: full slider travel always reaches your limits, and S only changes how much wheel movement it takes to get there.
- **Fine wheel motion is no longer thrown away.** The minimum-change gate before a velocity axis re-sent was coarser than a single wheel detent, so slow, delicate pan moves were swallowed until they accumulated and then fired in a lump — visible as stepping. The gate is now finer than one detent.
- **Scan UE no longer gives up too early.** The actor-list request timed out after 2 seconds; on a busy editor Unreal's reply arrived *after* that, so the scan reported "no cameras found" while the answer was still in flight. This was the cause of intermittent empty scans — including the confusing case where no cameras are listed but your sliders still drive the camera fine. The scan now waits properly.
- **Scan says what's actually wrong.** If Unreal is blocking remote calls, the log now names the setting to change instead of silently falling through to deprecated paths and filling Unreal's log with unrelated errors.
- **Grip limits grey out** when the **Limits** tickbox is off, so it's obvious they aren't applying.

## UE 5.8 note (important)

UE 5.8 **blocks remote function calls by default**, which stops Scan UE from listing your level.

**Project Settings → Plugins → Remote Control → Security → tick "Allow Any Remote Function Call".**

Three things worth knowing: it is **per-project**, so every new project needs it set again; it does **not** travel with the app or your config; and if it's already ticked but Scan still finds nothing, **untick it, re-tick it**, then Scan again. Full steps in **GETTING_STARTED.md**.

## Updating

Run `RexyBridge-Setup-3.4.0-beta.exe` over your current install, or click **Check for updates** in the top bar.

## Known notes

- **Unsigned installer** — SmartScreen warns on first run: **More info → Run anyway**.
- Requires **Unreal Engine 5.3+** (5.8 supported) with the **Remote Control API** plugin (WebSocket port `30020`).
- **Dolly Pedestal** requires absolute pan mode — that's where it gets the camera heading from.
- **Soft Stops** (per-parameter limits with feathered deceleration) is in development for the next release.
- If a move still looks stepped in a render, check the input itself — a low-resolution or slow-reporting control quantises the move before the bridge sees it, and no amount of filtering fully recovers it. The **Signal Filter Lab** and tune-scan export will show you.
- Beta — report anything odd via an **Issue** or **rob@realprogear.com**.
