# CH592 1.4.7 OTA

Requires HA integration 0.6.9+. Chinese is the default; English is available.

After this firmware is installed: click Update in HA, download and verify locally, wait for a normal advertising window to wake OTA automatically, upload and verify, reboot, and confirm a fresh target-version advertisement. Future updates require no B-button press.

The FIRST installation from firmware 1.4.6 or earlier still needs the existing B-button OTA entry or a private local wired-flash image: older firmware cannot receive a remote wake request. The new behavior requires both firmware 1.4.7 and HA integration 0.6.9.

No idle connection or OTA session is started. The first advertisement remains at about 60 seconds for 1 second; subsequent normal advertisements last about 300 ms per minute and now accept connections. HA connects only after an Update click and successful local verification. Missed windows are retried, with a three-minute wake timeout. Physical connection success and power consumption have not been measured; identical battery life is not guaranteed.

B remains available: release after about 5.1 seconds for existing nRF Connect settings, or hold about 10.2 seconds for manual OTA. Five idle seconds after release exits; valid OTA commands refresh the timer. B need not stay held during transfer.

This package contains the OTA application image only and requires an installed OTA bootloader. Complete wired-flash/recovery images remain private and local. Private application source, PCB and calibration data are not published.

Independent builds match. Host protocol, key, storage, idle, wake-window, connection-race, command and image checks pass. HA regression tests pass. Physical end-to-end OTA validation remains pending.
