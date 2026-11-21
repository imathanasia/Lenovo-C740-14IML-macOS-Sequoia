# Boot chime on cAVS

The boot chime works on this machine, but AudioDxe needs an explicit device. The reason is the PCI class reported by the audio controller.

The cAVS controller at `00:1f.3` is `8086:02c8`. `setpci -s 00:1f.3 0x0B.b` returns `04` and `setpci -s 00:1f.3 0x0A.b` returns `01`, so the device belongs to class `04:01`. AudioDxe's `HdaControllerDriverBindingSupported` gate expects class `04:03`. Without a force option, the driver skips this controller.

The working AudioDxe argument is:

```text
--force-device=PciRoot(0x0)/Pci(0x1f,0x3) --force-codec=0
```

It is present in `EFI/OC/Drivers` and in `evidence/config-redacted.json`. The AudioDxe change is associated with commit `79f0829` in OpenCorePkg (SOURCE: the OpenCorePkg history).

The chime file is `EFI/OC/Resources/Audio/OCEFIAudio_VoiceOver_Boot.mp3`, resampled to 48 kHz. The 44.1 kHz original is kept beside it as `.44k.bak`. `UEFI > Audio` has `PlayChime=Enabled`, `AudioCodec=0`, `AudioDevice=PciRoot(0x0)/Pci(0x1f,0x3)`, `AudioOutMask=-1`, and `DisconnectHda=true`. NVRAM has `SystemAudioVolume=0x30` and `StartupMute=0x00`.

Audio output into macOS still works after the change.
