# Serial and audio interfaces

## /dev/ttyS0 — radio/DMR control

**CONFIRMED:** QuickChat's DMR service opens `/dev/ttyS0` at **57600 baud** through `DmrManager` and the Wonder serial stack.

The native layer is still under static analysis. Until that is complete, framing and ttyS0 termios details should be treated as partially understood.

## /dev/ttyS1 — PCM/audio

**CONFIRMED:** QuickChat initializes `/dev/ttyS1` with:

| Setting | Value |
|---|---|
| Baud | 230400 |
| Data bits | 8 |
| Stop bits | 1 |
| Parity | None |
| Flow control | None |

The application explicitly logs this as PCM serial initialization.

### Why ttyS1 is important

If this stream contains accessible receive PCM, it may provide the clean internal audio bridge needed for:

- APRS/AX.25 decoding
- Rattlegram/Ribbit receive
- other experimental receive-only audio/data decoders

The next task is to determine the framing and direction of the stream without transmitting or modifying radio state.

## Intercom sysfs interface

The application references platform-driver controls beneath `/sys/devices/platform/intercom/`, including power, PTT and PWD functions.

These are **not normal configuration files**. Do not probe them by writing guessed values. In particular, factory-test, firmware-update and PTT paths are excluded from blind experimentation.

## Research rule

Prefer, in order:

1. static APK/native-library analysis;
2. read-only observation;
3. reproducible receive-only tests;
4. controlled state-changing tests only after the interface is understood.

This keeps the stock handset usable as our reference device.
