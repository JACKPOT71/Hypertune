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

`v8.6.74` · Windows 10 / 11 · x64 · Installer & Auto-Update

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
- **Seven languages** (English, German, French, Spanish, Italian, Russian, Chinese) — switching refreshes every page together and keeps the window where it was
- A single color language across the dashboard: red is reserved for errors and NOT-GO verdicts
- Game artwork ships with the installer; add your own per game by dropping in a JPG

---

## Release Notes v8.6.74

### The full view is easier to use

- **The dashboard shows one state per game.** Each game card keeps its own switch, and the status line says in plain words what happens next ("switch on, then start the game"). Nothing changes in the background without the switch.
- **Tuning steps explain themselves.** Every step on the tuning page carries a short sentence about what it does and when it applies. Steps that do not fit this machine stay visible but switched off, so the list never looks broken.
- **Saved profiles match what was applied.** A profile built from the overview carries the same choices that the overview applied. Loading it later restores the same view, including the network choices that belong to it.

- **This build is unsigned, and it says so.** Windows will show "Unknown publisher" on first run; that is expected for this release. The release page names the SHA-256 and ships `SMARTSCREEN.md` with the two clicks it takes.
- **Download:** [Hypertune on GitHub](https://github.com/JACKPOT71/Hypertune). The setup and its SHA-256 appear on the release page for v8.6.74.

## Release Notes v8.6.73

### Your network changes stay with the profile

- **What you change on the network page is part of the profile.** Until now the profile only remembered which profile file it used. A value you changed yourself was written to the machine and forgotten by the next run, which put the file's old value back. Now your changed values are stored in the profile as your own set, applied on top of the file they belong to - in one pass, not two.
- **Nothing is saved behind your back.** After a successful apply, Hypertune asks what should happen: take the values into the active profile, save them as a new profile, or decide later. "Later" leaves the file exactly as it was, and the network page keeps showing how many values are still open.
- **The page says what is stored.** A status line names how many changed values the active profile carries and when it was last saved. If the chosen profile file does not know one of your values at all, a short note says so - the value is stored and applied anyway.
- **Profiles and sessions on disk are protected.** Profile and session files are written in the protected profile format (HTP1); older plain-text files are still read and converted on the next save.

- **This build is unsigned, and it says so.** Windows will show "Unknown publisher" on first run; that is expected for this release. The release page names the SHA-256 and ships `SMARTSCREEN.md` with the two clicks it takes.
- **Download:** [Hypertune on GitHub](https://github.com/JACKPOT71/Hypertune). The setup and its SHA-256 appear on the release page for v8.6.73.

## Release Notes v8.6.71

### Steps that do not apply stay out of the way

- **Hardware that is not installed is no longer applied.** The tuning page keeps the row visible but switched off, marks it as not applicable, and leaves it out of Apply all and saved profiles. On a machine without NVMe, the NVMe steps no longer look like a required part of the setup.
- **Apply all and saved profiles agree.** A switch now saves and applies the same command, so a step can no longer be stored under one name and sent under another. The profile built from the automatic profile therefore matches what is actually applied.
- **A stalled start leaves a clean way back.** Hypertune records the last completed startup stage. After an interrupted start, the next launch can tell a stale run from a fresh one and opens normally instead of waiting on the old state.
- **NVIDIA profiles are named by what they do.** The list now uses Jackpot names only; the suffix says what the profile is for: Smooth GSync, Vsync on or off, Unlimited, LowLatency, FrameSync or Optimized.

- **This build is unsigned, and it says so.** Windows will show "Unknown publisher" on first run; that is expected for this release. The release page names the SHA-256 and ships `SMARTSCREEN.md` with the two clicks it takes.
- **Download:** [Hypertune on GitHub](https://github.com/JACKPOT71/Hypertune). The setup and its SHA-256 appear on the release page for v8.6.71.

## Release Notes v8.6.70

### Network and power tools, complete again

- **AFD socket tuning is back on the network page.** The tab sits beside RSS, advanced, global, power, interface and interrupt, with the full socket setting list in one place.
- **USB power tweaks are one click away again.** The power card offers the USB action next to device power saving, with the same confirmation and restore point.
- **The TCP parameter preset is back in the quick-pick list.** It applies the global TCP set and the matching AFD parameter step together, as before.

### Startup chain and Safe Mode, now with a way back

- **The Windows startup chain is managed in the overview.** The full edition can create or update the login chain from the active profile, including the boot-time hardware steps and the replay. The same card removes it again - no Autoruns and no manual Task Scheduler work.
- **The chain skips tuning in Safe Mode.** If Windows starts in Safe Mode, the chain records that it was skipped and exits before touching hardware. A broken chain therefore cannot keep the machine in a hardware-only boot loop.
- **Safe Mode now has a visible rescue path.** The rescue action removes the startup chain first and then prepares the next Safe Mode start. A small return path restores normal boot automatically at the next sign-in, even if Hypertune is not opened.
- **An unconfirmed Safe Mode flag keeps the return path active.** If Windows does not confirm the boot change, the automatic return path is not deleted; the app says so plainly and retries at the next start. This closes the remaining case that could leave a machine booting into Safe Mode.
### Recovery without a reboot

- **The V2 view now protects the same way as the classic view.** A running protected game blocks hardware writes, and the driver is unloaded after every apply, before a game launch, and while a game is detected in the background.

- **A driver that is still stopping no longer blocks the next start.** Hypertune now waits for Windows to release the hardware driver and then continues automatically. Closing and reopening the app is enough; a Windows restart is not needed.

- **This build is unsigned, and it says so.** Windows will show "Unknown publisher" on first run; that is expected for this release. The release page names the SHA-256 and ships `SMARTSCREEN.md` with the two clicks it takes.
- **Download:** [Hypertune on GitHub](https://github.com/JACKPOT71/Hypertune). The setup and its SHA-256 appear on the release page for v8.6.70.

## Release Notes v8.6.69

**A sharper cockpit, a quieter language switch**

- **Quick Start now reads like a route.** The overview walks from game to wish profile to arm or launch in three numbered steps, with one clear action at each stop.
- **The active page is easy to find.** The sidebar marks the current page with a gold edge, and Tab plus the arrow keys move through the navigation with a visible focus ring.
- **The top bar has room to breathe.** The small status pills are gone, leaving language, Credits, Donate and Discord in one calm line.
- **Copying the hardware ID confirms itself.** The license page shows "Copied" for two seconds and keeps the next step in view with a three-step guide.
- **An active license shows when it ends.** The status names the remaining term and the end date, not just "active".
- **Switching language no longer moves the window.** Size, position, fullscreen state and focus stay where they were, and all seven languages refresh together.
- **The Pro view stays clearly experimental.** Its link remains marked as an experimental preview beside the main workspace.
- **This build is unsigned, and it says so.** Windows will show "Unknown publisher" on first run; that is expected for this release. The release page names the SHA-256 and ships `SMARTSCREEN.md` with the two clicks it takes.
- **Download:** [Hypertune on GitHub](https://github.com/JACKPOT71/Hypertune). The setup and its SHA-256 appear on the release page for v8.6.69.

## Release Notes v8.6.68

**The view switch moved to the header**

- **The switch sits beside the language selector.** The pill that opens the simple view now lives in the top bar, next to the language choice and above Discord, Donate and Credits - not in the sidebar.
- **The sidebar is shorter again.** The switch no longer takes a row between the hardware tools, so pages and tools stay one readable list.
- **The two views themselves are unchanged.** The complete cockpit remains the default; the simple view opens with one click, the choice is remembered, and the old window stays open until the new one is ready.
- **This build is unsigned, and it says so.** Windows will show "Unknown publisher" on first run; that is expected for this release. The release page names the SHA-256 and ships `SMARTSCREEN.md` with the two clicks it takes.
- **Download:** [Hypertune on GitHub](https://github.com/JACKPOT71/Hypertune). The setup and its SHA-256 appear on the release page for v8.6.68.

## Release Notes v8.6.67

**Two views, one switch**

- **The complete cockpit is the default.** Hypertune opens with every page, measurement and tool visible; the reduced view is no longer forced on experienced users.
- **A simple view is one click away.** The button in the sidebar opens a calm interface with the few steps that matter, and the same button takes you back.
- **Hypertune remembers your choice.** The last selected view opens on the next start; a one-off command-line selection does not overwrite it.
- **The switch waits for the other window.** The current view stays open until the new one has reported ready. A declined Windows prompt or a failed start leaves a usable window instead of an empty desktop.
- **This build is unsigned, and it says so.** Windows will show "Unknown publisher" on first run; that is expected for this release. The release page names the SHA-256 and ships `SMARTSCREEN.md` with the two clicks it takes.
- **Download:** [Hypertune on GitHub](https://github.com/JACKPOT71/Hypertune). The setup and its SHA-256 appear on the release page for v8.6.67.

## Release Notes v8.6.66

**The calm interface, everywhere**

- **The new interface is now the default.** Dashboard, performance, network, hardware, BIOS, backup, security and help share one calm layout; the previous view stays available as a fallback.
- **The full edition opens all nine pages.** The dashboard and the profile page now live in the same window as the rest - no second program, no separate start.
- **Every label comes from one catalogue.** The new pages read their texts from the shared catalogue, so the language selector moves them together.
- **Hardware writes wait while the anti-cheat is running.** If Riot Client or Vanguard is active, Hypertune says so and changes nothing; the check runs before the first write.
- **This build is unsigned, and it says so.** Windows will show "Unknown publisher" on first run; that is expected for this release. The release page names the SHA-256 and ships `SMARTSCREEN.md` with the two clicks it takes.
- **Download:** [Hypertune on GitHub](https://github.com/JACKPOT71/Hypertune). The setup and its SHA-256 appear on the release page for v8.6.66.

## Release Notes v8.6.65

**Priority boost and Safe Mode improvements**

- **The Windows priority boost now behaves consistently.** The card, a saved profile and the automatic startup re-apply show the same state.
- **The way back is always available.** Restoring the boost is a single step and stays available when the app closes or restarts.
- **The card updates immediately.** After a change, it shows the current state without restarting the app.

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
