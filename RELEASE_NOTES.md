# Rexy Bridge 3.7.0-beta — Sandbox

The big one: **Sandbox practice levels.** Click **Install Sandbox** and Bridge downloads ready-made Unreal practice levels — a crane, a free camera, people walking and a car passing, repeating exactly the same every time — and launches and drives them for you. **No Unreal Engine install needed.**

**[Install & setup guide](GETTING_STARTED.md) · [User guide — 16. Sandbox](USER_GUIDE.md#16-sandbox--practice-levels) · [Build your own levels](https://github.com/RexyGaming/rexy-sandbox-kit)**

## New — Sandbox

- **Install / Update in the app.** One download (~600 MB) with the Sandbox player and its levels: **Practice Template** and **Street — Walkers & Car**. Newer players show up as an **⬇ Update** link.
- **Launch, Stop, E-Stop** — all bindable; E-Stop takes a system-wide key combo that works while the game has focus. Windowed or full screen, on the display you choose; the game window reopens where you left it.
- **Views** — an editor-style **blocking view** of the whole set showing every rig, and a **monitor window per camera** you can drag to any screen. Rig **Hide**, camera **rename (✎)**, crane **Smoothing**, and **in-game controls** for the action.
- **Look & performance** — **Motion blur** as a shutter angle (180° = film), **Frame lock** (24–60 fps with VSync), a live **fps** readout, **Monitor res** (monitors render smaller and scale up — the big speed win) and **Fast lighting**.
- **The action** — its own transport (start / play / end / scrub, all bindable) and a **loop** switch: off plays it once and holds the last frame, so you can line up your opening frame.

## New — Virtual MoCo

- **🔗 Lock to action** — the level's action is vMoCo's clock: **one transport** for vMoCo and Sandbox. REC punches in at the playhead (optional **Countdown**), overdubs only what you record, and ends on the last frame.
- **Takes per camera**, a timeline block per camera, and **🎥 Cameras play along** — record the crane's move, then operate the free camera while the crane repeats it.
- **＋ Add track** (no binding needed), **◆ Mark all**, **undo / redo** (Ctrl+Z, Ctrl+Shift+Z / Ctrl+Y), dashed **holds** before the first and after the last mark. *Bake* is now called **Countdown**.

## Updating

Click **Check for updates** in the top bar, or run the new installer over your current install. Then open the **Sandbox** panel and click **Install Sandbox**.

## Known notes

- **Sandbox needs a decent GPU.** If the fps readout is amber, lower **Monitor res**, try **Fast lighting**, or lower **Render quality**. Laptops whose screen runs from the integrated graphics chip can judder a little in windowed mode.
- **macOS:** the Bridge app is here now; the **Mac Sandbox player** follows shortly — until it's released, **Install Sandbox** on a Mac says there's no player yet.
- **Unsigned / un-notarised beta** — Windows SmartScreen: **More info → Run anyway**. macOS: **right-click → Open** the first time.
- **UE 5.8 with your own projects:** **Project Settings → Plugins → Remote Control → Security → Allow Any Remote Function Call** (per project) — see GETTING_STARTED.md.
- Beta — report anything odd via an **Issue** or **rob@realprogear.com**.
