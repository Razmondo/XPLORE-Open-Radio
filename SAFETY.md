# Safety and scope

XPLORE Open Radio is an interoperability and reverse-engineering research project.

## Safe defaults

- Prefer static analysis and receive-only observation.
- Keep the stock handset recoverable.
- Back up important information before experiments.
- Treat undocumented serial and sysfs write interfaces as potentially state-changing.
- Do not invoke factory-test or firmware-update paths without verified documentation and a recovery plan.
- Do not assume a command is safe merely because its Java method name looks harmless.

## Radio operation

Transmission must comply with local spectrum rules and the operator's licence conditions. Frequency, power, mode, identification and permitted data/encryption rules vary by jurisdiction.

Documentation of an internal command does not imply that transmitting with it is legal or safe.

## Proprietary material

Do not commit:

- QuickChat APKs;
- Blackview firmware images;
- full decompiled proprietary source trees;
- extracted proprietary native libraries.

Original analysis, interoperability notes, hashes, small necessary factual excerpts and independently written open-source code are appropriate.

## Responsible research

If a finding could brick devices, trigger unintended RF transmission, bypass device security or expose private data, open an issue describing the high-level concern before publishing a turnkey procedure.
