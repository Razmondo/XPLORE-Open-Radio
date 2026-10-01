# DMR protocol notes

This page records a **partial, inferred** map of the QuickChat-to-radio protocol. It is for static-analysis documentation, not a recipe for sending commands to the live module.

## Frame structure

QuickChat's Java code strongly suggests a normal command frame with:

```text
byte 0      0x68
byte 1      command ID
bytes 2-3   command-specific mode/status fields
bytes 4-5   checksum
bytes 6-7   payload length, big endian
bytes 8..   payload
final byte  0x10
```

Observed parser logic indicates a total frame size of payload length + 9. Checksum handling zeroes/replaces the checksum field during calculation.

This structure remains **INFERRED** until verified against captured receive/control traffic.

## Command IDs observed in application code

The following semantic names are based on QuickChat/DmrManager code:

| ID | Observed purpose |
|---|---|
| 0x22 | digital configuration |
| 0x23 | analogue configuration |
| 0x26 | launch/transmit-related command |
| 0x27 | initialization-complete check |
| 0x28 | enhancements |
| 0x29 | encryption |
| 0x2A | microphone gain |
| 0x2B | digital voice reception information |
| 0x2C | text message |
| 0x2D | SMS retrieval |
| 0x2E | volume |
| 0x2F | monitor |
| 0x30 | squelch |
| 0x31 | power saving |
| 0x32 | RSSI |
| 0x33 | relay/offline |
| 0x34 | version |
| 0x35 | transfer interrupt |
| ~0x37 | polite-related setting; needs verification |
| ~0x3A | SMS protocol; needs verification |
| ~0x3B | TOT; needs verification |
| ~0x3C | speaker enable; needs verification |

The approximate entries need additional verification before being promoted to confirmed mappings.

## Deliberately excluded

The application contains transmission, upgrade and low-level control functions. This repository will not publish guessed live-write procedures for those interfaces. We first want passive captures and independent confirmation of the protocol.
