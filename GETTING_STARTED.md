# Rexy Bridge 3.0 (beta) — Getting Started

Rexy Bridge drives Unreal Engine 5 cine cameras and crane rigs live from physical wheels, game controllers, MIDI, OSC, or the keyboard. This guide gets you from a downloaded installer to moving a camera in UE.

There are two halves to setup: **install Rexy Bridge** (5 minutes) and **prepare your UE project** (10 minutes the first time, seconds after that). Do them in either order — connect them at the end.

---

## Part 1 — Install Rexy Bridge

1. Download **`RexyBridge-Setup-3.4.0-beta.exe`**.
2. Double-click it. Windows will show a blue **"Windows protected your PC"** dialog — this is because the beta isn't code-signed yet, **not** a warning about the app itself. Click **More info → Run anyway**.
3. Follow the installer. You can choose the install location.
4. Launch **Rexy Bridge** from the Start menu.

When it opens you'll see the control panel with a **`v3.4.0-beta`** badge in the top-left next to the logo. If you ever don't see that badge after an update, you're looking at a cached window — press **Ctrl+Shift+R** to reload.

Rexy Bridge is self-contained: the app window, the bridge that talks to UE, and the gamepad reader are all inside it. Nothing else to install.

---

## Part 2 — Prepare your Unreal Engine project

You need UE **5.3 or newer**.

### 2.1 Enable Remote Control

1. In UE: **Edit → Plugins**.
2. Search **Remote Control**.
3. Tick **Remote Control API**.
4. Restart UE when prompted.

### 2.2 Confirm the WebSocket server

Rexy Bridge talks to UE over the Remote Control **WebSocket** server.

1. **Project Settings → Plugins → Remote Control**.
2. Check **WebSocket Server Port** is **`30020`** (the default Rexy Bridge expects).
3. Check the **bind address** is `0.0.0.0` or `127.0.0.1`.
4. Save and restart if you changed anything.

### 2.3 Add a camera (and optionally a crane)

> ⚠️ Use a **Cine Camera Actor**, not a plain "Camera Actor". Rexy Bridge only discovers CineCameraActors.

From **Place Actors → Cinematic**:

- Drop in a **Cine Camera Actor** — the camera you'll drive.
- (Optional) Drop in a **Camera Rig Crane** — if you want the Grip section to drive a jib.

To use the crane: drag the Cine Camera Actor **onto** the crane in the World Outliner so it parents to the crane's **CameraMount** socket. Rexy Bridge auto-detects the attachment and enables Crane mode for that camera.

That's it — **no `mappings.json` editing and no RexyControl preset needed** in v3. Discovery is automatic (see below).

---

## Part 3 — Connect them

1. Make sure your UE project is **open in the editor** (you do **not** need to press Play — Remote Control writes live in the editor).
2. In Rexy Bridge, look at the three status dots, top-right:
   - **HARDWARE** — your wheels/controller. Grey until you click the window once and **press a physical button** (browsers only wake the gamepad API on a button press, not an axis move).
   - **WS** — the internal app↔bridge link. Should be green on launch.
   - **UE RC** — the Unreal connection. Goes green once it reaches UE.
3. Click **⌕ Scan UE** (in the camera row). Your Cine Camera Actor appears as a button. If you added a crane and parented the camera to it, it's detected automatically.
4. Click your camera to select it, then move a wheel or drag the **pan** slider — the camera rotates in UE in real time.

If the camera moves in UE, you're connected — even if the **UE RC** dot is briefly slow to turn green.

---

## Output modes

Top of the app, the **osc / ue** vs **freed** toggle chooses what Rexy Bridge drives:

- **osc / ue** (default) — drives Unreal directly via Remote Control. This is what the steps above set up.
- **freed** — instead broadcasts a **FreeD** camera-tracking stream on the network, so any FreeD-compatible virtual-production app (not just UE) can consume it. No UE writes in this mode.

---

## Troubleshooting

| Symptom | Fix |
|---|---|
| **Windows blocks the installer** | Expected for an unsigned beta — **More info → Run anyway**. |
| **App looks like an old version** | Press **Ctrl+Shift+R** in the window to reload. Confirm the **v3.4.0-beta** badge shows. |
| **HARDWARE stays grey** | Click the app window, then **press a button** on the controller (not just move a stick/wheel). |
| **WS OFFLINE** | Another copy of Rexy Bridge may be running and holding the port — close it and relaunch. |
| **UE RC won't connect** | UE project not open, Remote Control API plugin not enabled, or WebSocket port isn't `30020`. Re-check Part 2. |
| **Scan UE finds nothing** | You're using a plain Camera Actor instead of a **Cine** Camera Actor, or UE isn't reachable yet (fix UE RC first). |
| **Scan UE finds nothing on UE 5.8+** (log shows *"GetAllLevelActors … not allowed by remote control settings"*) | UE 5.8 blocks remote function calls by default. **Project Settings → Plugins → Remote Control → Security → tick "Allow Any Remote Function Call"**, then Scan again. Three things to know: it's **per-project**, so every new project needs it set again; it does **not** travel with the app or your config; and if it's already ticked but Scan still finds nothing, **untick it, re-tick it**, then Scan — the setting sometimes needs re-applying to take effect. |
| **Scan finds no cameras, but the sliders still drive the camera** | Normal, and it tells you exactly what's wrong. Driving the camera uses the object paths already saved in your config from a previous successful scan — that keeps working. **Scan** is a separate call (`GetAllLevelActors`) which is the thing being blocked. So this combination almost always means the *"Allow Any Remote Function Call"* setting above, not a lost connection. |
| **Camera moves the wrong way** | Use the **Inv** button on that control, or re-bind pushing the control in your "positive" direction first. |
| **Stick/wheel drifts at rest** | Gamepad Debug panel → **Null Drift (5s)** to null residual offset, or the per-axis **C** wizard for full range calibration. |
| **Motion is steppy or judders, but the raw *and* filtered input both look smooth** | Not an input problem — your PC is likely maxed out and Unreal can't process the Remote Control round-trip fast enough. Free up disk space and RAM, close other heavy apps (including extra UE instances), lower the editor's viewport / scalability settings, or use a more powerful machine. A smooth signal in Rexy Bridge that stutters in UE is the tell-tale sign. |

---

## Where things live

- **Config** (connection host/ports, output mode, all your bindings and tuning) can be saved and re-loaded from the Config row — export a `.json` to move a setup between machines.
- **Lens boxes** and **takes** export/import independently, so you can share a lens kit or a move without sharing the whole config.

For what every control does, see **USER_GUIDE.md**.

*Questions or bug reports: rob@realprogear.com*
