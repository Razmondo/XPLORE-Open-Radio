# Community and public research

This page separates third-party reports from findings reproduced on our own device.

## Blackview / public specifications

Public Blackview material describes the Walkie Talkie edition as a hardware VHF/UHF analogue/digital radio handset rather than an internet-only push-to-talk service.

## myGMRS

A long-running XPLORE 1 owner discussion contains reports of:

- successful repeater contacts;
- DMR operation requiring experimentation;
- APRSdroid working on the handset;
- AFSK being the APRSdroid connection type used.

These are **COMMUNITY REPORTS** until independently reproduced.

Source:
https://forums.mygmrs.com/topic/12029-soooi-just-bought-a-hamgmrscell-phone-combo-blackview-xplore-1/

## 4PDA

Community discussion has covered the XPLORE radio software, firmware/root experiments and radio/headset behaviour. Reports include limitations around DMR monitoring and some audio/accessory behaviour.

Firmware/root anecdotes are useful as recovery research, but are not treated as instructions. The project is deliberately keeping its main reference handset stock while the radio interfaces are still being mapped.

Source:
https://4pda.to/forum/index.php?showtopic=1118235

## Tech Minds

Tech Minds has published a hands-on XPLORE 1 radio video covering analogue/DMR operation and radio testing.

Source:
https://www.youtube.com/watch?v=N08KmKLJiEM

## Chamsion / Wonder lead

The stock package name is `com.chamsion.quickchat`, while the DMR/serial Java namespaces include `com.wonder.*`.

Current working hypothesis: identifying the ODM/module supplier behind those names may reveal documentation or another product using the same radio subsystem.

This is a **research lead**, not a confirmed attribution of the radio design.

## Search targets

Useful future searches include:

- `com.chamsion.quickchat`
- `libwonder_serialport`
- `com.wonder.dmr`
- `intercom_ptt_control`
- `intercom_power_control`
- Chinese-language combinations involving 对讲机 (walkie-talkie), 串口 (serial), DMR and the relevant vendor/module names.

If you find another device exposing the same class names or Linux driver strings, please open an issue.
