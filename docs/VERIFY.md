# Verify

Run these on the machine after boot. The expected outputs are the bits that matter, not a full transcript.

| Check | Command | Expected |
|---|---|---|
| Graphics acceleration | `system_profiler SPDisplaysDataType` | Metal Support: Metal 3, display Online |
| Audio output | `system_profiler SPAudioDataType` | Built-in Output, 48000 Hz |
| Boot chime config | `plutil -p EFI/OC/config.plist \| grep -A2 Audio` | `PlayChime=Enabled`, AudioDxe argument present |
| Wi-Fi controller | `system_profiler SPAirPortDataType` | Interface `en0`, linked |
| Bluetooth | `system_profiler SPBluetoothDataType` | Controller State: On |
| Webcam | `system_profiler SPUSBDataType` | Integrated Camera, vendor `5986`, product `2115` |
| Sleep and wake | `pmset -g log \| grep -E 'Sleep\|Wake from'` | Normal Sleep followed by Wake from Normal Sleep |
| Keyboard backlight | Fn+Space | Brightness changes in YogaSMC |
| Touchpad | move pointer, tap, double-click | Pointer moves; tap works; double-click mostly works |
| CFG-Lock | `sudo rdmsr -p0 0xE2` | `1e008008` |

`EFI/OC/config.plist` in the repository is the published copy. It has a blank SMBIOS identity. Do not boot it until you fill in your own values.
