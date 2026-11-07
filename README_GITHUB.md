<div align="center">

# ZENIT HYPERTUNE

**Jackpot's Hardware Register Engine — Hypertune Premium Edition**

*Full-stack Windows performance engineering for competitive gaming.*

[![Latest release](https://img.shields.io/github/v/release/JACKPOT71/Hypertune?label=release&style=flat-square&color=8B6914)](https://github.com/JACKPOT71/Hypertune/releases/latest)
[![Downloads](https://img.shields.io/github/downloads/JACKPOT71/Hypertune/total?style=flat-square&color=8B6914)](https://github.com/JACKPOT71/Hypertune/releases)
![Windows 10 / 11](https://img.shields.io/badge/Windows-10%20%2F%2011-0078D6?style=flat-square&logo=windows&logoColor=white)
![x64](https://img.shields.io/badge/arch-x64-555?style=flat-square)
[![Discord](https://img.shields.io/badge/Discord-join-5865F2?style=flat-square&logo=discord&logoColor=white)](https://discord.gg/M92HV4zfag)
[![Donate](https://img.shields.io/badge/Donate-PayPal-00457C?style=flat-square&logo=paypal&logoColor=white)](https://www.paypal.com/donate/?hosted_button_id=DTMM65KUFT732)

[**Download**](https://github.com/JACKPOT71/Hypertune/releases/latest) ·
[**Screenshots**](SCREENSHOTS.md) ·
[**Discord**](https://discord.gg/M92HV4zfag) ·
[**Donate**](https://www.paypal.com/donate/?hosted_button_id=DTMM65KUFT732) ·
[**Report a bug**](https://github.com/JACKPOT71/Hypertune/issues/new) ·
[**Changelog**](CHANGELOG.md)

`v8.6.65` · Windows 10 / 11 · x64 · Installer & Auto-Update

</div>

> [!WARNING]
> **This build is unsigned, and it says so.** The setup ends in `-unsigned`; Windows shows "Unknown publisher" on first run. The release page lists the SHA-256, and [SMARTSCREEN.md](https://github.com/JACKPOT71/Hypertune/releases/latest/download/SMARTSCREEN.md) explains the two clicks. Nothing here is called signed, verified or safe.

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

### Frame limiter — stored for every start, live in the running game
Per-game frame rate limiting through the same mechanism as the NVIDIA Control Panel slider (driver settings API). The set value is read back and re-verified on every launch; orphaned entries from older versions are cleaned up automatically. Because the driver applies a profile when the game starts, *Set* additionally hands the value to RivaTuner Statistics Server, which reaches the game that is already running - there is no switch to forget. Two things the status line always tells you: which path is active, and the frame rate measured inside the game. A limit can only lower the frame rate; if the game caps itself below your value, that measured number is what you see, not a promise.

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
A read-only view shows what is actually active after every reboot: USB state, U0 locks, data-fabric C-states, power plan, boot task health, GPU watchdog. No claims — measured values.

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

## Release Notes v8.6.65

**Priority boost is licensed - and the way back stays free**

- **The Windows priority boost now sits behind the licence check.** Switching it off requires an active licence or a running trial. After the trial ends, the switch stays locked and no profile or automatic startup re-apply can turn it off.
- **The way back is never locked.** Restoring the boost is always allowed. If the licence expires while the boost is off, Hypertune turns it back on instead of leaving the machine in that state.
- **One rule for every path.** The card, a saved profile and the automatic startup re-apply follow the same licence rule. If the licence does not allow it, nothing is changed.
- **The licence page applies immediately.** After activation the card is unlocked without restarting the app.
- **Safe Mode now has an automatic way back.** Hypertune sets up the automatic return before it changes the boot setting; if that is not possible, nothing is changed. A leftover Safe Mode setting is cleared at the next start.
- **This build is unsigned, and it says so.** Windows will show "Unknown publisher" on first run; that is expected for this release. The release page names the SHA-256 and ships `SMARTSCREEN.md` with the two clicks it takes.
- **SHA-256 of `Hypertune_Setup_8.6.65-unsigned.exe`:** `d5dcc5c8940e763152640d1e35b70f0561d59db23e5efb3ad1a11b7f365c5ddb`. The `.sha256` file next to the setup carries the same value.
- **Download:** [Hypertune on GitHub](https://github.com/JACKPOT71/Hypertune) · [Direct setup](https://github.com/JACKPOT71/Hypertune/releases/download/v8.6.65/Hypertune_Setup_8.6.65-unsigned.exe).

## Release Notes v8.6.63

**RX High Priority and the Fortnite latency test**

- **The Fortnite latency test asks for the right order.** Start Fortnite, join a match, then press `START CAPTURE`. Starting the capture first could end with "server not found"; the window now names the working order everywhere.
- **The language switch is complete.** Switching between English and German now updates the `NOTE`/`NOTIZ` label, the verdicts in the already-filled hop table, the segment line and the report headers. The English view no longer shows German table labels, and German shows the matching German labels.
- **The NetBench window carries the Jackpot mark.** The round Jackpot icon now appears in the title bar and taskbar.
- **RX High Priority works after a network-adapter reset.** Windows can move a network card to a new address when the adapter is re-detected. The step now checks the machine's current hardware instead of only the saved address, so it finds the RTL8125 again and can apply the priority ports.
- **A failed read is not called "no card" anymore.** If the adapter cannot be read, the app says that. If an RTL8125 is present but cannot be addressed, it says that too. "No RTL8125" only appears when no matching card is present.
- **No hooking, no injection, no game-file changes.** This build does not patch or inspect another program's code, read its memory, or change anti-cheat behaviour. It configures your own network adapter.
- **Safety unchanged.** No thermal or power limit was changed. Every write is still checked by reading it back, and Undo restores the previous state.
- **Your install stays yours.** Profiles, the active power plan and an activated licence stay in place.
- **This build is unsigned, and it says so.** Windows will show "Unknown publisher" on first run; that is expected for this release. The release page names the SHA-256 and ships `SMARTSCREEN.md` with the two clicks it takes.
- **SHA-256 of `Hypertune_Setup_8.6.65-unsigned.exe`:** `fa5f07a9256c7140bd885aa5b32e13ddbc67a8d3360fe973ef0b4b92e65cf78d`. The `.sha256` file next to the setup carries the same value.
- **Download:** [Hypertune on GitHub](https://github.com/JACKPOT71/Hypertune) · [Direct setup](https://github.com/JACKPOT71/Hypertune/releases/download/v8.6.63/Hypertune_Setup_8.6.65-unsigned.exe).

## Older releases

See [CHANGELOG.md](CHANGELOG.md) for the public release history.
