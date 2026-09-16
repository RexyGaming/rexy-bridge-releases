# Rexy Bridge

**Virtual production camera control for Unreal Engine 5.** Drive Cine Camera Actors and CameraRig_Crane rigs live in the editor with physical wheels, game controllers, MIDI, OSC, or the keyboard.

This repository is the **download page and documentation** for Rexy Bridge. (The v3 application is closed source.)

---

## ⬇️ Download

**[→ Download the latest release](../../releases/latest)**

Rexy Bridge runs on **Windows** and **macOS**:

- **Windows** — grab `RexyBridge-Setup-<version>.exe`, run it, and follow the setup guide below.
- **macOS — Apple Silicon (M-series)** — grab `RexyBridge-Setup-<version>-arm64.dmg`, open it, and drag **Rexy Bridge** to Applications.
- **macOS — Intel** — grab `RexyBridge-Setup-<version>-x64.dmg` instead.

> **Heads-up — the installers aren't code-signed yet.**
> - **Windows** shows a blue **"Windows protected your PC"** dialog — click **More info → Run anyway**.
> - **macOS** blocks a normal double-click — **right-click (or Control-click) the app → Open → Open**. You only need to do this once. On first controller use, allow **Input Monitoring** (System Settings → Privacy & Security → Input Monitoring).
>
> This is expected for a beta and is not a warning about the app itself.

---

## 📖 Documentation

- **[Getting Started](GETTING_STARTED.md)** — install the app and connect it to Unreal Engine (start here).
- **[User Guide](USER_GUIDE.md)** — every control, panel by panel.
- **[User Guide — print / greyscale (PDF)](USER_GUIDE-light.pdf)** — a light-background, mono-friendly edition for printing.

---

## Requirements

- **Windows** (64-bit) **or macOS** (Apple Silicon or Intel)
- **Unreal Engine 5.3+** with the **Remote Control API** plugin enabled
- A Cine Camera Actor in your level (a crane rig is optional)

Everything else — the bridge, the control panel, and the gamepad reader — is bundled inside the installer. No Node, Python, or dependencies to install.

---

## Feedback

This is a **beta**. Bug reports and suggestions are very welcome:

- Open an **[Issue](../../issues)** here, or
- Email **rob@realprogear.com**

*© RealProGear. Rexy Bridge v3 is closed source; this repo hosts the downloads and docs only.*
