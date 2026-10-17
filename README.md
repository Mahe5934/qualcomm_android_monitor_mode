# qualcomm_android_monitor_mode

Qualcomm QCACLD WiFi (Android) monitor mode

[

![Monitor mode](https://img.shields.io/badge/monitor%20mode-working-brightgreen.svg)

]()
[

![Kali](https://img.shields.io/badge/Kali-supported-blue.svg)

](https://www.kali.org)
[

![aircrack-ng](https://img.shields.io/badge/aircrack--ng-supported-blue.svg)

](https://github.com/aircrack-ng/aircrack-ng)
[

![wifite2](https://img.shields.io/badge/wifite2-supported-blue.svg)

](https://github.com/derv82/wifite2)

## NOTES

This method works out of the box on devices where CodeAurora enabled monitor mode
at the driver level — no kernel patch required. The patch in `files/` is only
needed on older or unmaintained kernels where the switch wasn't flipped upstream.

## DEPENDENCIES

1. A rooted Android environment.
2. A kernel with the `con_mode` driver parameter exposed (no custom kernel
   compile required on most modern devices — see `monmode` below).
3. A WiFi chipset using the QCACLD driver/firmware.

Older devices/drivers may need the patch in `files/`. Future kernels (4.9, 4.14,
4.19+) often ship this working out of the box from vendor. See
`LIST_OF_DEVICES.txt` for known-working phones. Use issue reports for new
device confirmations.

---

## `monmode` — monitor mode toggle script

A self-contained shell script that switches WiFi between managed and monitor
mode by writing directly to the driver's `con_mode` sysfs parameter, with
channel/frequency setup and status verification built in.

**Tested on:** Nothing Phone 2 (qca6490). Device-specific — no fallback paths
for other chipsets. If your device uses a different driver module, adjust
`DRV_PARAM` at the top of the script accordingly (check
`/sys/module/*/parameters/con_mode`).

### Usage

```sh
su
./monmode on [channel|MHz]   # default: channel 1 (2412 MHz)
./monmode off
./monmode status
