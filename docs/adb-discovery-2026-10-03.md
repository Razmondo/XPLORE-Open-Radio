# ADB discovery — 2026-10-03

## Scope

Read-only ADB reconnaissance of a stock Blackview XPLORE 1 Walkie Talkie. No root, flashing, partition writes, firmware updates or unattended transmission were performed.

## Confirmed device/platform observations

- Device identifies as the XPLORE 1 Walkie Talkie / `XPLORE_1_WT`.
- Android 15.
- MediaTek MT6877-family / Dimensity 7050 platform.
- Stock radio UI package: `com.chamsion.quickchat`, installed at `/system/app/QuickChat/QuickChat.apk`.
- A separate privileged Blackview component is present: `com.blackview.radioservice`, installed at `/product/priv-app/DKRadioService/DKRadioService.apk`.

The relationship between DKRadioService and QuickChat has not yet been proven. Static analysis of both APKs is the next step.

## Serial-device observations

The live ADB device listing shows `/dev/ttyS0` and `/dev/ttyS1` exposed with permissive mode bits (`crwxrwxrwx`) on this handset.

This is significant because earlier QuickChat static analysis identified:

- `/dev/ttyS0` at 57600 baud for the DMR/control stack.
- `/dev/ttyS1` at 230400 baud for a separate PCM/audio path.

Permissive device-node mode bits are encouraging, but they do **not** yet prove an ordinary third-party Android app can open either port: SELinux policy, process domain, device ownership and concurrent use by the stock service still need testing.

Other MediaTek modem/diagnostic tty devices are present. They are not targets for exploratory writes.

## APRS status correction

APRS over the built-in VHF/UHF hardware remains **unconfirmed**.

APRSdroid is available on the handset and can be configured for Audio (AFSK), but there has not yet been a controlled end-to-end RF test proving that a packet received by the XPLORE's built-in radio is decoded by APRSdroid, or that APRSdroid AFSK can be transmitted through the built-in radio.

Planned validation is a controlled bench test with a known-good APRS-capable radio (Anytone 878), testing RX first and then TX while collecting Android logs.

## PoC application clarification

VoxDMR is a Push-to-Talk-over-Cellular application. Its presence on the handset is not evidence about the XPLORE's built-in VHF/UHF DMR radio path and it should not be treated as an RF-radio control application.

## Next safe work

1. Pull the stock `QuickChat.apk` and `DKRadioService.apk` from the handset for local static analysis.
2. Map any Binder/services/intents linking QuickChat and DKRadioService.
3. Inspect native libraries and serial-open code without invoking upgrade/factory-test paths.
4. Determine whether a non-privileged test application can obtain read-only access to ttyS0/ttyS1.
5. Characterize ttyS1 receive framing before attempting any state-changing serial writes.
6. Run the controlled APRS bench test separately.

## Safety note

Do not blindly write bytes to ttyS0/ttyS1, intercom sysfs controls, firmware-update interfaces, factory-test functions or PTT controls. Receive-first observation remains the project rule.
