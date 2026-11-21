# Missing inputs

These were not captured and are not guessed.

1. Exact SSDT-I2C1 rename that shipped with the removed SSDT-TPL1.
2. A successful boot of the sanitized EFI with blank identity keys.
3. Human-provided screenshots that need physical camera work: boot picker and panic screen. See `docs/img/SHOTLIST-PENDING.md` if present.
4. A retained source for the HTTP 403 result from the old recovery board-id.
5. Proof that Wi-Fi reconnects after reboot; the controller is verified, that specific behaviour is not.
6. A retained capture for keyboard backlight beyond operator confirmation.
7. A successful fix for the touchscreen panic. VoodooI2CHID 2.6.5 is UNRUN; XOSI and a patched `parseElements` are UNVERIFIED.
