# Security

The published files remove the machine serial, MLB, system UUID, ROM, Wi-Fi and Bluetooth MACs, hostnames, Apple identity values, LAN addresses, personal paths, SSH key filenames, and disk or filesystem identifiers. Replacement rules use `~` for home directories, a generic host name for the machine, and `LAN` for LAN addresses.

Evidence files keep their raw command output except for those replacements. Some identifiers appear in the audit process outside the repository; those files are not shipped.

Screenshots use opaque boxes over anything private. Metadata is stripped from shipped images. Every shipped image is OCR-checked against the same identifier list used for the tree grep.

To report a leak, open a private issue or contact the maintainer before posting the value in public.
