# Rexy Bridge 3.6.2-beta

The tidy-up release: every section of the panel now **collapses to a colour-coded header**, so you can fold away the parts you're not using and keep the controls you care about in view. Everything from the **3.6.0** many-wheels release (16-bit SDL input, many devices) is still here.

**[Install & UE setup guide](GETTING_STARTED.md) · [User guide](USER_GUIDE.md) · [Print / greyscale guide](USER_GUIDE-light.pdf)**

## New

- **Collapsible panels.** Every section — Rexy Wheels, Rexy Focus, Rexy Grip, Functions, Virtual MoCo, Soft Stops, Gamepad Debug and Alt Inputs — now has a **caret** and a **colour patch** in its header. Click the header (or the arrow) to fold that section down to a single labelled line; click again to open it. Each panel remembers whether you left it open or closed, so your layout comes back the way you set it.
  - **Consistent headers.** Gamepad Debug and Alt Inputs used to have a separate *Show / Hide* button — they now match every other section with the same caret-and-colour header.
  - **Soft Stops** sits above its box like the rest, so collapsing it leaves a clean single-line header.
- **Cleaner layout order.** **Functions** now sits directly below **Rexy Grip**, and **Soft Stops** sits directly below **Virtual MoCo** — grouping the controls that belong together and shortening the scroll when panels are folded away.

## Also in the 3.6 line (from 3.6.0-beta)

- **SDL input mode — 16-bit, many devices.** The **"SDL 16-bit · multi"** toggle in the Gamepad Debug panel reads your wheels directly in the bridge's main process: full 16-bit resolution (not the browser's 8-bit) and **more than 4 devices** at once.
- **SDL / USB axis scan** and **raw 16-bit code in the calibration wizard** for verifying wheel firmware resolution and report rate.

## Note on 3.6.1

3.6.1 was a **macOS-only** build (arm64 + x64 for Apple Silicon / Intel Macs) with no functional changes on Windows. 3.6.2 brings both platforms back to parity.

## UE 5.8 note (unchanged, still important)

UE 5.8 **blocks remote function calls by default**, which stops Scan UE from listing your level.

**Project Settings → Plugins → Remote Control → Security → tick "Allow Any Remote Function Call".** It is **per-project**; it does **not** travel with the app or config; and if it's already ticked but Scan still finds nothing, **untick it, re-tick it**, then Scan again. Full steps in **GETTING_STARTED.md**.

## Updating

Run `RexyBridge-Setup-3.6.2-beta.exe` over your current install, or click **Check for updates** in the top bar.

## Known notes

- **SDL input mode needs the installed desktop app** — SDL reads USB devices in the bridge's main process, so a remote browser panel on another device can't use the host machine's wheels (it can still drive everything else over the network).
- **Re-bind after switching input source** — Browser and SDL number devices differently, so bindings made under one won't line up under the other.
- **Unsigned installer** — SmartScreen warns on first run: **More info → Run anyway**.
- Requires **Unreal Engine 5.3+** (5.8 supported) with the **Remote Control API** plugin (WebSocket port `30020`).
- Beta — report anything odd via an **Issue** or **rob@realprogear.com**.
