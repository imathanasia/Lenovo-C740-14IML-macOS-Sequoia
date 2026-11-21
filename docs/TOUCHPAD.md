# Touchpad

The reliable touchpad setup uses VoodooRMI 1.4.3 with RMII2C, VoodooI2C 2.9.1, and VoodooGPIO. VoodooI2CHID is not installed. With that combination, pointer movement works, tap works, and double-click mostly works.

The ForceTouch settings are in the kext's own Info.plist:

```text
VoodooRMI.kext/Contents/Info.plist
IOKitPersonalities -> RMIDevice -> Configuration
ForceTouchType = 0
ForceTouchMinPressure = 0
```

The wrong path seen in older notes is `RMIDevice.Mode`. It does not exist in this kext. Copying that path changes nothing.

The published kext has the 0/0 values. Older notes in this project used 1/40 and are stale. macOS tap-to-click is also enabled with `com.apple.AppleMultitouchTrackpad Clicking = 1`.

The Synaptics touchpad is `06CB:CD3E`. The USB dump also shows `06CB:00BE`; that is the fingerprint device, not the touchpad.
