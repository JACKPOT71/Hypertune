### A labelled installer, and the tuning this machine runs

- **This build is unsigned, and it says so.** Windows will show "Unknown publisher" on first run; that is expected for this release. The release page names the SHA-256 and ships `SMARTSCREEN.md` with the two clicks it takes. Nothing here is called signed, verified or safe.
- **The checksum travels with the download.** Every setup now gets a `<name>.sha256` file next to it, so the file can be checked before it runs. The release text names the same value.
- **The tuning is unchanged.** `Jackpot_7800X3D_Fortnite`, `Jackpot_Hypertune.nip` and `Jackpot_Hypertune.pow` are the same files from 8.6.54: the 150-setting NVIDIA base profile, the 40-value power plan, the 1920 MHz GPU lock and the unlimited frame limiter. No profile was rebuilt for this release.
- **Your install stays yours.** The setup replaces the program files; profiles, the active power plan and the licence stay in place.
