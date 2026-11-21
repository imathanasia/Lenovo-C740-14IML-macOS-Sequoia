# Touchscreen panic

The Wacom touchscreen on this unit does not work. The panic is in `evidence/macos-panic.txt`.

## Panic stack

```text
VoodooI2CMultitouchHIDEventDriver::parseElements + 0x3eb
VoodooI2CTouchscreenHIDEventDriver::handleStart
IOHIDEventService::start
```

VoodooI2CHID 1.0 is the loaded version. `parseElements` is the faulting function, offset `+0x3eb`. Both the touchscreen driver and the generic HID event service appear in the call chain.

## ACPI shape

The device is `WCOM51EF` on `I2C1`. The Wacom digitizer exposes two application collections:

- `Wacom HID 51EF Pen`
- `Wacom HID 51EF Finger`

Older notes in this project said three collections. That was wrong.

The kext carries two matching personalities. `VoodooI2CHIDDevice Touchscreen HID Event Driver` has `IOProbeScore` 400. `VoodooI2CHIDDevice Multitouch HID Event Driver` has `IOProbeScore` 200. Removing only the Touchscreen personality still leaves the 200-score Multitouch personality in the path to `parseElements`, so it still panics.

## Tested

`SSDT-TPL1.aml` was tested and did not prevent the panic. VoodooI2CHID was removed again and the machine booted cleanly.

## Untested

VoodooI2CHID 2.6.5 — status UNRUN. A patched `parseElements` and the XOSI route are also UNVERIFIED. No claim is made that any of them fixes this digitizer.
