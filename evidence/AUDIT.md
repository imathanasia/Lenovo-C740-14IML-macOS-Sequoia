# AUDIT.md — Phase A claim audit

Tag legend: `VERIFIED` = captured in `evidence/`; `SOURCE` = URL opened in this session; `UNVERIFIED` = no comparable capture. Verdict legend: `proved`, `claimed-only`, `contradicted`. Every claim below has a final tag and a resolution; no untagged claim may ship.

| Claim | Tag | Evidence | Verdict | Resolution |
|---|---|---|---|---|
| Model is Lenovo Yoga C740-14IML, product 81TC | VERIFIED | `evidence/dmidecode.txt` | proved | Keep |
| Board name is LNVNB161216 | VERIFIED | `evidence/dmidecode.txt` | proved | Keep |
| BIOS is BNCN41WW | VERIFIED | `evidence/dmidecode.txt` | proved | Keep |
| CPU is Intel Core i5-10210U | VERIFIED | `evidence/sysprof-all.txt` | proved | Keep as 4-core 2.11 GHz capture; exact model comes from fixed brief |
| GPU is Intel UHD 620 `8086:9B41` | VERIFIED | `evidence/lspci-nn.txt` | proved | Keep; do not cite sysprof for PCI id |
| RAM is 8 GB DDR4-2667 | VERIFIED | `evidence/sysprof-all.txt`, `evidence/macos-panic.txt` | proved | Keep; omit “soldered” unless fixed brief is cited |
| Storage is Kingston SNV2S250G | VERIFIED | `evidence/sysprof-all.txt` | proved | Keep; serial redacted |
| Audio codec is ALC285 behind cAVS `8086:02c8` at `00:1f.3` | VERIFIED | `evidence/lspci-nn.txt` | proved | Keep cAVS id from capture; ALC285 from fixed brief |
| Wi-Fi is AX201 `8086:02f0` | VERIFIED | `evidence/lspci-nn.txt` | proved | Keep; add `SPAirPortDataType` capture if available |
| Bluetooth is `8087:0026` | VERIFIED | `evidence/lsusb.txt` | proved | Keep |
| Webcam is `5986:2115` | VERIFIED | `evidence/lsusb.txt`, `evidence/input-devices.txt` | proved | Keep |
| Touchpad is Synaptics `06CB:CD3E` | VERIFIED | `bundle/logs/TOUCHPAD.md` | proved | Keep; `06CB:00BE` in USB dumps is fingerprint device |
| macOS is Sequoia 15.8.3 (24H241) | VERIFIED | `evidence/sysprof-all.txt` | proved | Keep |
| CFG-Lock is set, `rdmsr 0xE2 = 1e008008` | VERIFIED | `evidence/msr-e2.txt` | proved | Keep |
| Boot args are `keepsyms=1 debug=0x100 alcid=61 igfxonln=1` | VERIFIED | `evidence/config-redacted.json`, `evidence/config-keys.txt` | proved | Keep |
| As-booted OpenCore is 1.0.7; publish target is 1.0.8 | VERIFIED | `MANIFEST.md`, release page | proved | Keep |
| Debian occupies the first ~50 GB; APFS is next | VERIFIED | `evidence/lsblk.txt` | proved | Keep |
| No Windows install shares the disk | VERIFIED | `evidence/windows.txt`, `evidence/lsblk.txt` | proved | Keep |
| Graphics acceleration works | VERIFIED | `evidence/sysprof-all.txt` (Metal 3, display Online) | proved | Keep; real screenshot pending Phase E |
| Audio output works with layout 61 | VERIFIED | `evidence/sysprof-all.txt`, `evidence/config-redacted.json` | proved | Keep |
| Built-in microphone present and default input | VERIFIED | `evidence/sysprof-all.txt` | proved | Keep; do not say untested |
| Boot chime works with AudioDxe forced to cAVS | VERIFIED | `evidence/config-redacted.json`, `evidence/config-keys.txt` | proved | Keep; add exact argument and 48 kHz file |
| Wi-Fi works on `en0` | VERIFIED | `evidence/lspci-nn.txt`, `evidence/config-redacted.json` | proved | Keep; do not claim reconnect verified unless captured |
| Bluetooth controller active; one phone paired | VERIFIED | `evidence/sysprof-all.txt`, `evidence/lsusb.txt` | proved | Keep “controller active, paired device listed”; current capture says Not Connected |
| Webcam UVC works | VERIFIED | `evidence/lsusb.txt`, `evidence/input-devices.txt` | proved | Keep |
| Clean sleep/wake verified | VERIFIED | `evidence/sleep-wake.log` | proved | Keep 6-second captured wake; 64-second operator report is downgraded to UNVERIFIED |
| Keyboard backlight via YogaSMC on VPC2004 | VERIFIED | `bundle/logs/UPDATE_YOGASMC.md` | claimed-only | Downgrade to operator-confirmed with log citation; empty `ioreg-i2c.txt` is not proof |
| Touchpad movement and tap work; double-click mostly works | VERIFIED | `bundle/logs/TOUCHPAD_SETTLED.md` | proved | Keep exact wording; do not claim two-finger tap |
| Touchscreen panics in `VoodooI2CMultitouchHIDEventDriver::parseElements +0x3eb` | VERIFIED | `evidence/macos-panic.txt` | proved | Keep exact symbol and offset |
| Panic call chain includes `VoodooI2CTouchscreenHIDEventDriver::handleStart` and `IOHIDEventService::start` | VERIFIED | `evidence/macos-panic.txt` | proved | Keep |
| Wacom exposes two collections: Pen and Finger | VERIFIED | `evidence/input-devices.txt`, `bundle/logs/TOUCHSCREEN.md` | proved | Keep; do not say three |
| Touchscreen HID personality at score 400 sits above Multitouch at 200 | VERIFIED | `bundle/logs/THIRD_PARTY_REFINED.md` | proved | Keep as log-cited finding |
| VoodooI2CHID 2.6.5 experiment was not run | VERIFIED | `bundle/logs/THIRD_PARTY_REFINED.md` | proved | Keep status UNRUN |
| SSDT-TPL1 was tested and did not prevent panic | VERIFIED | `bundle/logs/TOUCHSCREEN_FAILED.md` | proved | Keep |
| Exact SSDT-I2C1 rename was not captured | UNVERIFIED | `MISSING-INPUTS.md` | claimed-only | Keep in missing-inputs list only |
| `AppleXcpmCfgLock = true` and `AppleCpuPmCfgLock = true` | VERIFIED | `evidence/config-redacted.json`, `evidence/msr-e2.txt` | proved | Keep with CFG-Lock reason |
| `RebuildAppleMemoryMap`, `SyncRuntimePermissions`, `DisableIoMapper` true | VERIFIED | `evidence/config-redacted.json` | proved | Keep |
| `SecureBootModel = Disabled`, `Vault = Optional`, `ScanPolicy = 0`, `ApECID = 0` | VERIFIED | `evidence/config-redacted.json`, `evidence/config-keys.txt` | proved | Keep |
| `ResizeAppleGpuBars = -1`, `MinDate = -1`, `MinVersion = -1` | VERIFIED | `evidence/config-redacted.json`, `evidence/config-keys.txt` | proved | Keep |
| `Misc > Debug Target = 67`, `DisplayLevel = 2147483714` in published config | VERIFIED | `evidence/config-redacted.json`, `evidence/config-keys.txt` | proved | Correct old 0/0 draft values before shipping |
| ForceTouch keys are under `IOKitPersonalities.RMIDevice.Configuration` | VERIFIED | `bundle/draft/EFI/OC/Kexts/VoodooRMI.kext/Contents/Info.plist` | proved | Keep; document wrong `RMIDevice.Mode` path |
| `ForceTouchType = 0`, `ForceTouchMinPressure = 0` in published kext | VERIFIED | shipped kext Info.plist | proved | Keep; old 1/40 note is stale |
| Phases 7 and 8 are complete | VERIFIED | `bundle/logs/FINAL_EFI_STATE.md`, handover | proved | Keep; fix old ERRATA line that said phase 8 pending |
| OpenCore 1.0.8 release is commit `6fe4d15`, 27 Sep 2026 | SOURCE | https://github.com/acidanthera/OpenCorePkg/releases/tag/1.0.8 | proved | Keep |
| Humanizer v4.0.0 is MIT and from blader/humanizer | SOURCE | https://github.com/blader/humanizer | proved | Keep; include notice row |
| BsxM1 theme credit is Blackosx | SOURCE | https://github.com/blackosx/BsxM1 | proved | Keep |
| Sequoia recovery command uses board `Mac-7BA5B2D9E42DDD94` | SOURCE | https://raw.githubusercontent.com/acidanthera/OpenCorePkg/master/Utilities/macrecovery/recovery_urls.txt | proved | Keep |
| Board `Mac-53F27B3A7AFB7B5F` returned HTTP 403 | UNVERIFIED | no capture retained | claimed-only | Drop; keep only the working board-id command |
| AirDrop, Handoff, Sidecar, iMessage, FaceTime were not attempted | UNVERIFIED | no capture | claimed-only | Keep in not-attempted list only |
| Apple Watch unlock was not attempted | UNVERIFIED | no capture | claimed-only | Keep in not-attempted list only |
| USB port mapping was not generated | VERIFIED | `evidence/config-redacted.json` (no USBMap kext) | proved | Keep in not-attempted list |
| CPUFriend was not applied | VERIFIED | `evidence/config-redacted.json` (no CPUFriend kext) | proved | Keep in not-attempted list |
| Custom OpenCanopy wallpaper was not made | VERIFIED | shipped theme assets are upstream BsxM1 | proved | Keep in not-attempted list |
| iServices were never configured | UNVERIFIED | no comparable capture | claimed-only | Keep as UNVERIFIED |
| SMBIOS identity was inherited from ThrRip reference and replaced before publication | VERIFIED | `bundle/logs/FINAL_EFI_STATE.md`, published config | proved | Keep; tell readers to generate their own |
| AirDrop/Handoff unavailable with AX201 | UNVERIFIED | no retained source | contradicted | Drop; replaced by not-attempted list |
| Fingerprint reader accepted dead | UNVERIFIED | no retained source | contradicted | Drop |
| Machine has no Thunderbolt | UNVERIFIED | no retained source | contradicted | Drop |
| macOS 27+ impossible on this CPU | UNVERIFIED | no retained source | contradicted | Drop |
| Built-in microphone not tested this session | UNVERIFIED | no retained source | contradicted | Drop |
| Revert script syntax verified | UNVERIFIED | no shipped evidence | contradicted | Drop |
| “Everything fully working” | UNVERIFIED | no comparable capture | contradicted | Never ship; README must state touchscreen does not work |
| Bluetooth reconnect after reboot verified | UNVERIFIED | no comparable capture | claimed-only | Downgrade to UNVERIFIED or drop |
| 64-second sleep verified in retained capture | UNVERIFIED | `bundle/logs/VERIFIED_STATE.md` only | claimed-only | Downgrade to operator report; retain 6-second log as VERIFIED |
| Two-finger tap verified | UNVERIFIED | no retained capture | claimed-only | Drop |
| Boot chime “diagnosed, unrun” | UNVERIFIED | old note | contradicted | Corrected in ERRATA |
| Three Wacom collections | UNVERIFIED | old note | contradicted | Corrected in ERRATA |
| VoodooI2CHID 2.6.5 failed | UNVERIFIED | old note | contradicted | Corrected in ERRATA |
| ForceTouch keys under `RMIDevice.Mode` | UNVERIFIED | old note | contradicted | Corrected in ERRATA |
| Debug values 0/0 in draft config | UNVERIFIED | old draft | contradicted | Corrected to 67/2147483714 in Phase B |
| Redaction already proved for all evidence files | UNVERIFIED | old gate | contradicted | Re-run full grep/OCR in Phase F and record actual result |
| Every README working line carries a tag and evidence file | UNVERIFIED | old gate | contradicted | Rebuilt README in Phase C with one tag per row |
| Sanitized EFI booted with blank identity | UNVERIFIED | no boot test retained | claimed-only | Keep PENDING until a boot test is captured; release notes must say pending |
