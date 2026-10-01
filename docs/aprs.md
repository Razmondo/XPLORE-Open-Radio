# APRS / AFSK experiments

## Goal

Establish whether the XPLORE 1's built-in VHF receiver can feed an Android AFSK decoder directly.

The first target is the UK 2 m APRS channel, **144.800 MHz**, using receive-only tests.

## Local experiment

A stock QuickChat analogue channel was configured for 144.800 MHz and APRSdroid was configured to use its **Audio (AFSK)** connection mode with the high-quality demodulator.

APRSdroid successfully generated an AFSK burst when its local send-position function was accidentally tested. That proves Android-side AFSK generation works, but **does not prove that the built-in radio transmitted it** and does not establish an internal TX audio route.

Likewise, seeing stations in APRSdroid is not by itself proof of RF reception because APRS data can also arrive through internet infrastructure or cached state.

### Result so far

**UNCONFIRMED:** built-in VHF RX -> APRSdroid AFSK decoder.

This remains our first end-to-end milestone.

## Community evidence

A myGMRS XPLORE 1 discussion includes an owner report that APRSdroid works on the handset and specifically mentions AFSK mode. This is encouraging independent evidence, but the exact internal audio route still needs reproduction and documentation.

An APRS.fi station description has also identified use of a Blackview XPLORE 1 with APRSdroid; observed TCP/IP routing means that example alone is not proof of RF AFSK decoding.

## Next receive-only tests

- Distinguish APRS-IS/network packets from locally decoded AFSK frames in logs.
- Use a known legal RF APRS source when available to create a controlled receive test.
- Continue static analysis of the ttyS1 PCM path.
- Determine whether QuickChat exposes/captures internal receive audio in a way another Android application can consume.

## Sources

- myGMRS XPLORE 1 discussion: https://forums.mygmrs.com/topic/12029-soooi-just-bought-a-hamgmrscell-phone-combo-blackview-xplore-1/
- APRS.fi: https://aprs.fi/
