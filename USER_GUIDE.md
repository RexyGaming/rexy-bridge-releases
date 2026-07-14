# Rexy Bridge 3.0 — User Guide

A panel-by-panel tour of every control. Setup and UE connection are covered in **GETTING_STARTED.md**; this document assumes you're connected and driving a camera.

> 📸 **Screenshot:** the whole app window, so readers can see the overall layout before we go section by section.

---

## Core concepts (read this first)

**Binding.** Almost every control has a **Bind** button. Click it, then actuate the input you want — a wheel, a stick, a keyboard key, a MIDI knob, or an OSC/FreeD channel. For continuous controls, push it the way you want to be "positive" first; for keys/buttons it captures a two-stage *increase* then *decrease*. Right-click a Bind button to clear it.

**Per-camera bindings.** Every camera you select keeps its **own** set of bindings. Switch cameras and your inputs re-map to that camera's saved layout.

**S / C / D / F tuning.** Wherever you see these four little boxes, they shape how an input drives the value:

- **S — Sensitivity / Speed.** Multiplies how fast the control moves the value. Works for analogue *and* keyboard/button inputs (higher = faster).
- **C — Curve.** Response gamma. `1.0` = linear; higher = "fluid-head" feel (gentle at first, faster as you push); lower = punchy.
- **D — Deadband.** Ignores tiny inputs near centre — kills stick/wheel drift. (Not relevant to keyboard/button inputs.)
- **F — Feather.** Smooths the start and stop so motion eases in and out instead of snapping.

**Inv / Hold / Reset.** **Inv** flips a binding's direction. **Hold** (on wheels) freezes that axis so its binding is ignored. **Reset** returns the control to centre/default.

---

## 1. Top bar

> 📸 **Screenshot:** the top bar — logo + version badge on the left, status dots and Units/Output toggles on the right.

- **Version badge** (`v3.0.0-beta.1`) — the running build. If it's missing or wrong after an update, press **Ctrl+Shift+R**.
- **HARDWARE** dot — your gamepad/wheels. Wakes when you click the window and press a physical button.
- **WS** dot — the internal app↔bridge link.
- **UE RC** dot — the Unreal Remote Control connection.
- **Units** — global metric (m/cm) vs imperial (ft/in) for distances and positions.
- **Output mode** — **osc / ue** drives Unreal directly; **freed** broadcasts a FreeD tracking stream instead.

---

## 2. Camera row

> 📸 **Screenshot:** the camera row with a couple of discovered cameras and the Scan UE button.

- **⌕ Scan UE** — auto-discovers every CineCameraActor and CameraRig_Crane in your open level. No preset or `mappings.json` editing required.
- **Camera buttons** — click to select the active camera. The selected camera's bindings and profile load. Each camera button can itself be **bound** to a key/button for fast switching.
- A camera parented to a crane enables **Crane** mode automatically.

---

## 3. Connection & Config row

> 📸 **Screenshot:** the config row (connection fields + Save/Load).

- **Script Host / Port** and **UE Host / Port** — where the bridge and Unreal live. Defaults work for everything on one PC.
- **Save / Load config** — writes or restores a `.json` holding your connection settings, bindings, tuning, lenses, lens boxes, favourites, jog binding, and modes. Use it to move a complete setup between machines.

---

## 4. Functions panel

Bindable one-shot actions. Each card has a **Trigger** (fire it now) and a **Bind** (assign a key/button). Binding any copy of an action keeps every copy in sync.

> 📸 **Screenshot:** the Functions panel showing all cards.

- **Autolevel Roll** — smoothly returns roll to 0° over **Time** seconds, with an **F** easing.
- **MoCo · Rec / Play / Stop / Home / Mark** — transport actions, bindable so you never have to reach for the mouse mid-take. **Mark** drops a mark on **every bound track** at the playhead.
- **Lens · Tighter / Wider** — step to the next longer/shorter lens in the active **lens box**.

---

## 5. Rexy Wheels — camera head

The three head axes: **pan, tilt, roll**.

> 📸 **Screenshot:** the Wheels panel (all three cards), plus a close-up of one card showing every control.

- **Absolute / Relative** (panel header) — Absolute: wheel position = camera angle. Relative: wheel deflection = rotation *speed*, centre = hold (endless-rotation, fluid-head style).
- **Value** and **live —** readouts — what you're commanding vs the camera's actual angle from UE.
- **Slider** — drag directly, or watch it track your bound input.
- **Bind / Hold / Inv / Reset** — as described in Core concepts.
- **S / C / D / F** — per-axis tuning.
- **Min / Max** — clamp the output range for that axis.

---

## 6. Rexy Focus — lens & body

> 📸 **Screenshot:** the whole Focus panel.

### Lens & body (left)

- **Camera body / filmback** — sensor/filmback preset.
- **Lens** — pick a lens; UE's LensSettings (focal, aperture, min-focus) update live.
- **+ Add custom lens** — define name, focal min/max, f-stop min/max, and **Min focus** (shown in cm or ft to match your Focus-units toggle). It's added to the list and applied.

### Lens boxes

A **lens box** is a named kit — a list of lenses you cycle through on set.

> 📸 **Screenshot:** the Lens box section with a box loaded and a few lenses in it.

- **Box selector** + **Create lens box** — make and switch between kits.
- **Add lens to box** dropdown — add any existing lens, or **✎ + Custom lens…** to define a new one that's dropped straight into the box.
- **Lens chips** — the box's lenses, always sorted by focal length; the active lens is highlighted. ✕ removes one.
- **◀ Wider / Tighter ▶** — step through the box by focal length (clamped at the ends). Each has a **Bind** for hardware control.
- **Save / Export / Import / Delete** — boxes export and import independently of the main config, so you can share a kit.

### Favourite lenses

> 📸 **Screenshot:** the Favourites list with a couple of favourites and their Bind buttons.

A global quick-jump list. Add any lens, then **Bind** a key/button to jump straight to it — independent of which box is loaded.

### Focus / Iris / Zoom

> 📸 **Screenshot:** the Focus/Iris/Zoom rows showing the sliders and the S/C/D/F boxes.

Each has a slider, **Bind**, **Inv**, a live readout, and the full **S / C / D / F** tuning row — so a focus puller can bind a wheel or keys and tune the feel exactly like the head axes. Zoom locks automatically on a prime lens.

---

## 7. Grip — crane / dolly / drone

> 📸 **Screenshot:** the Grip panel with the Crane/Dolly/Drone mode buttons.

- **Crane / Dolly / Drone** modes:
  - **Crane** — the grip swings a jib arm around its base (yaw, pitch, scope/arm-length).
  - **Dolly** — straight ground translation (X/Y/Z), no arm pivot.
  - **Drone** — free flight through 3D space.
- **Grip cards** (craneYaw, scope, cranePitch) — same binding + S/C/D/F model as the wheels.
- **Crane Base** (baseX/Y/Z) with **Absolute / Relative** — Absolute: slider = position between Min/Max. Relative: slider deviation = movement speed, centre = stop.

---

## 8. Position panels

> 📸 **Screenshot:** the camera and crane position panels.

Live **X / Y / Z** readouts for the camera and crane, with **Set** (send a manual position; blank axes keep their current value) and **Zero** (reset to 0,0,0).

---

## 9. Virtual MoCo

Record, edit, and play back moves across every bound parameter.

> 📸 **Screenshot:** the full Virtual MoCo panel — transport, timeline, and track list.

### Transport

> 📸 **Screenshot:** the transport row (REC / STOP / PLAY / Bake / Rewind / Home / Mark / Jog).

- **● REC / ■ STOP / ▶ PLAY** — each with a **Bind** button for hardware control. STOP leaves the playhead where it is; **Home** (or Rewind) returns it to the start.
- **Bake** — a 3-2-1 countdown on REC/PLAY so you can sync with UE's Take Recorder.
- **⌂ HOME** — snaps play-armed tracks to their start values and the playhead to 0.
- **◆ MARK** — drops a mark on every bound track at the playhead.
- **Jog: Bind** — bind an analogue wheel/axis (or keys) to **shuttle** the playhead: push from centre to scrub forward/back, speed proportional to deflection, centre = hold.

### Takes

> 📸 **Screenshot:** the take controls (New / Duplicate / Delete / take selector / Save / Load / Expand / Reset).

Multi-take management. Save/Load moves as `.rxmove` files. **Expand** stacks each track in its own lane; **Reset** clears everything.

### Timeline

> 📸 **Screenshot:** the timeline canvas with a recorded move, playhead, and some marks.

Colour-coded per track. Scrub by dragging the playhead, zoom with the scroll wheel, and drag anchor dots to reshape curves.

### Track list & arming

> 📸 **Screenshot:** the track list showing the P / R / E / M arm buttons on a track.

Each track has four arm toggles:

- **P — Play** — plays back its recorded/marked data.
- **R — Record** — captures live input on the next REC (recording over a track auto-erases its marks).
- **E — Edit** — drag anchor dots to reshape. Available once a track has recorded data **or 2+ marks** — entering E on a marked-but-unrecorded track lays down draggable anchors that smooth the marks into **S-curves**.
- **M — Mark** — drops a fixed point at the playhead; the curve always passes through marks. Placing a mark auto-adds a start mark at t=0 so the move has a defined beginning.

---

## 10. Gamepad Debug & calibration

> 📸 **Screenshot:** the Gamepad Debug panel open, showing live axis bars.

- **Show / Hide** — toggles the live view of every axis and button on connected controllers.
- **Null Drift (5s)** — samples all axes for 5 seconds and stores the average as zero, nulling resting drift. **Clear Cal** removes it.
- **Per-axis "C" button** — opens the calibration wizard:

> 📸 **Screenshot:** the calibration wizard modal (ideally on the "Tune response" step showing the curve + waveform).

  - **Steps 1–3** capture the axis **max**, **min**, and **rest** so uneven hardware maps to a clean −1…+1.
  - **Tune response** shapes the feel with a preset (Linear / Relaxed / Aggressive) or a custom curve, with a live waveform and curve preview. **Skip** jumps straight to the tuner; **Redo step** re-captures the current step.

---

## 11. Other inputs — OSC, MIDI, FreeD

> 📸 **Screenshot:** the alt-inputs area (OSC in, MIDI, FreeD in).

- **OSC in** — accept OSC from external devices (e.g. the Rexy Wheels). Set **port**, an optional **prefix** filter, and the input **min/max** range. **Sample 10s** records every OSC message for ten seconds and exports a JSON log — the ground-truth capture for diagnosing a device.
- **MIDI** — **Enable MIDI** reads MIDI controls (knobs, faders, notes, pitch-bend) into the same input path as gamepads, so they bind the same way.
- **FreeD in** — accept an incoming FreeD tracking stream.

All three feed the same binding system: enable the source, then **Bind** any control to it.

---

## 12. OSC output log

> 📸 **Screenshot:** the log panel.

A live feed of what the bridge is sending and status messages — handy for confirming a control is reaching UE and for spotting warnings.

---

*Questions or bug reports: rob@realprogear.com*
