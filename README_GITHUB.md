<div align="center">

# ZENIT HYPERTUNE

**Jackpot's Hardware Register Engine — Hypertune Premium Edition**

*Full-stack Windows performance engineering for competitive gaming.*

`v8.6.56` · Windows 10 / 11 · x64 · Installer & Auto-Update

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

## Release Notes v8.6.56

**A labelled installer, and the tuning this machine runs**
- **This build is unsigned, and it says so.** Windows will show "Unknown publisher" on first run; that is expected for this release. The release page names the SHA-256 and ships `SMARTSCREEN.md` with the two clicks it takes. Nothing here is called signed, verified or safe.
- **The checksum travels with the download.** Every setup now gets a `<name>.sha256` file next to it, so the file can be checked before it runs. The release text names the same value.
- **The tuning is unchanged.** `Jackpot_7800X3D_Fortnite`, `Jackpot_Hypertune.nip` and `Jackpot_Hypertune.pow` are the same files from 8.6.54: the 150-setting NVIDIA base profile, the 40-value power plan, the 1920 MHz GPU lock and the unlimited frame limiter. No profile was rebuilt for this release.
- **Your install stays yours.** The setup replaces the program files; profiles, the active power plan and the licence stay in place.

## Release Notes v8.6.54

**The plan, the preset and the profile this machine runs**
- **`Jackpot_Hypertune.pow` is the plan from the test machine.** All 40 values were read back from the active power scheme and compared with the file that ships: no difference. Import it once and the machine runs on exactly the plan the frame measurements were taken with.
- **`Jackpot_Hypertune.nip` is the only Jackpot preset left.** One base profile with 150 NVIDIA settings, applied machine-wide instead of per game - the older Jackpot presets are gone from the folder, and an existing install removes them on update.
- **`Jackpot_7800X3D_Fortnite` ships as a ready-made profile.** Power plan, GPU clock lock at 1920 MHz, Game Mode, the Competitive Gaming thread profile, the network profile, the Realtek/NIC/PCIe/MSR/USB chain and an unlimited frame limiter - the state this machine is tuned to, one click away.

## Release Notes v8.6.53

**Frame limiter: the executable that actually runs**
- **The limit went into a profile the game never loads.** Fortnite starts as `FortniteClient-Win64-Shipping_EAC_EOS.exe`, not as `FortniteClient-Win64-Shipping.exe`. RTSS picks its profile by file name, so the value sat in a profile that never applies - the status line said "saved", the game stayed uncapped.
- **Every executable of a game gets the value now.** The tool collects the resolved name, its siblings in the game folder, the running process and every profile that already exists for the family, and writes all of them.
- **Unlimited clears the whole family.** A leftover cap in a second executable can no longer survive the reset and silently keep limiting.
- **The read-back is per profile.** If one of them refuses the value, the message names it instead of reporting success.

## Release Notes v8.6.52

**Jackpot's NVIDIA presets on board - and a profile list that only shows current stands**
- **`Jackpot_SmoothDX12.nip`.** DWM low latency on, three pre-rendered frames, a 10 GB shader cache and the highest refresh rate the display offers - built for even frame delivery instead of the highest peak.
- **`Jackpot_MaxFPS.nip`.** V-Sync off, G-Sync off, texture filtering on High performance: a base profile that gets out of the engine's way.
- **`Jackpot_LowLatency.nip`.** Ultra low latency mode with V-Sync and G-Sync off - the shortest path from input to picture.
- **Each preset carries a base profile and the Fortnite executables**, so it applies to the game and not to the whole machine.
- **The old master profile is out of the setup.** `14.10.2026` still sat in the list next to the current stands. It stays in the working tree as a test fixture only, and the installer removes it from the program folder on update - Inno never deletes files it did not install itself, so it would have stayed there forever.
- **`Jackpot_Hypertune.pow` needs no second import.** The power plan has been in `pow/` since 8.6.51 - the same file, byte for byte.

## Release Notes v8.6.51

**BIOS Tuner: six more switches - and names that finally match the board**
- **PCIe payload and read request at the maximum.** Both sat on `Auto`; the tuned profile now asks for 4096 bytes per transaction - fewer headers for the same amount of data.
- **Network boot off.** LAN boot, the onboard PXE option ROM and the IPv4/IPv6 PXE stack are switched off, so the BIOS stops looking for a boot server while the machine starts.
- **USB mass storage driver off.** The UEFI driver that offers USB sticks as boot devices is disabled; installing Windows from a stick means switching that one back on in the BIOS first.
- **One sentence of warning comes with it.** The Optimized tier now says out loud that network boot and the USB mass storage driver are turned off - before anything is written.
- **Three names corrected for AMD boards.** "Intel LAN Controller" also finds the Realtek controller of an AM5 board, "Enable AER Cap" finds the board's "Advanced Error Reporting (AER)", and "Thunderbolt Support" points at the real Thunderbolt/USB4 switch.
- **A wrong similarity hit is closed.** "Thunderbolt Support" used to land on "Thunderbolt L1SS Support" only because the two names look alike; that block is named explicitly now.
- **The Optimized tier carries 103 switches** - 96 before - and every one of them was checked against a real board export before it shipped.

## Release Notes v8.6.50

**Measurement run: the governor decides whether the numbers count**
- **A/B in blocks, guided in plain words.** One button records one block, and the tick "lever is applied" decides which side it belongs to - a forgotten switch cannot silently flip the comparison.
- **Warm-up and pauses are part of the run.** The first capture after a change is discarded instead of scored, and the card says so while it happens.
- **Four numbers that show what you feel.** Spread, 99.9th percentile frame time and stutters per ten minutes now sit next to average and 1 % low.
- **No verdict on moving ground.** The tool records the platform's clock floor during every capture. Two sides that stood on a different floor get "no verdict", with the numbers kept beside it as information.
- **The clock can be pinned for a run - and released again.** One button puts back exactly the value that was there before.
- **"No stutters" is a result, not missing data.** A measured zero no longer blocks the verdict.

## Release Notes v8.6.49

**BIOS Tuner: a way back you can read**
- **Back to stock in one click.** The footer writes the state from before the first change back to the board.
- **The stock state exists before you need it.** It is captured automatically before the first write.
- **Readable names and a real list.** Stock, Basics, Optimized, Expert - each with date and file, no guessing from timestamps.
- **No more silent undo.** Applying on a stale basis re-reads the BIOS first, because an import writes every row.

## Release Notes v8.6.48

**Revert Center: pick the step you want to go back**
- **The folder is now a chronicle.** The sidebar button opens a timeline of every apply run with its steps, next to the registry snapshots - newest first.
- **Undo single steps.** Tick the steps you want back instead of undoing everything; the rest of the profile stays applied.
- **Back to a point in time.** Pick a run and roll back run by run to exactly that point - the newest run always goes first.
- **Every step says how it returns.** Classic steps return to the value recorded before that run; hardware steps return to Windows default. The row names it.
- **Nothing is undone twice.** Steps already taken back are locked, and a step with no way back is reported instead of counted as done.
- **The emergency .reg files stay reachable.** The offline folder is still one button inside the window, for when the app itself does not start.

## Release Notes v8.6.47

**BIOS Tuner: the crest, and every switch in your hand**
- **Your crest sits in the corner.** The round badge at the top left of the BIOS Tuner shows the suite's crest instead of the two letters. A stand-alone copy without the crest falls back to the letters, so nothing breaks.
- **Every row has a tick.** Basics, Optimized and Expert now put a check box in front of every setting. Only ticked rows are written; everything unticked stays exactly as it is on the board.
- **Every target value can be changed.** Double-click a target value to choose from the values the board actually offers, or type a number. Changed rows are marked in the table and tick themselves.
- **One setting, one row in Expert.** When both the profile and the engine proposed a setting, Expert listed it twice - two rows with two values. Each setting now appears once.
- **A contradiction is reported, not guessed.** If two ticked rows point at the same BIOS setting with different values, neither is written and the confirmation names it. Untick one of them and the other applies.
- **The way back stays one click.** Every apply still writes its own backup first; "Restore backup" in the footer puts the previous state back into the BIOS.

## Release Notes v8.6.46

**Game Mode always releases what it paused**
- **Turning Game Mode off during a game frees every paused program.** Programs could stay paused when a game kept running and the mode was switched off in between - they then had to be ended by hand. Everything the switch pauses is now released again.
- **Pausing the same program twice no longer stacks.** A program that had been paused in more than one pass survived a single release and stayed frozen. The switch now checks what is already paused before it pauses anything, and it releases a program until it is verifiably running again.
- **The automatic watcher acts on a change, not on a state.** It pauses when a game appears and releases when the game ends - switching Game Mode off during a game now stays off.

## Release Notes v8.6.45

**The frame limiter takes effect at once**
- **"Set" changes the frame rate while the game is running.** Until now the value was only stored and took effect from the next launch - a limit set during a session never reached the running game. It does now, without restarting anything.
- **"Unlimited" really removes every limit.** A limit left behind in the base profile could keep capping the game even after "Unlimited" was pressed. Every place the suite can write is cleared now.
- **The status line says what is happening.** It shows the frame rate measured inside the running game and, when the running game is not ready for a change yet, tells you to restart it once instead of claiming success.
- **The install-time self-check leaves an existing driver service alone.** It reports a driver that still points at an older installation instead of reconfiguring it mid-check. A missing service is still created, otherwise the check would have nothing to verify.

### BIOS Tuner: one profile for the 7800X3D, less risk

- **PBO keeps AMD's standard limits** (162 W / 120 A / 180 A). Above those the 7800X3D only gets warmer - the cache sits on the cores and the temperature ends the boost before the power limit does.
- **The curve starts at -20 instead of -30.** -20 runs on practically every 7800X3D; -30 tips over on many chips and ends in a restart loop. The warning above the Expert step now names the way back and the test that proves it.
- **Boost override is capped at +100 MHz.** The 7800X3D tops out around 5.05 GHz, so anything above that is paid for in voltage without arriving as clock.

### Note

- A network value the suite wrote for years is gone: it had no measurable effect. The value next to it stays, and it is now described correctly (it is a specific setting, not an "off" switch).

## Release Notes v8.6.44

**The game link arrives on its own**
- **The desktop link is read in both forms.** Windows stores a downloaded game link either as a shortcut or as a small internet shortcut file. Both now count when "Set game path" looks for the game, and both can be imported.
- **Pasting no longer needs the keyboard.** The link field is filled from the clipboard the moment it opens, and "Set game path" gained an entry that takes the link straight from the clipboard - one click, no typing.
- **A profile without a game name inherits the only game.** When the suite knows exactly one launch target - or the desktop holds exactly one game link - a profile named after its date starts with it. With several games the dialog still asks instead of guessing.

## Release Notes v8.6.43

**The game starts without typing the launcher link**
- **Launch Game finds the link itself.** A profile that names no game - for example a session named after its date - now uses the launcher link of the only game registered in the suite. For Fortnite that link ships with the app, so such a profile starts without any dialog.
- **Shortcuts are found, not pasted.** "Set game path" has a new entry that looks for the game's desktop shortcut and stores the link it carries. Profiles with a registered game path are filled at startup, without opening the dialog at all.
- **Copying a shortcut now works in the link dialog.** Copying a desktop shortcut puts a file on the clipboard, not text - pasting into a text field therefore did nothing. The dialog reads a copied shortcut directly and offers its link.

## Release Notes v8.6.42

**The frame limiter acts while the game runs**
- **Set takes effect at once.** The frame limiter writes both paths every time: the driver profile for every future start, and the live value through RivaTuner Statistics Server for the game that is already running. No switch to forget.
- **The suite starts RivaTuner Statistics Server itself** when it is installed but not running — a live limit only reaches a game that starts after the server does.
- **The status line says which effect really happened** — live now, or from the next game start, with the reason when one path was unavailable.
- **Unlimited removes every limit the tool has set.** A system-wide limit could previously survive and keep capping the game while the tool reported it as removed.
- **A game profile no longer caps the whole machine.** A value saved for one game was also written system-wide, so it applied to the desktop, the browser and every other game.
- **The status says when a value takes effect**, instead of reading as active now when the driver applies it at the next game start.

**The BIOS Tuner has a way back**
- **Restore backup.** One button writes the state from before the last change back to the BIOS. It names the file and its date first, then asks for confirmation; a restart applies the old values.
- **A safety copy is taken automatically** before a profile is written, including the first run where no earlier export exists.

## What changed since 8.6.31

**What arrived since 8.6.31**
- **Profiles are one file now.** "Share profile" writes the whole profile - tuning and game session - into a single `.hypertune` file. It is encoded, and import asks before replacing an existing name.
- **Closing the suite gives the machine back.** Game Mode suspension and Thread Tuner priority, affinity and efficiency mode are restored on exit; nothing stays frozen or boosted.
- **A saved profile keeps what you changed**, and Auto-Tune no longer resets a recorded choice.
- **IPv6 is measured instead of rewritten**, the MTU probe can climb again, and German Windows no longer blinds the network check.
- **The start board stops promising twice**; the banner and mascot ship with the setup again.
- **Older Intel CPUs start again:** the build no longer requires AVX-512, and a failed driver check shows a dialog instead of a silent exit.

**One thing to do:** a serial issued before 19.10.2026 needs one fresh activation after this update.

See [CHANGELOG.md](CHANGELOG.md) for the full history.

<details>
<summary><strong>Full prerequisite list (target machine)</strong></summary>

| Requirement | Scope | Why |
|---|---|---|
| Administrator start | Mandatory | Kernel driver, bus configuration, boot settings |
| Antivirus exclusion for install folder | Strongly recommended | Kernel driver is classified as a generic "Hacktool" by pattern-based AV engines |
| BIOS: CFG Lock disabled | Intel platforms only | Firmware-locked power settings reject low-power-state writes; the engine detects and reports this |
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
The tool uses documented operating system and driver interfaces wherever they exist. There is no injection, no hooking, no memory manipulation of other processes. The frame limiter uses the official driver settings interface — the same one the NVIDIA Control Panel uses. The live path does not inject anything itself: it hands the value to RivaTuner Statistics Server, which you install and run yourself. Kernel access is used to read and write your own hardware's configuration registers. Close the tool before gaming if you prefer a minimal process footprint.

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
