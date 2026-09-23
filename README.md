<div align="center">

# ZENIT HYPERTUNE

**Jackpot's Hardware Register Engine — Hypertune Premium Edition**

*Full-stack Windows performance engineering for competitive gaming.*

`v8.6.12` · Windows 10 / 11 · x64 · Installer & Auto-Update

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

### Game Launch — the command center
One card, one goal: **APPLY EVERYTHING** runs the complete session in a single pass — network profile, thread tuning, power plan, GPU lock, game mode — re-verifies the hardware layer, then launches the game. A readiness checklist shows the true, freshly verified state of every component before launch: PCIe registers, USB interrupt affinity, frame limiter, boot task, GPU watchdog. Green only appears where something was actually checked.

**Smart Launch:** the game never starts untuned. If the tuning chain does not complete, the launch button does not fire. Games are registered as an executable, a launcher URI or a shortcut — remembered across reboots.

### Frame limiter — driver level
Per-game frame rate limiting through the same mechanism as the NVIDIA Control Panel slider (driver settings API). No injection, no overlay, no extra process. The set value is read back live from the driver and re-verified on every launch; orphaned entries from older versions are cleaned up automatically.

### Benchmarks & frame limit advisor
CapFrameX captures are imported automatically and reported honestly: average, 1 % low, latency. The advisor combines your monitor refresh rate with the measured numbers and returns a classified limit suggestion. Your own numbers can be entered manually; the capture folder is configurable with auto-detection.

### Hardware layer (Premium)
- Direct PCIe device configuration (link power management, request sizing, interrupt delivery) with per-device read-back verification and conservative guards on root ports
- Per-core CPU delivery control with live read-back of the current request/state on every logical core
- Boot-time low-power state limiting on modern Intel platforms, with safety detection for BIOS-locked systems
- USB controller interrupt tuning on the xHCI level
- All writes verified. All failures reported honestly — if the platform refuses a write, the log says so, in plain words. No silent fallback to stock.

### Process layer — Mission Control
- One process list, three actions: park, throttle, boost. Game Mode's background control and the Thread Tuner united in a single view
- Foreground awareness: when a game from your editable list takes focus, background noise (launchers, overlays, updaters) is suspended — and resumed the moment you switch away
- Thread Tuner profiles: rules applied automatically on game start, saved, loaded and shared as strictly validated JSON files
- The Game Catcher shows running processes live and captures the exact process name with one click — no executable hunting
- Everything is journaled after every state change; a crash guard resumes anything still suspended on the next start. Nothing is ever terminated.
- A hard blocklist protects system processes, the game itself and anti-cheat components — they are never touched, by design.

### Game Session — one switch per game
The toggle on the dashboard: all optimizations for a game on or off, nothing else to click. The selection is remembered across reboots, every change is journaled and rolls back cleanly.

### Live State Probe — trust through reading
A read-only view shows what is actually active after every reboot: USB state, U0 locks, data-fabric C-states, power plan, boot task health, GPU watchdog. No claims — register values.

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
- End-to-end latency measurement with jitter analysis against selectable targets and a live sparkline history
- DPC/ISR latency reporting via Windows Performance Toolkit integration
- TSC/timer verification: shows whether your system actually uses the invariant hardware counter — with measured QPC call costs as proof

### Windows tools
- Win Tweak Verifier: static analysis of system binaries to verify that registry values are actually consumed by Windows code paths (not just present)
- Registry Shield: snapshot & rollback for arbitrary `.reg` files before you import them
- Device Cleaner, service profile management, power plan awareness, driver repair utilities
- GPU module: clock pinning via the official driver interface, NVIDIA control panel restoration, driver hygiene helpers

### Interface
- **Six languages** (English, German, French, Spanish, Russian, Chinese) — switching moves every card instantly, verified by automated tests
- A single color language across the dashboard: red is reserved for errors and NOT-GO verdicts
- Game artwork ships with the installer; add your own per game by dropping in a JPG

---

## Release Notes v8.6.12

**Game Launch & frame limiter**
- New Game Launch card: one-click full-session apply with readiness checklist and smart launch continuation
- Driver-level per-game frame limiter (no injection, live read-back, re-verified every launch)
- Game artwork now ships with the installer

**Benchmarks**
- New Benchmarks card with CapFrameX capture import, honest statistics (average, 1 % low, latency) and the classified frame limit advisor
- Configurable capture folder with auto-detection

**Process layer**
- Mission Control: Game Mode and Thread Tuner united in one process list with park / throttle / boost actions
- Game Catcher: live process list with one-click name capture
- Thread Tuner profile sharing via validated JSON export/import

**Transparency**
- New Live State Probe card: read-only register-level verification of what survived the reboot
- Game Session toggle now remembers its selection across reboots

**Interface**
- Full six-language sweep: every dashboard card follows the language switch, protected by an automated pairing test
- Unified dashboard color language; red reserved for errors

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
3. Start Hypertune. The daily update check keeps you current automatically; updates install with one click from inside the app — downloaded, checksum-verified, then installed.

Your settings, snapshots and profiles live in `%LOCALAPPDATA%` and survive updates **and** uninstallation.

### Antivirus notice

Hypertune uses an open-source kernel driver (WinRing0 family) for protected hardware register access. Because the same capability is used by malware, antivirus engines flag it generically. It is not — and here is why: the driver is a **public, open-source component** ([WinRing0 on GitHub](https://github.com/GermanAizek/WinRing0)) that monitoring tools like Open Hardware Monitor have used for years. Hypertune uses it solely to read and write your own hardware's configuration registers. For details on why pattern-based AV engines flag it anyway, use the one-click exclusion button in the app (**Maintenance → Allow in Windows Defender**).

---

## FAQ

**Will this trigger anti-cheat systems?**
The tool uses documented operating system and driver interfaces wherever they exist. There is no injection, no hooking, no memory manipulation of other processes. The frame limiter uses the official driver settings interface — the same one the NVIDIA Control Panel uses. Kernel access is used to read and write your own hardware's configuration registers. Close the tool before gaming if you prefer a minimal process footprint.

**Does it collect anything?**
No telemetry, no accounts, no phone-home. The only network request is the daily version check against this repository.

**What if something feels wrong?**
Every write is preceded by a snapshot; the Security Center lists them all. Restore takes one click. The driver diagnostics and the exported support bundle make remote debugging trivial.

**Does it work on my hardware?**
The engine is vendor-aware: Intel and AMD paths are separate, root-port guards protect mismatched boards, unsupported features report "unsupported" instead of guessing. The *Prerequisites* chapter in the Help Manual documents exactly what each feature needs.

---

## What Hypertune will never do

This project has hard boundaries. No exception, no "experimental" flag, no future release will cross them:

- **No DLL injection.** Hypertune never writes code into another process's address space.
- **No function hooking.** No patching of other processes' imports or code paths.
- **No memory manipulation of other processes.** Your game's memory is your game's business.
- **No modification of game files.** Nothing in a game installation is patched, unpacked or rebuilt.
- **No simulated input.** No macros, no automation, nothing a game could read as bot behavior.
- **No anti-cheat evasion.** Nothing here is designed to hide from detection — because there is nothing to detect.

Why this matters: Hypertune configures **your own hardware and operating system** — the state your machine is in *before* a game starts, not what happens *inside* a game while it runs. Configuration is not manipulation. That distinction is why the answer to "will I get banned?" is the same today as it will be in every future release: the tool does nothing anti-cheat systems look for, and we intend to keep it exactly that way.

---

## Repository contents

| Path | Purpose |
|---|---|
| `latest.json` | Update manifest consumed by the in-app update check |
| `CHANGELOG.md` | Version history at a glance |
| [Releases](https://github.com/JACKPOT71/Hypertune/releases) | Setup binaries per version, checksum listed in each release |

---

<div align="center">

*Built by a tweaker, for tweakers. Measure first, change one layer at a time, verify everything.*

</div>
