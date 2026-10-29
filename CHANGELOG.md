# Changelog

All notable changes to Hypertune are documented here, newest first. This is the public history: it describes what changed for the user, not how it is implemented. Detailed engineering notes stay with the source.

## 8.6.56 - 2026-10-29

### A labelled installer, and a checksum you can check

- **Unsigned builds are labelled, not hidden.** The setup ends in `-unsigned`; Windows will show "Unknown publisher" on first run. `SMARTSCREEN.md` explains the two clicks, and a `<name>.sha256` file sits next to the download.
- **The checksum is the same in the release text and the file.** Compare it before running the setup.
- **The trial period says five days in every language.** The app and the licence page now agree; an existing trial keeps its start date.
- **Nothing needs to be re-entered.** An activated licence stays activated; profiles, the active power plan and settings stay in place.
- **No tuning changes.** Profiles, power plan and measurement paths are unchanged.

## 8.6.55 - 2026-10-29

### Five days, a cleaner build, and profiles you can still share

#### Fixed
- **The licence window says five days in every language.** The code already granted five days, but the interface said three - in all seven languages.
- **A developer-only path is no longer part of the build.** The benchmark capture fallback pointed at one machine's desktop and was a dead path everywhere else.

#### Changed
- **An activated licence stays activated.** The update keeps the existing state; no re-activation is needed.
- **Profiles stay shareable.** The profile format is unchanged, and a profile from another machine still imports.

## 8.6.54 - 2026-10-29

### The plan, the preset and the profile this machine runs

#### Added
- **`Jackpot_7800X3D_Fortnite` ships as a profile.** It carries the state of the tuning machine in one file: power plan, GPU clock lock at 1920 MHz, Game Mode, the Competitive Gaming thread profile, the network profile, the Realtek/NIC/PCIe/MSR/USB chain and an unlimited frame limiter.

#### Changed
- **`Jackpot_Hypertune.pow` is checked against the running scheme.** All 40 values of the active plan were read back and compared with the shipped file - no difference. What the setup installs is the plan the measurements ran on.
- **`Jackpot_Hypertune.nip` is the single Jackpot preset in `nip/`.** One base profile with 150 settings, applied machine-wide; the older Jackpot presets are gone from the folder and are removed from an existing install on update.

## 8.6.53 - 2026-10-28

### Frame limiter: the executable that actually runs

#### Fixed
- **The limit landed in a profile the game never loads.** Fortnite starts as `FortniteClient-Win64-Shipping_EAC_EOS.exe`, while the tool wrote `FortniteClient-Win64-Shipping.exe`. RTSS picks its profile by file name, so the value was never applied: the status line said "saved", the game stayed uncapped.
- **Every executable of a game is written now.** The resolved name, its siblings in the game folder, the running process and every existing profile of the family all receive the same value.
- **Unlimited clears the whole family.** A leftover cap in a second executable can no longer survive the reset and keep limiting.
- **The read-back is per profile.** If one of them refuses the value, the message names it instead of claiming success.

## 8.6.52 - 2026-10-28

### Jackpot's NVIDIA presets on board - and a profile list that only shows current stands

#### Added
- **Three NVIDIA presets from Jackpot.** `Jackpot_SmoothDX12.nip` (DWM low latency, three pre-rendered frames, 10 GB shader cache, highest refresh), `Jackpot_MaxFPS.nip` (V-Sync and G-Sync off, texture filtering on High performance) and `Jackpot_LowLatency.nip` (ultra low latency). Each one carries a base profile plus the Fortnite executables, so it applies to the game and not to the whole machine.
- **The power plan was already on board.** `Jackpot_Hypertune.pow` has been in `pow/` since 8.6.51 - the same file, byte for byte.

#### Changed
- **The setup ships only current profiles.** The old master stand `14.10.2026` still travelled along and sat in the profile list next to the current saves. It stays in the working tree as a test fixture only.

#### Fixed
- **A retired profile would have stayed forever.** Inno deletes only what it installed itself, so a dropped template survived every update in the program folder - and kept showing up in the list. The installer removes it by name now.

## 8.6.51 - 2026-10-27

### BIOS Tuner: six more switches, three corrected names

#### Added
- **PCIe payload and read request at the maximum.** `Maximum Payload` and `Maximum Read Request` sat on `Auto`; the Optimized profile now asks for 4096 bytes per transaction - fewer headers for the same amount of data.
- **Network boot off.** `LAN Boot`, `Onboard PCIE LAN PXE ROM`, `IPv4 PXE Support` and `IPv6 PXE Support` are switched off, so the BIOS no longer looks for a boot server during POST.
- **USB mass storage driver off.** `USB Mass Storage Driver Support` is disabled; a Windows installer or rescue stick from USB needs that switch back on in the BIOS first.
- **One sentence of warning comes with it.** The Optimized tier now says out loud that network boot and the USB mass storage driver get switched off, before anything is written.

#### Fixed
- **The LAN controller of an AM5 board was never found.** "Intel LAN Controller" looks for a name the board does not know; it calls its chip "Realtek LAN Controller". The name is an alias now.
- **AER was invisible, and Thunderbolt was matched by similarity.** The board calls "Enable AER Cap" -> "Advanced Error Reporting (AER)" with the values Not Supported/Supported/Auto; the rule names that block and its value. "Thunderbolt Support" was matched to "Thunderbolt L1SS Support" only because the names look alike - a different switch on a different section. The real block, "Thunderbolt/USB4 (Intel JHL8540 controller) Support", is named explicitly.
- **Every switch was checked against a real board before shipping.** On the reference export, 67 of the 103 Optimized switches find their block; the rest are names other boards use.

## 8.6.50 - 2026-10-27

### Measurement run: the governor decides whether the numbers count

#### Added
- **"Measurement run" card.** Record A, change one lever, record B, compare - one block per press, with a plain-words line saying what comes next. PresentMon reads along (ETW), the game stays in front.
- **Spread as its own row.** Spread in percent, 99.9th percentile frame time and stutters per ten minutes. A tweak that lifts the average and the spread with it now shows up instead of hiding behind a nicer mean.
- **The clock floor of every run.** The card records what the platform allowed while it captured, and whether the processor ever reported that it could not deliver the minimum.
- **Optional measurement mode "clock pinned".** Holds the clock for A and B so a jumping clock cannot be mistaken for an effect. It is a measurement, not tuning: one button restores the exact value that was there, and the next restart removes it anyway.

#### Changed
- **Blocks instead of two record buttons.** Which side a block belongs to is decided by the tick "lever is applied", not by the order of presses - a forgotten switch can no longer turn the reference into the new side.
- **Warm-up and pauses belong to the run.** The first capture after a change is discarded, and there is a pause between captures so one capture does not measure the heat of the previous one.
- **The A/B chain uses the same gate.** The chain report now says "no verdict" when its two sides stood on a different clock floor, and keeps the statistics beside it.

#### Fixed
- **A measured zero was read as missing data.** "No stutters in ten minutes" is a valid, common value; it was treated as "no data" and could block a verdict. Zero now counts as zero, and a ratio against zero is refused instead of invented.
- **The clock trace could not be read at all.** The offered performance ladder was never part of the recorded series, and two values stood as plain numbers where the evaluation expected fields - so the trace reported "not readable" on every machine, and the protection against a changed clock floor would never have triggered. Both are fixed, and a test now proves the trace reads what it announces.
- **An empty register is reported as empty.** When the platform does not publish an allowed ceiling, the window says so and shows a dash - instead of "0 of 255", which would be a statement nobody made.

## 8.6.49 - 2026-10-27

### BIOS Tuner: a way back you can read

#### Added
- **"Back to stock" in the footer.** One button, one question, restart - the board is back to the state from before the first change.
- **The stock state is captured automatically.** Before the first write the tool saves the untouched BIOS under a readable name; the button is live from that moment on.
- **"Other state ..." lists every saved state.** Stock, Basics, Optimized, Expert - with date and file name, newest first, stock always on top.

#### Changed
- **Saved states have readable names.** `Stock_BIOS_before_everything_YYYY-MM-DD_HHMM.txt`, `BIOS_Optimized_...`, `BIOS_Expert_...` instead of `BIOSSettings_backup_<stamp>_basics`.
- **A register (`snapshots.json`) names the kind of every state.** Names are re-read from the folder, so a lost register costs nothing.
- **Applying re-reads the BIOS when the basis is stale.** An older loaded file no longer gets written over everything; the window refreshes first and asks for one more click.

#### Fixed
- **Restore no longer guesses.** The old code took the newest file with `_backup_` in the name and, on 27.10, restored the wrong state - the result looked like "nothing changed". The stock entry is now explicit.
- **Silent undo is gone.** Reverting while an old stock file was loaded rewrote all 2268 rows and cleared the Optimized values along the way.

## 8.6.48 - 2026-10-27

### Revert Center: pick the step you want to go back

#### Added
- **The sidebar button opens a chronicle.** Every apply run is listed with its steps and the state before it, next to the registry snapshots - newest first.
- **Single steps can be undone.** Tick exactly the switches you want back; the rest of the profile stays applied.
- **"Back to this point" rolls back run by run.** The newest run is always taken back first; the rollback stops and says so if a step is not confirmed.
- **Every row names its way back.** Classic steps return to the value recorded before that run, hardware steps to Windows default.

#### Changed
- **The emergency .reg folder moved inside.** The offline files are still one button away, but they are no longer the only thing the button does.
- **A step with no way back is reported.** If the recorded pre-state is missing, the window says "no way back" instead of claiming the switch was restored.

## 8.6.47 - 2026-10-27

### BIOS Tuner: the crest, and every switch in your hand

#### Added
- **Your crest sits in the corner.** The round badge at the top left of the BIOS Tuner shows the suite's crest instead of the two letters. A stand-alone copy without the crest falls back to the letters, so nothing breaks.
- **Every row has a tick.** Basics, Optimized and Expert now put a check box in front of every setting. Only ticked rows are written; everything unticked stays exactly as it is on the board.
- **Every target value can be changed.** Double-click a target value to choose from the values the board actually offers, or type a number. Changed rows are marked in the table and tick themselves.

#### Changed
- **One setting, one row in Expert.** When both the profile and the engine proposed a setting, Expert listed it twice - two rows with two values. Each setting now appears once.
- **A contradiction is reported, not guessed.** If two ticked rows point at the same BIOS setting with different values, neither is written and the confirmation names it. Untick one of them and the other applies.
- **The way back stays one click.** Every apply still writes its own backup first; "Restore backup" in the footer puts the previous state back into the BIOS.

## 8.6.46 - 2026-10-26

### Game Mode always releases what it paused

#### Fixed
- **Turning Game Mode off during a game frees every paused program.** Programs could stay paused when a game kept running and the mode was switched off in between - they then had to be ended by hand. Everything the switch pauses is now released again.
- **Pausing the same program twice no longer stacks.** A program that had been paused in more than one pass survived a single release and stayed frozen. The switch now checks what is already paused before it pauses anything, and it releases a program until it is verifiably running again.
- **The automatic watcher acts on a change, not on a state.** It pauses when a game appears and releases when the game ends - switching Game Mode off during a game now stays off.

## 8.6.45 - 2026-10-26

### The frame limiter takes effect at once

#### Fixed
- **"Set" changes the frame rate while the game is running.** Until now the value was only stored and took effect from the next launch - a limit set during a session never reached the running game. It does now, without restarting anything.
- **"Unlimited" really removes every limit.** A limit left behind in the base profile could keep capping the game even after "Unlimited" was pressed. Every place the suite can write is cleared now.
- **The status line says what is happening.** It shows the frame rate measured inside the running game and, when the running game is not ready for a change yet, tells you to restart it once instead of claiming success.
- **The install-time self-check leaves an existing driver service alone.** It reports a driver that still points at an older installation instead of reconfiguring it mid-check. A missing service is still created, otherwise the check would have nothing to verify.

### BIOS Tuner: one profile for the 7800X3D, less risk

#### Changed
- **PBO keeps AMD's standard limits** (162 W / 120 A / 180 A). Above those the 7800X3D only gets warmer - the cache sits on the cores and the temperature ends the boost before the power limit does.
- **The curve starts at -20 instead of -30.** -20 runs on practically every 7800X3D; -30 tips over on many chips and ends in a restart loop. The warning above the Expert step now names the way back and the test that proves it.
- **Boost override is capped at +100 MHz.** The 7800X3D tops out around 5.05 GHz, so anything above that is paid for in voltage without arriving as clock.

#### Note
- A network value the suite wrote for years is gone: it had no measurable effect. The value next to it stays, and it is now described correctly (it is a specific setting, not an "off" switch).

## 8.6.44 - 2026-10-26

### The game link arrives on its own

#### Added
- **The desktop link is read in both forms.** Windows stores a downloaded game link either as a shortcut or as a small internet shortcut file. Both now count when "Set game path" looks for the game, and both can be imported.
- **Pasting no longer needs the keyboard.** The link field is filled from the clipboard the moment it opens, and "Set game path" gained an entry that takes the link straight from the clipboard - one click, no typing.
- **A profile without a game name inherits the only game.** When the suite knows exactly one launch target - or the desktop holds exactly one game link - a profile named after its date starts with it. With several games the dialog still asks instead of guessing.

## 8.6.43 - 2026-10-26

### The game starts without typing the launcher link

#### Added
- **Launch Game finds the launcher link itself.** A profile that names no game - for example a session named after its date - now uses the launcher link of the only game registered in the suite. For Fortnite that link ships with the app, so such a profile starts without any dialog.
- **Shortcuts are found, not pasted.** "Set game path" has a new entry that looks for the game's desktop shortcut on the desktop, the public desktop and next to OneDrive, and stores the link it carries. Profiles with a registered game path are filled at startup, without opening the dialog at all.

#### Fixed
- **Copying a shortcut now works in the link dialog.** Copying a desktop shortcut puts a file on the clipboard, not text - pasting into a text field therefore did nothing. The dialog reads a copied shortcut directly and offers its link.

## 8.6.42 - 2026-10-26

### The frame limiter can act while the game runs

#### Added
- **Set takes effect at once.** The frame limiter now writes both paths every time: the driver profile for every future start, and the live value through RivaTuner Statistics Server for the game that is already running. There is no switch to forget.
- **The suite starts RivaTuner Statistics Server itself** when it is installed but not running. A live limit only reaches a game that starts after the server does, so waiting for the user to open another program was the reason a set value could do nothing.
- **The status line says which effect really happened** - live now, or from the next game start, with the reason when one path was unavailable.

#### Fixed
- **Unlimited now removes every limit the tool has set.** Previously a system-wide limit could survive and keep capping the game, even though the tool reported it as removed.
- **A game profile no longer caps the whole machine.** A value saved for one game was also written system-wide, so it applied to the desktop, the browser and every other game. It now applies to that game only.
- **The status says when a value takes effect.** It no longer reads as "active now" when the driver applies it at the next game start.

## 8.6.41 - 2026-10-26

### The BIOS Tuner has a way back

#### Added
- **Restore backup.** One button in the BIOS Tuner writes the state from before the last change back to the BIOS. It names the file and its date first, then asks for confirmation; a restart applies the old values.
- **A safety copy is taken automatically.** Before a profile is written, the current state is saved next to the export. This also covers the first run, where no earlier export existed and there was nothing to fall back to.

#### Notes
- **The button stays inactive until a safety copy exists.** The tooltip says why. Nothing is overwritten and no profile is deleted.

## 8.6.40 - 2026-10-25

### The engine finds its driver after an update

#### Fixed
- **A previous installation no longer blocks the start.** If the driver service still points at an older installation, the app now recognises that state, repairs its own service entry and starts the engine - instead of stopping with a driver error.

#### Notes
- **Nothing else changes.** Profiles, tuning and measurements stay exactly as they were; this release only removes that one start blocker.

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
