# AVCRT Kernel Patches

[AVCRT (Android Voice Changer Real Time)](https://github.com/Kukumba-Z/Android_Voice_Changer_Real_Time)
is a real-time voice changer for rooted Android devices. It can apply voice
effects and mix soundboard clips into supported recordings and calls.

## Why these patches are needed

Cellular (SIM) calls use a device-specific audio path separate from ordinary
app recording. These patches let AVCRT identify or recover that path and mute
the original microphone signal so the other caller hears the processed audio
instead of both signals. The patches do not process audio on their own; AVCRT
does that separately.

## Devices

| Device | Kernel source | Patch guide |
| --- | --- | --- |
| OnePlus Nord 1 (`avicii`) | Vendor Linux 4.19 kernel | [AVCRT patches for OnePlus Nord 1](avicii-oneplus-nord-1/README.md) |
| Xiaomi Poco F6 (`peridot`) | Vendor modules for Linux 6.1 | [AVCRT patches for Xiaomi Poco F6](peridot-xiaomi-poco-f6/README.md) |

## How to use

These are source patches, not flashable packages. Follow the guide for your
device: check that the patches apply to the matching source tree with
`git apply --check`, then apply them and rebuild the affected kernel or modules.

**Experimental:** these patches are not final and may contain bugs.
Compatibility depends on the kernel, firmware, and call audio route. Do not
apply a device's patches to another model or force them onto an incompatible
source tree.
