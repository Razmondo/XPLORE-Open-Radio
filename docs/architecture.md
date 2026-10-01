# Architecture

## Status labels

- **CONFIRMED** — observed directly on an XPLORE 1 or in the stock QuickChat application.
- **INFERRED** — strongly indicated by static analysis but not yet demonstrated end-to-end.
- **COMMUNITY REPORT** — reported independently by another owner.
- **TODO** — not yet established.

## High-level model

The current evidence points to three layers:

```text
QuickChat Android UI
       |
       +-- DMR/control stack
       |      DmrService
       |        -> DmrManager
       |        -> SerialTools / SerialPort
       |        -> libwonder_serialport.so
       |        -> /dev/ttyS0
       |
       +-- PCM/audio stack
       |      q0.f0
       |        -> SerialPortHelper
       |        -> /dev/ttyS1
       |
       +-- Linux platform driver
              /sys/devices/platform/intercom/
```

## DMR/control path — CONFIRMED

The stock application contains `com.wonder.dmr.DmrManager`. Decompiled application code opens:

```text
/dev/ttyS0
baud: 57600
```

The Java serial wrapper loads the native library `wonder_serialport`. The APK contains `libwonder_serialport.so` for arm64-v8a.

The exact termios configuration of ttyS0 is still a TODO until the native library analysis is completed. Do not assume 8N1 merely from the baud rate.

## PCM/audio path — CONFIRMED

A separate QuickChat code path initializes:

```text
/dev/ttyS1
baud: 230400
data bits: 8
stop bits: 1
parity: none
flow control: none
```

This is logged by the application as `initPcmSerialPort`.

This separation between control and PCM is one of the most promising findings for open data-mode integration.

## Linux intercom driver — CONFIRMED

QuickChat references an Android/Linux platform device under:

```text
/sys/devices/platform/intercom/
```

Observed application strings include controls for power, PTT and PWD. A factory-test interface also exists.

These nodes are documented here only as architecture evidence. Unknown writes can alter radio state, trigger transmission or enter test/update modes, so this project does not recommend exploratory writes.

## Open questions

1. What radio module/chipset sits behind ttyS0/ttyS1?
2. What is the PCM framing transported over ttyS1?
3. Is RX PCM continuously available, or only while QuickChat has configured a channel?
4. Can a third-party Android app access the same path safely without privileged permissions?
5. Does the module itself implement all DMR baseband/codec functions?
6. What exact serial setup does `libwonder_serialport.so` apply to ttyS0?

The immediate project strategy is to answer these questions receive-first.
