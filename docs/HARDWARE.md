# Hardware

| Device | ID | Bus/location | Tag and evidence |
|---|---|---|---|
| CPU | Intel Core i5-10210U | socket | VERIFIED — `evidence/sysprof-all.txt` |
| UHD 620 | `8086:9b41` | PCI `00:02.0` | VERIFIED — `evidence/lspci-nn.txt` |
| Thermal subsystem | `8086:1903` | PCI `00:04.0` | VERIFIED — `evidence/lspci-nn.txt` |
| xHCI USB | `8086:02ed` | PCI `00:14.0` | VERIFIED — `evidence/lspci-nn.txt` |
| AX201 Wi-Fi | `8086:02f0` | PCI `00:14.3` | VERIFIED — `evidence/lspci-nn.txt` |
| I2C controllers | `8086:02e8`, `8086:02e9`, `8086:02c5` | PCI `00:15.0`, `00:15.1`, `00:19.0` | VERIFIED — `evidence/lspci-nn.txt` |
| cAVS audio | `8086:02c8` | PCI `00:1f.3` | VERIFIED — `evidence/lspci-nn.txt` |
| SMBus | `8086:02a3` | PCI `00:1f.4` | VERIFIED — `evidence/lspci-nn.txt` |
| NVMe SSD | Kingston SNV2S250G, `2646:5017` | PCI `01:00.0` | VERIFIED — `evidence/lspci-nn.txt` |
| AX201 Bluetooth | `8087:0026` | USB | VERIFIED — `evidence/lsusb.txt` |
| Webcam | `5986:2115` | USB | VERIFIED — `evidence/lsusb.txt`, `evidence/input-devices.txt` |
| Fingerprint | `06cb:00be` | USB | VERIFIED — `evidence/lsusb.txt` |
| Touchpad | `06CB:CD3E` | I2C | VERIFIED — `AUDIT.md`, log-cited |
| Wacom touchscreen | `056A:51EF` | I2C1, `WCOM51EF` | VERIFIED — `evidence/macos-panic.txt`, `docs/TOUCHSCREEN-PANIC.md` |
