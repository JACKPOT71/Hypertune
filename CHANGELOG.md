# Changelog

All notable changes to Hypertune are documented here, newest first. This is the public history: it describes what changed for the user, not how it is implemented. Detailed engineering notes stay with the source.

## 8.6.39 - 2026-10-24

### The profile folder carries profiles, not the workshop

#### Changed
- **Four profiles instead of eighteen.** The shipped folder had collected every working copy of the master profile: test builds, superseded iterations, two files that were identical to the default profile and one that carried a single setting. What ships now is `Windows-Default` (the unload target), `14.10.2026` (master with a launch link), `Fortnite_Competitive_22.10.2026` (the active one) and `Auto Fortnite 360` (the Smart Auto-Pilot profile).
- **Helper files stay behind.** Backup copies, the machine fingerprint and the author's active-profile marker no longer travel; the fingerprint now lists only profiles that exist. The game sessions were cleaned the same way.

#### Notes
- **A serial issued before 19.10.2026 needs one fresh activation** after this update.

## 8.6.38 - 2026-10-24

### A profile is one file now - encoded, and it asks before overwriting

#### Added
- **Central "Share profile" card on the start board.** One dropdown, two buttons, one file: `<name>.hypertune`. The export merges the target profile and the game session, so the user never has to know that two stores exist.
- **Import asks instead of overwriting.** An existing name offers Replace / Keep as copy / Cancel. Replace writes both stores under the same name; copy keeps the `-2` suffix. An imported profile is selected, not applied.

#### Changed
- **The shared file is encoded**, like the shipped templates. It is no longer a readable recipe, but import still reads the older plain files, so nothing shared before breaks.
- **Six languages** for the new card.

## 8.6.37 - 2026-10-24

### Closing the suite gives the machine back what it borrowed

#### Fixed
- **A browser no longer stays suspended after the suite closes.** The Game Mode watcher could still see the open game during shutdown, suspend the launcher and the browser again - and then the window was gone, so nothing resumed them. The watcher is stopped before the first resume now, and a tick that was already queued returns immediately while the window closes.
- **The Thread Tuner gives the target process its values back.** Priority, affinity and EcoQoS belong to the browser or the launcher, not to Hypertune. Closing the suite restores what was read before the change; anything that could not be restored is named in the shutdown diagnostics.

#### Changed
- **The shipped tune profiles are no longer plain text.** They travel encoded and are read through the same path as a customer profile; templates are no longer copied into the data folder on first start.
- **The start board stops promising twice.** "Optimize (Apply && Save)" is gone - it ran the same scan as the strip below it while the label promised apply and save. The Hyper trophy only appears on a synced machine, and Smart Auto-Pilot sits in the score card.
- **Unchanged by design:** hardware and registry values written by the boot chain stay persistent. This release restores the process state Game Mode and the Thread Tuner changed.

## 8.6.36 - 2026-10-23

### IPv6 is measured, not assumed - and the MTU probe can climb again

#### Fixed
- **IPv6 is reported instead of rewritten.** The default now measures address, route and echo and leaves the system value alone; replacing it stays an explicit choice.
- **The MTU probe can climb again.** The probe raises its own ceiling for the measurement, takes the smallest confirmed value, and writes nothing when fewer than two targets answer. IPv6 gets its own MTU, and a revert no longer restores values that were never written.
- **German Windows no longer blinds the network check.** Five values sat permanently at "not measurable" because the output was translated; the reader now uses the untranslated form and resolves adapters by their device description again.

#### Changed
- **The sidebar lost two entries** (Quality Self-Check and the separate network bench), the duplicate "Optimize" button is gone, and the header shows the banner.
- **The setup carries the banner and the portrait**, without which both were blank in every standalone build.

## 8.6.33 - 2026-10-22

### The frame limiter reaches the game - and the start check says what it could not measure

#### Fixed
- **A 360 FPS cap never arrived at Fortnite.** It was written to the global driver profile, which only applies to applications without a profile of their own. With a resolvable program name the game's own profile is written as well.
- **The session status measured a different place than the apply wrote to.** Status and apply now read the same place, so a set cap no longer shows as "no limit set".
- **The limiter no longer blocks the game launch.** A missing cap is a visible hint, not a launch criterion; when the game ends the cap is removed from both places.
- **The start check no longer hides what it could not measure.** Rows that could not be read stay on the board as hints instead of disappearing and leaving a perfect-looking score.

## 8.6.32 - 2026-10-22

### A saved profile keeps what you changed in the tool

#### Fixed
- **A manual change disappeared on the next save.** The profile card wrote the last session snapshot back over the profile. The profile is the authority now; the session only fills keys the profile does not carry yet.
- **A session save mirrors only what it actually changed.** Unchanged values leave the profile alone, a changed value wins, and a field the session never had does not delete the profile's value.
- **Auto-Tune keeps a recorded choice** on a second run instead of resetting it to the synthesised base.
- **Verified manual actions are recorded instead of forgotten** - a proven profile import, a power-plan switch, a Thread-Tuner profile or a Network-Tweaker profile now survive the next save.
- **Closing the window no longer ends in an error code.** A live probe still running at close was torn out; the probes stop cooperatively now, and the shutdown no longer leaves a crashing thread behind.

#### Notes
- **This build is unsigned.** Windows SmartScreen will warn on first run; verify the SHA-256 of the installer and the signature of the manifest against the release page.

## 8.6.31 - 2026-10-21

### A diagnosis that no longer kills the app

#### Fixed
- **"Export diagnostics" no longer ends the app.** The worker outlived the slot that reported it; the reference is now released on its finished signal, for the export and the upload, and the busy guard asks whether the worker is still running.
- **The two probes that reach into foreign code run in a child process.** A crash or a timeout becomes a finding inside the support zip instead of a vanished window.
- **The isolated probe writes UTF-8 itself**, so a German console code page no longer turns the zip contents into an encoding error.
- **In the built EXE the compiled engine wins** over a leftover source file next to the executable.
- **A failed driver check is shown instead of ending the app silently** - a dialog naming the file plus a crash log entry.

## 8.6.30 - 2026-10-20

### One activation, and a build that starts on older CPUs

#### Notes
- **Every serial issued before 19.10.2026 must be activated once more.**

#### Fixed
- **The binary no longer requires AVX-512.** The build compiler was targeting the build machine's CPU in its link step; a Comet Lake machine died with an illegal instruction before any window appeared. Both pipelines now compile through a baseline wrapper and verify the shipped binary.

#### Added
- **Intel network latency coverage was extended** to the interrupts, delay and power-saving fields the detected card family actually documents - and skipped, not guessed, on a family without a documented field.
- **Intel clock modulation and the uncore ring have their own switches**, each gated by firmware state and each with its own revert.
- **The Realtek 2.5G step now also covers PCIe power saving in the adapter**, migrated into existing profiles.
- **A profile can be built for hardware that is not in this machine**, marked "profile only" instead of locked.
- **RX High Priority uses the real ports of the running game** instead of filling the table with a guessed range.

## 8.6.28 - 2026-10-04

### The effect card measures watts

- Every A/B run reports the CPU's own energy counter per phase, and each row names which counter produced the figure or says that none is available.
- The read-only hardware catalogue grew, with every field checked against the vendor documentation for the exact CPU family.

## 8.6.27 - 2026-09-30

### The License button works again

- The lower sidebar button opened nothing after a navigation entry was removed. It opens the licence page directly now.

## 8.6.26 - 2026-09-30

### Sidebar cleanup and release announcements

- The sidebar no longer shows "License" twice; the lower button is the only door to the licence page.
- The lower sidebar reads as one colour gradient.
- Discord messages are always English, and the release channel announcement carries `@everyone`.

## 8.6.25 - 2026-09-30

### Release channel and a consistent name

- **A second Discord channel** can be configured for releases; both channels receive the same text.
- **The in-app update returns to the app** after the installer finishes.
- **"Beyond" is renamed to "Jackpot"** everywhere - power plans, action names, help texts and translations. Imported plans are renamed to the file stem.
- **The engine-failure dialog is styled like the suite** and offers an elevated restart and details.

## 8.6.24 - 2026-09-30

### Honest verdicts

- **The GPU clock lock is proven by measurement** on drivers that no longer expose the applied value: the pin counts when the clock holds its value, and a floating clock stays "unverified".
- **Clearing the frame limiter no longer reports a failed delete** when the driver only leaves a zero entry behind.
- Two hard-coded German evidence lines now translate with the rest of the interface.

## 8.6.10 - 2026-09-23

### Game launch, frame limiter and benchmarks

- **Game Launch card:** one click applies the whole session - network profile, thread tuning, power plan, GPU lock, game mode - with a live readiness checklist and a smart launch continuation.
- **Driver-level frame limiter per game:** no injection, read back from the driver, re-verified on every launch and cleaned up when the game ends.
- **Benchmarks card:** CapFrameX capture import, honest statistics and a classified frame-limit advisor.

## Earlier releases

The 8.6.5 to 8.6.9 builds introduced the in-app update system with checksum-verified installers, per-core write acceptance reporting, the extended driver diagnostics, the automatic antivirus exclusion and the prerequisites chapter in the help manual. Their full notes remain on the [Releases](https://github.com/JACKPOT71/Hypertune/releases) page.
