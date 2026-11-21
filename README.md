# C740-14IML-OpenCore

OpenCore EFI and evidence for a Lenovo Yoga C740-14IML running macOS Sequoia.

## Specs

| Item | Value | Tag and evidence |
|---|---|---|
| Model | Yoga C740-14IML, product 81TC | VERIFIED — `evidence/dmidecode.txt` |
| Board | LNVNB161216 | VERIFIED — `evidence/dmidecode.txt` |
| BIOS | BNCN41WW | VERIFIED — `evidence/dmidecode.txt` |
| CPU | Intel Core i5-10210U | VERIFIED — `evidence/sysprof-all.txt` |
| GPU | Intel UHD 620, `8086:9b41` | VERIFIED — `evidence/lspci-nn.txt` |
| RAM | 8 GB DDR4-2667 | VERIFIED — `evidence/sysprof-all.txt` |
| Storage | Kingston SNV2S250G | VERIFIED — `evidence/sysprof-all.txt` |
| Audio | ALC285 behind cAVS `8086:02c8` at `00:1f.3` | VERIFIED — `evidence/lspci-nn.txt` |
| Wi-Fi | Intel AX201, `8086:02f0` | VERIFIED — `evidence/lspci-nn.txt` |
| Bluetooth | Intel AX201 USB, `8087:0026` | VERIFIED — `evidence/lsusb.txt` |
| Webcam | `5986:2115` | VERIFIED — `evidence/lsusb.txt` |
| Touchpad | Synaptics `06CB:CD3E` | VERIFIED — `AUDIT.md`, log-cited |
| macOS | Sequoia 15.8.3 (24H241) | VERIFIED — `evidence/sysprof-all.txt` |
| CFG-Lock | Set, `rdmsr 0xE2 = 1e008008` | VERIFIED — `evidence/msr-e2.txt` |
| OpenCore | 1.0.8 published, 1.0.7 as booted | VERIFIED — `VALIDATION.md` |

## Working on this unit

Every row has one tag and an evidence link. Everything in this table works on this machine. The touchscreen does not, as described below.

| Feature | Tag and evidence |
|---|---|
| Boot to desktop with acceleration | VERIFIED — `evidence/sysprof-all.txt` |
| Speakers and headphone jack, layout 61 | VERIFIED — `evidence/sysprof-all.txt`, `evidence/config-redacted.json` |
| Built-in microphone present as default input | VERIFIED — `evidence/sysprof-all.txt` |
| Boot chime | VERIFIED — `evidence/config-redacted.json`, [Boot chime on cAVS](docs/BOOT-CHIME-cAVS.md) |
| Wi-Fi controller present and enabled | VERIFIED — `evidence/lspci-nn.txt`, `evidence/config-redacted.json` |
| Bluetooth controller active, phone paired | VERIFIED — `evidence/sysprof-all.txt`, `evidence/lsusb.txt` |
| Webcam | VERIFIED — `evidence/lsusb.txt` |
| Sleep and wake, 6-second captured interval | VERIFIED — `evidence/sleep-wake.log` |
| Keyboard backlight | VERIFIED, operator-confirmed — `AUDIT.md` |
| Touchpad movement, tap, mostly working double-click | VERIFIED — `AUDIT.md` |

## Not working

The Wacom touchscreen panics VoodooI2CHID in `VoodooI2CMultitouchHIDEventDriver::parseElements +0x3eb`. See [Touchscreen panic](docs/TOUCHSCREEN-PANIC.md). The panic is in `evidence/macos-panic.txt`.

## Not attempted

AirDrop, Handoff, Sidecar, iMessage, FaceTime, Apple Watch unlock, USB port mapping, CPUFriend, and a custom OpenCanopy wallpaper. These are UNVERIFIED.

iServices were never configured. The SMBIOS model is `MacBookPro16,2`, inherited from the reference build. Generate your own identity before using this EFI on your machine. `ROM` must be your own `en0` MAC.

## Quirks

| Quirk | Reason |
|---|---|
| `AppleXcpmCfgLock = true`, `AppleCpuPmCfgLock = true` | VERIFIED: CFG-Lock is set, `evidence/msr-e2.txt` |
| `ResizeAppleGpuBars = -1` | VERIFIED: config, `evidence/config-keys.txt` |
| `SecureBootModel = Disabled`, `Vault = Optional` | VERIFIED: config, `evidence/config-keys.txt` |
| `ScanPolicy = 0`, `ApECID = 0` | VERIFIED: config, `evidence/config-keys.txt` |
| Boot args `keepsyms=1 debug=0x100 alcid=61 igfxonln=1` | VERIFIED: `evidence/config-redacted.json` |

## First boot on your own machine

1. Generate a unique SMBIOS identity with GenSMBIOS.
2. Set `SystemSerialNumber`, `MLB`, `SystemUUID`, and `ROM` in `EFI/OC/config.plist`.
3. Set `ROM` to your own `en0` MAC.
4. Read [Install](docs/INSTALL.md) and [Verify](docs/VERIFY.md).

See [Hardware](docs/HARDWARE.md), [Touchpad](docs/TOUCHPAD.md), [Missing inputs](docs/MISSING-INPUTS.md), [Errata](ERRATA.md), [Notice](NOTICE.md), and [Security](SECURITY.md).
