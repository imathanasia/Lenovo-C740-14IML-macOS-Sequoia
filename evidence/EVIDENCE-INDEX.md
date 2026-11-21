# EVIDENCE-INDEX.md

| File | Command | Proves |
|---|---|---|
| `dmidecode.txt` | `dmidecode -t 0 -t 1 -t bios` on target host | BIOS `BNCN41WW`, product `81TC`, family `Yoga C740-14IML`, board identity |
| `lsblk.txt` | `lsblk -f` on target host | Debian on p2, APFS on p3, swap on p4, EFI on p1, no Windows partition |
| `efibootmgr.txt` | `efibootmgr -v` on target host | OpenCore, Debian and firmware boot entries |
| `pci-subclass.txt` | `setpci -s 00:1f.3 0x0A.b` | PCI subclass `01` |
| `pci-class.txt` | `setpci -s 00:1f.3 0x0B.b` | PCI class `04` |
| `windows.txt` | `test -d /boot/efi/EFI/Microsoft && echo windows-present \|\| echo no-windows` | No Windows bootloader directory on internal ESP |
| `lspci-nn.txt` | `lspci -nn` on target host | PCI ids for UHD 620 `8086:9b41`, cAVS `8086:02c8`, AX201 `8086:02f0` |
| `lsusb.txt` | `lsusb` on target host | BT `8087:0026`, webcam `5986:2115`, Synaptics `06cb:00be` |
| `msr-e2.txt` | `rdmsr -p0 0xE2` | CFG-Lock bit set, value `1e008008` |
| `sysprof-all.txt` | `system_profiler SPHardwareDataType SPSoftwareDataType SPAudioDataType SPBluetoothDataType SPDisplaysDataType SPNVMeDataType` on target host | Hardware, OS, audio, BT controller, display and storage facts |
| `input-devices.txt` | `system_profiler SPUSBDataType` on target host | Webcam and BT USB identity |
| `macos-panic.txt` | copy of newest `/Library/Logs/DiagnosticReports/*.panic` | Touchscreen panic stack and offsets |
| `sleep-wake.log` | `pmset -g log \| tail -n 400` | Clean sleep/wake with 6-second captured interval |
| `pmset.txt` | `pmset -g custom` | Power settings |
| `config-redacted.json` | plist parse of the as-booted config with identity keys elided | Sanitized config values, boot args, quirks, AudioDxe argument |
| `config-keys.txt` | targeted extraction from published config | Upload-checklist values |
| `routes.txt` | `netstat -rn \| head -40`, redacted | Network routing with addresses redacted |
| `ioreg-i2c.txt` | `ioreg -r -c AppleIntelLpssI2CDevice -l` | Empty output; not used as proof of keyboard backlight or touchpad |
| `AUDIT.md` | Phase A claim audit | Claim verdicts and resolutions |
