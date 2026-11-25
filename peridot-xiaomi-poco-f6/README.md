# AVCRT kernel patches for Xiaomi Poco F6 (peridot / sm8635)

These patches let AVCRT replace the stock microphone signal during cellular
calls on compatible codec and USB-C headset routes.

**Experimental:** these patches are not final and may contain bugs.

## What the patches do

- [0001 — LPASS microphone mute](0001-audio-lpass-tx-mute-lease.patch): lets
  AVCRT temporarily mute the original microphone on the codec path. The driver
  restores the signal when the mute expires or the affected route changes.
- [0002 — SPF voice routing and USB-C microphone cutoff](0002-audio-spf-voice-tx-usb-cutoff.patch):
  tracks the active call route, handles a rejected start during a route switch,
  and lets AVCRT mute the original USB-C microphone feed while verifying the
  mute and its rollback with the DSP.

## How to apply

Apply from the root of the clean Linux 6.1 **vendor modules** source tree, not
the main kernel tree. Use the `seventeen` base at commit
[`ed4ad0d1ad00`](https://github.com/peridot-dev/android_kernel_xiaomi_sm8635-modules/commit/ed4ad0d1ad00b755af2fe61387dcc5397ad20b8f).
Adjust `patch_dir` if the repositories are not siblings.

```sh
patch_dir=../avcrt-kernel-patches/peridot-xiaomi-poco-f6
git apply --check \
  "$patch_dir/0001-audio-lpass-tx-mute-lease.patch" \
  "$patch_dir/0002-audio-spf-voice-tx-usb-cutoff.patch" &&
git apply \
  "$patch_dir/0001-audio-lpass-tx-mute-lease.patch" \
  "$patch_dir/0002-audio-spf-voice-tx-usb-cutoff.patch"
```

If the check fails, use `git apply --reverse --check` on each patch to see if
it is already present. Do not reapply it or force it onto an incompatible tree.
