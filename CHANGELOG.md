# Changelog

All notable changes to Hypertune are documented here. Versions are newest first. Dates follow the GitHub release tags.
## 8.6.30 — 2026-10-20
### Fixed
- **The 8.6.29 binary could not start on a 10th-gen Intel CPU.** It ended with `0xC000001D` (`STATUS_ILLEGAL_INSTRUCTION`) before any window appeared. The build targeted the build machine's CPU when compiling, and the linker produced its runtime for that CPU as well: the artifact carried 102 AVX-512 instructions. This build carries none — measured across 15,578 functions and 7.57 M instructions
- **Compiling and linking now use the same fixed CPU baseline**, so link-time optimisation stays on without bringing the problem back
- **A failed driver check is reported instead of ending the app silently.** The bundled WinRing0 files are still verified before the first hardware module loads; a failure now shows a message naming the file and writes `crash_entry.txt`, instead of a windowless exit code. The check itself is unchanged

## 8.6.29 — 2026-10-20
### Fixed
- **Applying a profile no longer shortens the saved start chain.** The chain is written once and then treated as the profile's own: a later apply re-reads it instead of rebuilding it from a scan, so the nine RX High Priority ports and the fourteen device addresses stay in the BAT across reboots
- **An explicit Apply Everything is never swallowed.** The rocker's position is a state, not a click filter: pressing the button always starts exactly one session, even when it already shows ON
- **A network value that cannot be read back is no longer counted as removed.** For a removal, "not set" is the desired result — and a refused read used to look exactly the same. Unverifiable removals are now reported as unverified instead of successful
### Changed
- **RX High Priority writes the profile's ports, not a guessed block.** The old template filled all 128 slots with the beginning of the UDP range, covering 119 of 53,001 ports. A range is now written only when it fits completely; otherwise the profile's fixed ports are used. Ports of a running game are read live, used for that session and never saved
### Added
- **Energy and average power in every A/B check**, read from a probed hardware counter and named per row (`AMD L3/CCD`, `Intel Package`, `Intel DRAM`, or "not available"). Unsupported hardware reports "not available" instead of a number
- **Read-only register catalogue grown to 56 entries**, each field checked against the processor documentation for the exact CPU. Catalogue only — the app writes none of them

## 8.6.27 — 2026-09-30

### Fixed
- **The License button opens the license page again.** The click had stopped working in 8.6.26; this release restores it. No other changes

## 8.6.26 — 2026-09-30

### Fixed
- **Sidebar no longer shows "License" twice**: the stray icon-less navigation entry is gone; the License button in the lower sidebar is the only door to the license page (page itself untouched)

### Changed
- **Lower sidebar reads as one blue gradient**: License `#0090B8` → BSoD Guard `#00B8E8` → Repair Driver Service `#00D5FF` → Reboot System `#33EFFF`, each hover one step brighter; the version line closes the gradient in the brightest blue (`#4DF5FF`)
- **Discord messages are always English** regardless of the suite's UI language; the automatic release announcement carries **@everyone** on the release channel while the main channel stays quiet

## 8.6.25 — 2026-09-30

### Added
- **Second Discord channel (release channel)**: optional second webhook in the update-notify dialog; releases are announced to both channels with the same formatting and the same signed release text. The once-per-version marker stays shared, so the main channel can never be silenced by a dead second one
- **Post-update auto-return**: the in-app update runs the installer with /PASSIVE, closes the suite cleanly and the installer's post-install launch brings it back automatically (visible checkbox, no hidden autostart)

### Changed
- **"Beyond" renamed to "Jackpot" everywhere**: power plan files (`Jackpot_Maximum.pow`, `Jackpot-PERFORMANCE-*.pow`), S.U.C.K. action ids and cmdlets (`jackpot-ndis-global`, `Jackpot-GlobalOffloads`), vendor profiles, help texts and translations. Existing snapshots/journals on disk are untouched
- **Engine-failure dialog rebuilt**: suite-styled dialog instead of the grey Windows MessageBox, with built-in "Run as administrator" (one-click elevated restart) and "Show details" (opens crash/startup log); duplicate failures within two minutes show exactly one dialog instead of a stack

### Fixed
- **Language switch is honest**: changing language now asks to restart (or explicitly defer) instead of leaving half the interface in the old language — newer pages build their texts only at startup, and the app no longer pretends otherwise

## 8.6.24 — 2026-09-30

### Fixed
- **GPU clock lock verdict falls back to behavioral proof** on drivers without the value read-back channel (610.88 deprecates `clocks.applications.*`): the pin is proven by measurement — clock fixed at the requested value, spread ≤ 2 MHz, plus the driver's "Applications Clocks Setting" throttle reason. A pin at a different value is named; a floating clock stays honestly unverified. The lock mechanism itself is untouched
- **Frame limiter**: clearing a limit no longer reports "delete did not stick" — the driver's leftover value-0 entry now reads as "no limit set" on both the clear and read path
- **Quality Self-Check page**: two hard-coded German evidence lines now translate in all seven languages

### Changed
- Discord update messages embed the full release text from the repository's single source file (`_release_notes.md`) — GitHub release and Discord stay in sync from one edit
- Discord webhook dialog buttons use the suite's ModernButton style
- Sidebar version label lightened (`#FF6B85`)

### Security
- Manifest remains Ed25519-signed; notes now travel inside the signed manifest, so the Discord embed inherits the same tamper protection as the download URL

## 8.6.10 — 2026-09-23

### Added
- **Game Launch card**: one-click full-session apply (network profile, thread tuning, power plan, GPU lock, game mode) with a live readiness checklist and smart launch continuation — the game never starts untuned
- **Driver-level frame limiter** per game via the NVIDIA driver settings API: no injection, live read-back from the driver, re-verified on every launch, automatic cleanup of orphaned driver entries
- **Benchmarks card** with CapFrameX capture import, honest statistics (average, 1 % low, latency) and the classified frame limit advisor (grades A–D)
- **Mission Control**: Game Mode and Thread Tuner united in one process list with park / throttle / boost actions, plus the Game Catcher (live process list, one-click name capture)
- **Live State Probe card**: read-only, register-level verification of what actually survived the reboot
- Game artwork shipping with the installer (Fortnite, Valorant; extendable by dropping in JPGs)
- Thread Tuner profile sharing via strictly validated JSON export/import

### Changed
- Full six-language sweep (EN, DE, FR, ES, RU, ZH): every dashboard card follows the language switch; an automated pairing test now guards it
- Unified dashboard color language — red is reserved for errors and NOT-GO verdicts
- Game Session toggle remembers its selection across reboots
- Latency measurement against selectable targets with live sparkline history
- Release test battery extended to 22 automated suites

### Fixed
- Dashboard text freezing in the start language (header status, advisor verdicts, auditor report now retranslate)
- Update card wording for the up-to-date state and a clearer offline/re-check message in all six languages

## 8.6.9 — 2026-09

### Added
- Smart Update inside the app: manifest check, installer download, SHA-256 verification before install
- Red sidebar version display; honest "up to date" update wording
- Installer registers an optional antivirus exclusion for the installation folder
- Prerequisites documentation chapter: platform requirements per feature, per vendor

### Fixed
- Boot engine now reports per-core write acceptance honestly — a refused low-power-state write logs "NOT applied" instead of success
- Driver diagnostics extended: detects missing-driver-next-to-executable and USB helper-driver conditions with plain-language fixes
- Frozen-mode path handling: engine, BATs and scheduled task resolve inside the installed layout

## 8.6.8 — 2026-09

### Added
- Checksum-signed update manifest per release; checksum mismatch = hard fail, never a silent install
- One-click Defender exclusion handling in the maintenance area

### Changed
- Update card redesign with a single action button and quiet daily polling

## 8.6.7 — 2026-09

### Fixed
- WinRing0 driver loading on fresh installs: the driver file now ships next to the executable (Program Files paths with spaces resolved)
- Game Mode suspension reliability and crash-guard restore on abnormal exit

## 8.6.6 — 2026-09

### Fixed
- CPU vendor label on the dashboard reporting the wrong platform on Intel systems
- Driver service repair flow

## 8.6.5 — 2026-09

### Added
- RTL8125 Deep-Latency-Tuner as a selectable premium profile (deep apply, revert, NIC restart) for the Realtek RTL8125/8126 family
- 5-day full-feature auto trial on first launch

### Changed
- Credits and documentation updated; NIC profile scope documented in-app

## 8.6.x and earlier — 2026

- Game Mode with foreground detection, name-based process matching, suspendable background processes, journal and crash guard
- S.U.C.K. network protocol engine with apply → verify → diff, portable profiles and snapshot-before-write
- Win Tweak Verifier, Registry Shield, device cleaner and driver repair utilities
- Latency measurement with jitter analysis, DPC/ISR reporting, TSC verification
- PCIe/CPU/USB hardware layer with read-back verification, boot task persistence and GPU clock pinning
- Premium licensing with lifetime keys and auto trial
