# CH592 BTHome gas meter

1.5.6 / HA0.6.21: when no Bluetooth proxy currently has a connectable path to the meter, HA now waits for the next advertisement instead of retrying every 0.2 s; one wake round may last 240 s instead of 180 s; temporary wake diagnostics are added to the status sensor and will be removed once the issue is understood. Firmware changes only its version; metering, optics, sampling, sleep, battery, normal 300 ms/minute advertising, complete image writes and CRC are unchanged. Matching builds, firmware fault tests and 88 HA tests pass; physical OTA pending. OTA images only; full recovery remains local.

1.5.5 / HA0.6.20: before an explicit update or settings connection, discard this meter’s old ESPHome host service table. This avoids wasting an advertising cycle on a normal/OTA mode cache mismatch; retain capability reads and checked cache recovery. The optimization is in HA; firmware changes only its version. Metering, optics, sampling, sleep, battery, normal 300 ms/minute advertising, complete image writes and CRC are unchanged. Matching builds, firmware fault tests and 84 HA regressions pass; physical 1.5.4→1.5.5 OTA passed; measured results and limits follow. Publish OTA images only; full recovery remains local.

Physical 1.5.4→1.5.5 OTA passed: the successful run took 122.8 s, including wake 72.745 s (4 attempts), connection 4.926 s, erase 1.125 s, upload 37.480 s, whole-image CRC 1.330 s, END 0.144 s and reboot confirmation 5.003 s. HA confirmed 1.5.5, 100%, OTA off, preserved 22.52 m³ and resumed normal advertisements. A preceding run timed out after 180.2 s during wake without erasing/programming; the retry succeeded. The shorter successful run does not establish overall reliability or a guaranteed speedup. Power was not measured.

Physical 1.5.3→1.5.4 OTA succeeded in 181.0 s: wake wait 129.163 s (7 attempts), connection 4.330 s, erase 1.209 s, upload 39.716 s, whole-image CRC 1.433 s, END 0.140 s and reboot confirmation 5.004 s. HA confirmed 1.5.4, 100%, OTA off and the preserved 22.51 m³ reading. Normal advertising resumed the following minute; stale connection messages and wake errors cleared on success. Connection retries remain the main delay. Daily power policy is unchanged; current and battery lifetime were not measured.

Physical 1.5.1→1.5.2 OTA succeeded in 63.7 s: wake wait 13.111 s, connection 3.560 s, erase 1.028 s, upload 39.350 s, whole-image CRC 1.499 s, END 0.128 s and reboot confirmation 5.007 s. One wake attempt, no connection retries; HA confirmed 1.5.2, 100%, normal mode and 22.51 m³, with distinct chip/counter icons. Entry during this upgrade still ran on 1.5.1; the new 1.5.2 idle timing needs observation on a future update. The shorter total cannot be attributed entirely to that fix.

**Language: [中文（默认）](README.md) | English**

Public release files for the CH592 Bluetooth gas-meter broadcaster.

- `firmware/` — WCH BackupUpgrade OTA application image, manifest, and OTA instructions.
- `enclosure/` — printable flush-mount enclosure STL/3MF files.

The companion Home Assistant integration, ch592_ota, reads `firmware/manifest.json` through GitHub raw file service. Its code is not published.

## Firmware selection

Use `firmware/ch592_ota.bin` for Home Assistant OTA. This repository only publishes the application image for devices that already have the OTA bootloader; complete first-flash/recovery images remain in a private local backup and are not published here.

The current manifest is version **1.5.6**:

- WCH BackupUpgrade Image A/B + IAP flow
- BTHome gas value, battery data, and firmware-version advertisement
- Append-only gas records with read-back verification
- Binary size: 159,516 bytes
- CRC32: `0xFF0B59E2`
- SHA-256: `0e65581f06839314d913b69a587fdda71786a5262b5491f81c6b173eaec5aa75`

## Installation and OTA

This repository only provides the application image for devices with the OTA bootloader. Use your own wired backup for first hardware initialization; no complete recovery image is published here. Daily upgrades use Home Assistant OTA.

With HA 0.6.9 and firmware 1.4.7, click Update and the integration downloads, verifies and wakes OTA automatically. Older firmware still needs B for the first installation. The B button remains a manual fallback: On firmware 1.4.7, hold B for about 5 seconds and release before 10 seconds to enter `GasMeter-SET` for nRF Connect. Continue holding B to about 10 seconds to enter `GasMeter OTA` for HA. After releasing B, 5 seconds without the corresponding action returns to normal measurement and BTHome advertising. OTA commands refresh this idle timer; a successful phone write is saved and exits settings. Settings advertising cannot trigger HA installation.

Older OTA firmware (1.4.3 and earlier) still uses B for 3 seconds. The original 2026-08-22 firmware cannot use this repository for a direct OTA update; install an OTA-enabled version from your private wired recovery backup first. See [English instructions](firmware/Instructions.en.md). 1.5.1 passed physical OTA and fast-CRC retesting (1.33 s verification). 1.5.2 has matching independent builds and host tests; its physical OTA passed.

## Publication scope

This repository publishes only OTA firmware images and release notes. Firmware source, Home Assistant integration code, complete flash/recovery images, PCB layouts, schematics, and private calibration data are not published.

These artifacts are for matching product hardware. Verify the model before programming or updating.
