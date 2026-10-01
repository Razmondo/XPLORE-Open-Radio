# QuickChat stock application

## Confirmed package information

The built-in radio UI is a privileged Android system application.

| Field | Observed value |
|---|---|
| Package | `com.chamsion.quickchat` |
| System path | `/system/app/QuickChat` |
| Version name | `V1.0` |
| Version code | `1` |
| Minimum SDK | 29 |
| Target SDK | 36 |
| Primary ABI | arm64-v8a |

The package requests/holds unusually strong audio/system permissions consistent with its role as the built-in radio controller, including audio settings, audio capture, secure settings, microphone and media-control capabilities.

## Native components

Static inspection found serial-port native libraries including:

- `libwonder_serialport.so`
- `libserialport.so`

The Java class `com.wonder.serial.SerialPort` loads `wonder_serialport` and exposes native open/setup/read/write/close functions.

## Interesting application strings

The stock app contains references to:

- `/dev/ttyS1`
- `/dev/ttyUSB0`
- `/proc/tty/drivers`
- `/quickchat/`
- the Linux `intercom` platform-device controls
- DMR upgrade-related code paths

The presence of an upgrade path is **not** an invitation to invoke it. Firmware/update and factory-test functions are deliberately outside normal experimentation until the hardware and recovery process are understood.

## Why this matters

QuickChat appears to be much more than a conventional Android walkie-talkie UI. It is the privileged bridge between Android, a serial-controlled DMR subsystem, a separate PCM serial path and the platform's radio-control driver.

That architecture gives the project a realistic route toward a new Android front end without replacing radio firmware.
