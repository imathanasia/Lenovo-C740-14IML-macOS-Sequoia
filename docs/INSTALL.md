# Install

This is the path used on this machine. It assumes a blank disk with Debian already installed first.

## Recovery

Download Sequoia recovery with OpenCorePkg's `macrecovery.py`. The board-id below is the one that worked here.

```text
python3 ./macrecovery.py -b Mac-7BA5B2D9E42DDD94 -m 00000000000000000 download
```

Confirm that `BaseSystem.dmg` and `BaseSystem.chunklist` are present. `BaseSystem.dmg` should be several hundred MB.

## USB

1. Create one GPT disk.
2. Make a FAT32 partition labelled `OPENCORE`, type `0700`.
3. Copy this repository's `EFI/` directory to the partition root.
4. Create `com.apple.recovery.boot/` at the partition root.
5. Put `BaseSystem.dmg` and `BaseSystem.chunklist` in that directory.

## BIOS

Turn off Secure Boot and SGX. Use UEFI boot mode. Keep the firmware set to `BNCN41WW` or a version you have tested.

## Partitions used here

| Partition | Use |
|---|---|
| p1 | EFI System Partition |
| p2 | Debian root, about 50 GB |
| p3 | macOS APFS |
| p4 | Linux swap |

The macOS installer renamed the APFS partition from p4 to p3. `evidence/lsblk.txt` shows the final layout.

## Install

Boot the USB through OpenCore. Choose the macOS recovery entry. Use Disk Utility to erase the APFS target partition, then install Sequoia. Boot through OpenCore for every installer reboot.

After first boot, run [Verify](VERIFY.md). Before first boot on a different machine, replace the SMBIOS identity as described in [the README](../README.md).
