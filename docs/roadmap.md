# Roadmap

## Phase 1 — Preserve and document stock behaviour

- [x] Identify QuickChat package and system-app status.
- [x] Identify separate DMR/control and PCM serial paths.
- [x] Record ttyS1 serial configuration.
- [x] Extract an initial DMR command map from static analysis.
- [ ] Record stock firmware/build and hashes for reference.
- [ ] Complete offline analysis of `libwonder_serialport.so`.
- [ ] Identify the radio module/chipset.

## Phase 2 — Receive-only audio/data

- [ ] Prove built-in VHF RX -> Android AFSK decoder.
- [ ] Characterize ttyS1 PCM framing.
- [ ] Capture/document receive audio without changing radio state.
- [ ] Prototype APRS/AX.25 receive.
- [ ] Prototype Rattlegram/Ribbit receive.

## Phase 3 — Open Android interface

- [ ] Build a basic channel/status UI.
- [ ] Add RSSI and receive-state monitoring.
- [ ] Build a practical DMR monitor/scanner view.
- [ ] Add APRS station/message display.
- [ ] Add keyboard-oriented Rattlegram/Ribbit interface.

## Phase 4 — Controlled interoperability

Only after the control/audio interfaces are understood and receive functions are stable:

- [ ] Evaluate safe, licensed transmit integration.
- [ ] Explore APRS messaging.
- [ ] Explore open packet modes (FX.25/IL2P).
- [ ] Investigate Codec2/FreeDV/M17 possibilities.

## Design principles

1. Receive first.
2. Preserve a stock reference handset.
3. Never guess at firmware/factory-test commands.
4. Label evidence by confidence.
5. Prefer existing open-source components over reinventing protocols.
6. Keep proprietary firmware/APKs out of this repository.
