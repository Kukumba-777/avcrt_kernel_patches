# AVCRT kernel patches for OnePlus Nord 1 (avicii / lito)

These patches let AVCRT replace the stock microphone signal and recover the
voice path during cellular calls on compatible routes.

**Experimental:** these patches are not final and may contain bugs.

## What the patches do

- [0001 — Bolero decimator mute](0001-audio-bolero-decimator-mute.patch): adds
  `AVCRT Dec Mute` to silence the stock microphone signal sent to the modem.
- [0002 — Voice CVP recovery](0002-audio-voice-cvp-recovery.patch): adds
  `AVCRT CVP Rebuild` to recover the call's voice processing path without
  restarting Android's audio service.

## How to apply

From the root of a clean, compatible OnePlus Nord 1 vendor Linux 4.19 source
tree, run the following. Adjust `patch_dir` if the repositories are not siblings.

```sh
patch_dir=../avcrt-kernel-patches/avicii-oneplus-nord-1
git apply --check \
  "$patch_dir/0001-audio-bolero-decimator-mute.patch" \
  "$patch_dir/0002-audio-voice-cvp-recovery.patch" &&
git apply \
  "$patch_dir/0001-audio-bolero-decimator-mute.patch" \
  "$patch_dir/0002-audio-voice-cvp-recovery.patch"
```

If the check fails, use `git apply --reverse --check` on each patch to see if
it is already present. Do not reapply it or force it onto an incompatible tree.
