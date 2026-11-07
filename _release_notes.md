### Priority boost and Safe Mode improvements

- **The Windows priority boost now behaves consistently.** The card, a saved profile and the automatic startup re-apply show the same state.
- **The way back is always available.** Restoring the boost is a single step and stays available when the app closes or restarts.
- **The card updates immediately.** After a change, it shows the current state without restarting the app.

- **Safe Mode now has an automatic way back.** Hypertune sets up the automatic return before it changes the boot setting; if that is not possible, nothing is changed. A leftover Safe Mode setting is cleared at the next start.
- **This build is unsigned, and it says so.** Windows will show "Unknown publisher" on first run; that is expected for this release. The release page names the SHA-256 and ships `SMARTSCREEN.md` with the two clicks it takes.
- **SHA-256 of `Hypertune_Setup_8.6.65-unsigned.exe`:** `d5dcc5c8940e763152640d1e35b70f0561d59db23e5efb3ad1a11b7f365c5ddb`. The `.sha256` file next to the setup carries the same value.
- **Download:** [Hypertune on GitHub](https://github.com/JACKPOT71/Hypertune) · [Direct setup](https://github.com/JACKPOT71/Hypertune/releases/download/v8.6.65/Hypertune_Setup_8.6.65-unsigned.exe).
