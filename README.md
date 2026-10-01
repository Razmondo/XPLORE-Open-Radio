# XPLORE Open Radio

Community reverse-engineering and open-radio research for the **Blackview XPLORE 1 Walkie Talkie** Android phone.

The project is investigating how the stock QuickChat application talks to the phone's built-in analogue/DMR radio hardware, with the long-term goal of an easier, open interface for radio monitoring and amateur-radio data modes.

## Project goals

- Document the stock radio architecture.
- Build a receive-first DMR monitor/scanner interface.
- Explore APRS/AX.25 receive and messaging.
- Explore keyboard-to-keyboard text using open audio modes such as Rattlegram or Ribbit.
- Understand the internal PCM/audio path well enough to avoid awkward speaker-to-microphone coupling.
- Identify the underlying radio module/chipset and any public documentation.
- Keep findings reproducible and clearly separated into **confirmed**, **community reported**, and **hypothesis/TODO**.

## What we know so far

Static analysis of the stock system app has identified two distinct serial paths:

- **DMR/control path:** QuickChat uses the `com.wonder.dmr` stack and opens `/dev/ttyS0` at 57600 baud.
- **PCM/audio path:** QuickChat initializes `/dev/ttyS1` at 230400 baud, 8 data bits, 1 stop bit, no parity and no flow control.
- The Android platform exposes an `intercom` device with separate power/PTT/PWD controls.
- QuickChat is a privileged system application: `com.chamsion.quickchat`, version `V1.0`.

See [docs/architecture.md](docs/architecture.md) for the evidence and confidence levels.

## Current milestone

**Prove and document a receive-only path from the built-in VHF/UHF receiver into an Android decoder.**

APRSdroid/AFSK is our first practical test case. After that, the PCM framing is the most important unknown for native APRS and Rattlegram/Ribbit integration.

## Documentation

- [Architecture](docs/architecture.md)
- [QuickChat](docs/quickchat.md)
- [Serial and audio interfaces](docs/serial-interfaces.md)
- [DMR protocol notes](docs/dmr-protocol.md)
- [APRS experiments](docs/aprs.md)
- [Community research](docs/community-research.md)
- [Roadmap](docs/roadmap.md)
- [Safety and scope](SAFETY.md)

## Safety and legal scope

This repository documents interfaces and experiments for legitimate interoperability and amateur-radio research. Receive-only investigation comes first. Do not blindly write to unknown serial commands, sysfs nodes, factory-test controls, firmware-update paths, or transmit controls.

Users are responsible for complying with the radio regulations and licence conditions in their jurisdiction.

## Repository policy

This repository does **not** redistribute Blackview firmware, the proprietary QuickChat APK, decompiled source trees, or extracted proprietary native libraries. Documentation here is original research based on observations and static analysis.

## Status

Early research / reverse engineering. Expect findings to change as they are independently reproduced.

Contributions from other XPLORE 1 owners are very welcome.
