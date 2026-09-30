============================================================================
 JACKPOT'S HARDWARE REGISTER ENGINE v8.0 - HYPERTUNE EDITION
 Release Package
============================================================================

--- DEUTSCH -----------------------------------------------------------------

A) UPDATE UEBER EINE AELTERE INSTALLATION (Bestandsnutzer):

    1. Das Tool VOLLSTAENDIG schliessen (auch den Hintergrund-Task).
    2. Alle Dateien aus diesem Zip in den BESTEHENDEn Programmordner
       kopieren und beim Nachfragen "Ersetzen/Überschreiben" waehlen.
       Deine persoenlichen Dateien (IMOD_Profile.bat, IMOD_Launcher.vbs,
       Ghidra-Ordner, Logs) sind NICHT im Zip und bleiben unangetastet -
       die geplante Startup-Task bleibt gueltig.
    3. Falls Windows beim Kopieren von "chiptool\WinRing0.sys" /
       "WinRing0x64.sys" einen Fehler meldet (Datei in Benutzung):
       Neustart machen und NACH dem Boot, VOR dem ersten Tool-Start,
       die beiden Dateien erneut kopieren. Ist der Treiber identisch,
       koennen die beiden Dateien auch gefahrlos uebersprungen werden.
    4. WICHTIG - einmalig nach dem Update:
       a) Tool als Admin starten.
       b) "Scan Hardware Radar" ausfuehren.
       c) "Save Startup Profile" klicken und danach NEU STARTEN.
       Grund: aeltere Versionen konnten Startup-Profile OHNE die PCIe-
       Adressen (BDFs) speichern - solche Profile haben bei jedem Boot
       stillschweigend nichts getan. Der erneute Scan + Speichern
       schreibt ein vollstaendiges, funktionierendes Profil.
    5. Hinweis: Die Sprache wird beim Kopieren auf Englisch zurueck-
       gesetzt (neutrale settings.json im Zip). Einmal im Kopf oben
       rechts umschalten - die Einstellung bleibt danach erhalten.

B) NEUINSTALLATION:

    1. Dieses Paket in einen NEUEN Ordner entpacken (nicht ueber eine
       alte Installation kopieren).
    2. "Click_to_Start.bat" per RECHTSKLICK -> "Als Administrator
       ausfuehren". Das Setup installiert bei Bedarf automatisch
       Python 3.11 und alle Pakete (PyQt6, psutil, pefile, capstone).
    3. Im Programm:
       a) "Scan Hardware Radar" ausfuehren (Hardware wird eingelesen).
       b) Tweaks nach Wunsch setzen.
       c) "Save Startup Profile" klicken - das Profil MUSS aus einem
          frischen Scan heraus gespeichert werden (speichert die PCIe-
          Busadressen/BDFs deiner Hardware). Nach Hardware-Aenderungen
          einfach neu scannen und neu speichern.
       d) Neu starten - das Profil wird dann bei jeder Anmeldung
          automatisch ausgefuehrt (Task: IMOD_Startup_Task).

HINWEISE:
- Administrator-Rechte sind fuer alle Hardware-Tweaks erforderlich (MSR,
  PCIe-Konfigurationsraum, MMIO). Ohne Admin laufen nur die Registry-Teile.
- Der "BSoD Guard" schuetzt kritische Root-Ports (MPS Re-Framing wird
  bewusst uebersprungen) - das ist Sicherheits-Feature, kein Fehler.
- Die Sprache laesst sich oben rechts live umschalten (6 Sprachen).
- Treiber-Update gemacht? -> GPU-Seite: "Checkliste nach Treiber-Update"
  benutzen. Der Drift-Monitor auf dem Bento-Dashboard zeigt an, ob Tweaks
  noch aktiv sind ("Re-Check Now").

TROUBLESHOOTING:
- Startet das Tool nicht: "crash_log.txt" im Programmordner pruefen.
- Hardware-Tweaks "Unknown" im Radar: Einmal "Scan Hardware Radar" mit
  Admin-Rechten ausfuehren.
- WinRing0-Dienst-Probleme: Button "Repair Driver Service" unten links.

ANTI-CHEAT-KONFLIKT (WICHTIG FUER GAMER):
  Anti-Cheat-Systeme wie FACEIT AC oder Vanguard blockieren die Kernel-
  treiber WinRing0.sys und RwDrv.sys BEWUSST. In diesem Fall koennen die
  Hardware-Tweaks (PCIe, MSR, USB) nicht angewendet werden - sie bleiben
  auf Stock. Registry- und Netzwerk-Tweaks funktionieren weiterhin.
  Erkennen:
    - Beim Start erscheint ein ROTER HINWEISBANNER im Programm (wenn im
      letzten Boot-Log beide Kernel-Engines blockiert wurden), ODER
    - startup_log.txt enthaelt "WinRing0 Start fehlgeschlagen"
      (OLS_DLL_DRIVER_NOT_FOUND/BLOCKED) und danach nur noch Fehler wie
      "rw.exe command timed out" / "output contained no hex".
  Checkliste:
    1. Anti-Cheat-Client (z.B. FACEIT) vollstaendig beenden oder
       deinstallieren, dann NEU STARTEN.
    2. Tool MANUELL als Administrator starten und startup_log.txt pruefen.
    3. Windows-Sicherheit -> Gerätesicherheit -> Kernisolierung:
       "Speicherintegritaet" (HVCI) muss AUS sein.
    4. Dienst-Pfad pruefen: Eingabeaufforderung (Admin):
       sc qc WinRing0_1_2_0   (zeigt den konfigurierten .sys-Pfad)
    5. Button "Repair Driver Service" unten links ausfuehren.
  Anti-Cheat UND Hardware-Tweaks schliessen sich systembedingt aus -
  das ist keine Einschraenkung des Tools, sondern Absicht des AC.

S.U.C.K.-PROTOKOLL (NETZWERK-SEITE):
  Ersetzt Nic.ps1. Drei Presets: Soft (Offloads bleiben an - fuer
  Leitungen, die sie brauchen), Balanced (empfohlen) und Competitive.
  Vor jeder Anwendung wird automatisch ein Snapshot aller beruehrten
  Werte erstellt, danach laesst sich der Zustand pruefen ("Zustand
  pruefen") und mit "Snapshot wiederherstellen" exakt zuruecksetzen.
  Snapshots liegen im Ordner "suck\snapshots".

REGSHIELD (VERIFIER-SEITE):
  Vor jedem Klick auf "Apply 100% Verified Tweaks to Registry"
  speichert RegShield automatisch den exakten Live-Zustand aller
  betroffenen Registry-Werte im Ordner "Snapshots". Ueber den Button
  "RegShield Snapshots" lassen sich diese Snapshots einsehen und per
  Klick vollstaendig zurueckspielen - auch Werte, die vor dem Import
  nicht existierten, werden wieder entfernt. Ein schlechter .reg-
  Import ist damit immer ungeschehen machbar.

DER WIN TWEAK VERIFIER - ZWEI STUFEN:

Stufe 1 (immer verfuegbar, ohne Extra-Setup):
  Der Verifier analysiert die Windows-Treiber statisch mit pefile und
  capstone: Er sucht den Registry-Wertnamen im Treiber-Code, findet die
  Code-Referenzen und disassembliert die Umgebung. Ergebnis "CODE
  REFERENCE" bedeutet: Echter Treiber-Code referenziert diesen Wert in
  der Naehe von Registry-Lese-Logik. Zusaetzlich beweist die
  Registry-Ruecklese-Pruefung, dass die Werte physisch gesetzt wurden.

Stufe 2 (Ghidra, die tiefe Analyse - optional):
  Fuer den staerksten Beweis ("GHIDRA-CONFIRMED DATAFLOW": der Wert-
  Zeiger fliesst nachweislich in eine Registry-Query-API) benoetigt das
  Tool Ghidra. So wird es aktiviert:
    1. Ghidra von https://ghidra-sre.org/ herunterladen (Java 21 noetig,
       installiert Click_to_Start.bat automatisch).
    2. Ghidra nach "WinTweakVerifier\ghidra\" entpacken, sodass
       "WinTweakVerifier\ghidra\support\analyzeHeadless.bat" existiert
       - ODER die Umgebungsvariable GHIDRA_INSTALL_DIR setzen.
  Danach liefern die Ghidra-Buttons im Verifier die gruenen
  Datenfluss-Beweise. Ohne Ghidra bleibt der Verifier bei Stufe 1 und
  zeigt das ehrlich an - es wird nie ein Status vorgetaeuscht.

--- ENGLISH -----------------------------------------------------------------

A) UPDATING AN EXISTING INSTALLATION:

    1. Close the tool COMPLETELY (including the background task).
    2. Copy all files from this zip into the EXISTING program folder and
       choose "Replace/Overwrite" when asked. Your personal files
       (IMOD_Profile.bat, IMOD_Launcher.vbs, Ghidra folder, logs) are
       NOT part of the zip and stay untouched - the scheduled startup
       task remains valid.
    3. If Windows refuses to overwrite "chiptool\WinRing0.sys" /
       "WinRing0x64.sys" (file in use): reboot and copy those two files
       again AFTER booting, BEFORE starting the tool. If the driver is
       identical, skipping those two files is also safe.
    4. IMPORTANT - once after updating:
       a) Start the tool as admin.
       b) Run "Scan Hardware Radar".
       c) Click "Save Startup Profile", then REBOOT.
       Reason: older versions could save startup profiles WITHOUT the
       PCIe addresses (BDFs) - such profiles silently did nothing on
       every boot. Re-scanning + re-saving writes a complete, working
       profile.
    5. Note: copying resets the language to English (neutral
       settings.json in the zip). Switch it once at the top right - the
       setting then persists.

B) FRESH INSTALLATION:

    1. Extract this package into a NEW folder (do not copy over an old
       installation).
    2. RIGHT-CLICK "Click_to_Start.bat" -> "Run as administrator".
       The setup automatically installs Python 3.11 and all required
       packages (PyQt6, psutil, pefile, capstone) if needed.
    3. Inside the program:
       a) Run "Scan Hardware Radar" (reads your hardware).
       b) Apply the tweaks you want.
       c) Click "Save Startup Profile" - the profile MUST be saved from
          a fresh scan (stores the PCIe bus addresses/BDFs of your
          hardware). After hardware changes, simply re-scan and re-save.
       d) Reboot - the profile is then applied automatically on every
          login (task: IMOD_Startup_Task).

NOTES:
- Administrator rights are required for all hardware tweaks (MSR, PCIe
  config space, MMIO). Without admin, only the registry parts run.
- The "BSoD Guard" protects critical root ports (MPS re-framing is
  intentionally skipped) - this is a safety feature, not a bug.
- The language can be switched live at the top right (6 languages).
- Applied a driver update? -> Use the "Post Driver-Update Checklist" on
  the GPU page. The drift monitor on the Bento dashboard shows whether
  tweaks are still active ("Re-Check Now").

TROUBLESHOOTING:
- Tool does not start: check "crash_log.txt" in the program folder.
- Hardware tweaks show "Unknown" in the radar: run "Scan Hardware Radar"
  once with admin rights.
- WinRing0 service problems: use the "Repair Driver Service" button at
  the bottom left.

ANTI-CHEAT CONFLICT (IMPORTANT FOR GAMERS):
  Anti-cheat systems such as FACEIT AC or Vanguard deliberately block
  the kernel drivers WinRing0.sys and RwDrv.sys. When that happens the
  hardware tweaks (PCIe, MSR, USB) cannot be applied - they stay on
  stock. Registry and network tweaks keep working.
  How to detect it:
    - A RED warning banner appears in the program at start (shown when
      the last boot log proves both kernel engines were blocked), OR
    - startup_log.txt contains "WinRing0 Start fehlgeschlagen"
      (OLS_DLL_DRIVER_NOT_FOUND/BLOCKED) followed only by errors such
      as "rw.exe command timed out" / "output contained no hex".
  Checklist:
    1. Fully close or uninstall the anti-cheat client (e.g. FACEIT),
       then REBOOT.
    2. Start the tool MANUALLY as administrator and check
       startup_log.txt again.
    3. Windows Security -> Device Security -> Core Isolation:
       "Memory Integrity" (HVCI) must be OFF.
    4. Check the service path in an admin command prompt:
       sc qc WinRing0_1_2_0   (shows the configured .sys path)
    5. Run the "Repair Driver Service" button at the bottom left.
  Anti-cheat and hardware tweaks are mutually exclusive by design -
  that is the anti-cheat's intent, not a limitation of this tool.

S.U.C.K. PROTOCOL (NETWORK PAGE):
  Replaces Nic.ps1. Three presets: Soft (offloads stay on - for lines
  that need them), Balanced (recommended) and Competitive. Before
  every apply a snapshot of all touched values is created
  automatically; the state can then be checked ("Check State") and
  reset exactly via "Restore Snapshot". Snapshots live in the
  "suck\snapshots" folder.

REGSHIELD (VERIFIER PAGE):
  Before every click on "Apply 100% Verified Tweaks to Registry",
  RegShield automatically saves the exact live state of all affected
  registry values into the "Snapshots" folder. Via the "RegShield
  Snapshots" button these snapshots can be listed and restored with
  one click - including values that did not exist before the import;
  they get removed again. A bad .reg import can always be undone.

WIN TWEAK VERIFIER - TWO TIERS:

Tier 1 (always available, no extra setup):
  The verifier statically analyzes the Windows drivers with pefile and
  capstone: it searches the driver code for the registry value name,
  finds the code cross-references and disassembles their surroundings.
  A "CODE REFERENCE" result means: real driver code references this
  value near registry-reading logic. Additionally, the registry
  read-back check proves the values were physically written.

Tier 2 (Ghidra, the deep analysis - optional):
  For the strongest proof ("GHIDRA-CONFIRMED DATAFLOW": the value
  pointer provably flows into a registry query API), the tool needs
  Ghidra. How to enable it:
    1. Download Ghidra from https://ghidra-sre.org/ (Java 21 required;
       Click_to_Start.bat installs it automatically).
    2. Extract Ghidra to "WinTweakVerifier\ghidra\" so that
       "WinTweakVerifier\ghidra\support\analyzeHeadless.bat" exists
       - OR set the GHIDRA_INSTALL_DIR environment variable.
  Afterwards the Ghidra buttons in the Verifier produce the green
  dataflow proofs. Without Ghidra the verifier stays at Tier 1 and says
  so honestly - it never fakes a status.

--- DISCLAIMER / HAFTUNGSAUSSCHLUSS -----------------------------------------

Dieses Tool veraendert Systemeinstellungen (Registry, MSR, PCIe). Nutzung
auf eigene Verantwortung. Erstelle vor der ersten Verwendung einen
Wiederherstellungspunkt. / This tool modifies system settings (registry,
MSR, PCIe). Use at your own risk. Create a restore point before first use.

============================================================================
 (C) 2026 Jackpot's Hardware Register Engine
============================================================================
