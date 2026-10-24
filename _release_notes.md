### The profile folder carries profiles, not the workshop

- **Four profiles instead of eighteen.** The shipped folder had collected every working copy of the master profile: test builds, superseded iterations, two files identical to the default profile and one carrying a single setting. What ships now is `Windows-Default` (the unload target), `14.10.2026` (master with a launch link), `Fortnite_Competitive_22.10.2026` (the active one) and `Auto Fortnite 360` (the Smart Auto-Pilot profile).
- **Only the profiles travel.** Backups, the machine fingerprint and the author's active-profile marker stay on the build machine. The game sessions were cleaned the same way.

### Since 8.6.31 - the eight versions in this upgrade

- **Profiles are one file now.** "Share profile" writes the whole profile - tuning and game session - into a single `.hypertune` file. It is encoded, and import asks before replacing an existing name.
- **Closing the suite gives the machine back.** Game Mode suspension and Thread Tuner priority, affinity and efficiency mode are restored on exit; nothing stays frozen or boosted.
- **A saved profile keeps what you changed**, and Auto-Tune no longer resets a recorded choice.
- **IPv6 is measured instead of rewritten**, the MTU probe can climb again, and German Windows no longer blinds the network check.
- **The start board stops promising twice**; the banner and mascot ship with the setup again.
- **Older Intel CPUs start again:** the build no longer requires AVX-512, and a failed driver check shows a dialog instead of a silent exit.

### Before you start

- **A serial issued before 19.10.2026 needs one fresh activation** after this update.
