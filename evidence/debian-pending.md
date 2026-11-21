# debian-pending.md

Debian-side commands were not re-run into this bundle because HOST is booted into macOS.
They were captured earlier this session and are represented by debian-inventory-redacted.md.

Commands:
- dmidecode -t system -t baseboard -t bios -t memory
- lsblk -f
- efibootmgr -v
- setpci -s 00:1f.3 0x0B.b ; setpci -s 00:1f.3 0x0A.b
- ocvalidate EFI/OC/config.plist
- lsblk, efibootmgr, os-prober, test -d /boot/efi/EFI/Microsoft
- md5sum/sha256sum of committed EFI files and recursive EFI listing
- tar of the live ESP HOSTd-only

Status: PENDING until HOST is booted into Debian.
