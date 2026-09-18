<div align="center">

# ZENIT HYPERTUNE

**Jackpot's Hardware Register Engine — Hypertune Premium Edition**

*Full-stack Windows performance engineering for competitive gaming.*

`v8.6.8` · Windows 10 / 11 · x64 · Installer & Auto-Update

**[📸 View the screenshot gallery](SCREENSHOTS.md)**

</div>

---

## What is this?

Hypertune is a single Windows application that unifies **every layer of system latency** — CPU, PCIe bus, GPU, network stack and memory — behind one interface and one switch.

Instead of a folder full of scripts that each touch a different layer, Hypertune builds a complete performance profile of your machine, applies the appropriate optimizations per layer, **verifies every write by reading it back from the hardware**, and re-applies the volatile parts automatically at every boot.

Nothing here is a "tweak list". It is an engine: scan → decide → apply → verify → persist → prove.

---

## Highlights

### One-switch gaming readiness
A single rocker applies the full chain: boot-level hardware configuration, per-core CPU delivery steering, network stack hardening and GPU clock management. Close the app, start the game. The boot task keeps the hardware layer alive across reboots.

### Hardware layer (Premium)
- Direct PCIe device configuration (link power management, request sizing, interrupt delivery) with per-device read-back verification and conservative guards on root ports
- Per-core CPU delivery control with live read-back of the current request/state on every logical core
- Boot-time low-power state limiting on modern Intel platforms, with safety detection for BIOS-locked systems
- USB controller interrupt tuning on the xHCI level
- All writes verified. All failures reported honestly — if the platform refuses a write, the log says so, in plain words. No silent fallback to stock.

### Network layer (S.U.C.K. Protocol)
- Hardened network stack engine with **Apply → Verify → Diff** cycle: every value is compared live after application, deviations are reported per key
- Vendor-aware profiles (Realtek / Intel), including deep adapter-specific latency profiles for modern Realtek 2.5G NICs (RTL8125/8126 family) — available as a selectable profile, on/off, with revert
- RSS distribution profiles, congestion provider management, MTU auto-detection, interrupt affinity pinning
- Portable profiles: every setting set is a file. Export, share, import — with a checksum-verified snapshot of the previous state before anything is written.

### Safety architecture
- **Snapshot before write.** Every import and every apply creates a byte-exact copy of the affected registry state. One click restores it.
- **Restore points** alongside snapshots for system-level rollback.
- **Honest reporting**: the verification step distinguishes between "applied", "already optimal", "platform refuses this write" and "not applied". Stock settings never masquerade as tuned.
- **Driver diagnostics**: a built-in doctor that checks every known blocker for kernel-level access and names the exact fix per item.

### Measurement
- End-to-end latency measurement with jitter analysis and a live sparkline history
- DPC/ISR latency reporting via Windows Performance Toolkit integration
- TSC/timer verification: shows whether your system actually uses the invariant hardware counter — with measured QPC call costs as proof

### Windows tools
- Win Tweak Verifier: static analysis of system binaries to verify that registry values are actually consumed by Windows code paths (not just present)
- Registry Shield: snapshot & rollback for arbitrary `.reg` files before you import them
- Device Cleaner, service profile management, power plan awareness, driver repair utilities
- GPU module: clock pinning via the official driver interface, NVIDIA control panel restoration, driver hygiene helpers

---

## v8.6.8 Release Notes

**Software update system**
- Smart Update: the app downloads the official installer, verifies its SHA-256 checksum and launches it. No browser roundtrip, no manual hash comparison. The application closes itself; all settings survive the update.
- The update manifest is now checksum-signed per release. Checksum mismatch = hard fail with a clear message, never a silent install.

**Verification & transparency**
- Boot engine now reports per-core write acceptance counts. If a platform refuses a low-power-state write on every core, the log states "NOT applied" instead of a success line. Trust the log, not the hope.
- Driver diagnostics extended: detects the missing-driver-next-to-executable condition and the USB helper-driver condition, both with plain-language fixes.

**Deployment**
- The installer now registers an antivirus exclusion for the installation folder automatically (optional, one-click manual fallback inside the app under *Maintenance*).
- New built-in documentation chapter: *Prerequisites* — the exact set of platform requirements per feature, per vendor.

**UI**
- Live version display in the sidebar (red, always visible) and in the window title.
- Additional maintenance shortcut for Defender exclusion handling.

<details>
<summary><strong>Full prerequisite list (target machine)</strong></summary>

| Requirement | Scope | Why |
|---|---|---|
| Administrator start | Mandatory | Kernel driver, bus configuration, boot settings |
| Antivirus exclusion for install folder | Strongly recommended | Kernel driver is classified as a generic "Hacktool" by pattern-based AV engines |
| BIOS: CFG Lock disabled | Intel platforms only | BIOS-locked registers reject low-power-state writes; the engine detects and reports this |
| Memory Integrity (HVCI) disabled | Windows 11 only | HVCI enforces the Microsoft vulnerable-driver blocklist; irrelevant on Windows 10 |
| Realtek RTL8125/8126 NIC | Deep latency profile only | All other features are vendor-independent |

</details>

---

## Installation

1. Download `Hypertune_Setup_<version>.exe` from [Releases](https://github.com/JACKPOT71/Hypertune/releases).
2. Run it. The installer handles running instances, service state and the antivirus exclusion.
3. Start Hypertune. The daily update check keeps you current automatically; updates install with one click from inside the app.

Your settings, snapshots and profiles live in `%LOCALAPPDATA%` and survive updates **and** uninstallation.

### Antivirus notice

Hypertune uses an open-source kernel driver (WinRing0 family) for protected hardware register access. Because the same capability is used by malware, antivirus engines flag it generically. It is not — and here is why: the driver is a **public, open-source component** ([WinRing0 on GitHub](https://github.com/GermanAizek/WinRing0)) that monitoring tools like Open Hardware Monitor have used for years. Hypertune uses it solely to read and write your own hardware's configuration registers. For details on why pattern-based AV engines flag it anyway, use the one-click exclusion button in the app (**Maintenance → Allow in Windows Defender**).

---

## FAQ

**Will this trigger anti-cheat systems?**
The tool uses documented operating system and driver interfaces wherever they exist. There is no injection, no hooking, no memory manipulation of other processes. Kernel access is used to read and write your own hardware's configuration registers. Close the tool before gaming if you prefer a minimal process footprint.

**Does it collect anything?**
No telemetry, no accounts, no phone-home. The only network request is the daily version check against this repository.

**What if something feels wrong?**
Every write is preceded by a snapshot; the Security Center lists them all. Restore takes one click. The driver diagnostics and the exported support bundle make remote debugging trivial.

**Does it work on my hardware?**
The engine is vendor-aware: Intel and AMD paths are separate, root-port guards protect mismatched boards, unsupported features report "unsupported" instead of guessing. The *Prerequisites* chapter in the Help Manual documents exactly what each feature needs.

---

## Repository contents

| Path | Purpose |
|---|---|
| `latest.json` | Update manifest consumed by the in-app update check |
| [Releases](https://github.com/JACKPOT71/Hypertune/releases) | Setup binaries per version, checksum listed in each release |

---

<div align="center">

*Built by a tweaker, for tweakers. Measure first, change one layer at a time, verify everything.*

</div>
