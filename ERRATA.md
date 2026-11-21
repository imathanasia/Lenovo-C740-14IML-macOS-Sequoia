# Errata

Earlier notes in this project said the following. Each line is superseded by the correction here and in `AUDIT.md`.

| Old claim | Correction |
|---|---|
| Phases 7 and 8 were incomplete | Phases 7 and 8 are complete |
| ForceTouch keys were under `RMIDevice.Mode` | They are under `IOKitPersonalities.RMIDevice.Configuration`; `Mode` does not exist |
| Boot chime was diagnosed but unrun | VERIFIED working with the AudioDxe force-device argument and 48 kHz chime |
| Wacom had three collections | It has two: Pen and Finger |
| VoodooI2CHID 2.6.5 failed | It was never run; status UNRUN |
| SSDT-I2C1 rename was recorded | Not captured; listed in `docs/MISSING-INPUTS.md` |
| AppleXcpmCfgLock was not documented | Confirmed true; CFG-Lock is set |
| Debug values were 0/0 | Published config uses 67/2147483714 |
| Touchpad had verified two-finger tap | Not retained; only movement, tap, and mostly-working double-click are claimed |
| Sleep was verified at 64 seconds | Retained log shows a 6-second interval; 64 seconds remains an operator report |
| AirDrop/Handoff were unavailable with AX201 | Not attempted in this pass; moved to the not-attempted list |
| Fingerprint reader was dead | Dropped; no retained source |
| The machine had no Thunderbolt | Dropped; no retained source |
| macOS 27+ was impossible on this CPU | Dropped; no retained source |
| Built-in microphone was untested | Present as default input in `evidence/sysprof-all.txt` |
