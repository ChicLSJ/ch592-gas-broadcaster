# Firmware releases

`ch592_ota.bin` is the WCH BackupUpgrade application image consumed by the CH592 OTA Home Assistant integration. It is intended for devices that already have the OTA bootloader.

## OTA 1.4.5

- WCH BackupUpgrade Image A/B + IAP flow.
- BTHome gas value, battery data, and firmware version advertisement.
- Append-only gas records with read-back verification.
- See `manifest.json` for exact size, CRC32, and SHA-256.

Keep the device powered during OTA erase, write, verify, and reboot. Complete first-flash/recovery images are kept in a private local backup and are not published here.

For Home Assistant, click the update entity first. The integration downloads and verifies `ch592_ota.bin` into its local `.storage/ch592_ota/firmware/` cache, then waits for the device's OTA advertisement. After the upload and a fresh normal BTHome broadcast with the new version, OTA mode closes automatically.
