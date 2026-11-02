# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A ZMK user-config repo for the Taira split keyboard (nice!nano v2 on each half, BLE split). There is no application code, no tests, and no local toolchain set up. The files are Devicetree, Kconfig, and YAML that ZMK compiles.

## Building

The firmware is built only by GitHub Actions. `.github/workflows/build.yml` calls ZMK's reusable `build-user-config.yml@v0.3` on every push, pull request, and manual dispatch. `build.yaml` defines the build matrix, and each matrix entry produces one `.uf2` in the `firmware` artifact:

- `taira_left`: the central half. It is built with the `studio-rpc-usb-uart` snippet and `-DCONFIG_ZMK_STUDIO=y`, so ZMK Studio works over USB on this half only.
- `taira_right`: the peripheral half.
- `settings_reset`: clears stored BLE bonds. It is the fix when the halves won't pair with each other.

To check a change, push it (or open a PR) and watch the run with `gh run list` / `gh run watch`. If the build fails, the Devicetree or Kconfig errors appear in the "Build" step log (`gh run view --log-failed`).

ZMK is pinned to `v0.3` in two places: `config/west.yml` and the workflow `uses:` ref. Change both together.

## Architecture

**Shield definition** (`config/boards/shields/taira/`):
- `Kconfig.shield` / `Kconfig.defconfig`: make the left half the split central and set the keyboard name.
- `taira.dtsi`: the shared GPIO matrix (5 rows × 7 cols, col2row) and the `default_transform`, which maps the 5×14 logical matrix to the 66 keymap positions. The right half's columns come from `col-offset = <7>` in `taira_right.overlay`. Note that its columns are mirrored in the transform, so the order runs RC(r,12)…RC(r,7).
- `taira-layouts.dtsi`: the `zmk,physical-layout` that ZMK Studio uses. It has 66 key entries in keymap binding order, derived from the upstream PCB, with the thumb clusters rotated ±30°.
- `taira.zmk.yml`: shield metadata. `features: studio` is listed here.

**Invariant:** keymap binding count, transform `map` entries, and physical-layout `keys` must all be 66 and in the same order. If you add, remove, or reorder positions, update all three.

**Keymap** (`config/taira.keymap`): the layers are DEFAULT(0), GAME(1), LOWER(2), RAISE(3), and ADJUST(4).
- GAME sits directly above DEFAULT on purpose. It replaces the base keys with no hold-tap behaviours, and LOWER/RAISE/ADJUST stay above it, so `&tog GAME` on ADJUST can still turn it off.
- ADJUST is reached two ways: as a tri-layer via `conditional_layers` (LOWER+RAISE), or by holding the `&lt ADJUST DEL` key.
- `extra1`/`extra2` are `status = "reserved"` layers. They give ZMK Studio room to add layers at runtime.
- Each layer has an ASCII-art comment above its bindings. `README.md` repeats the same diagrams. When you change bindings, update the layer's comment and the README diagram too.

**Global config** (`config/taira.conf`): sleep timeout, experimental BLE connection settings, +8 dBm TX power, and proxying the peripheral's battery level to the host.

## Flashing (from README)

Download the `firmware` artifact. Double-tap reset on a half (or use `Boot` on the Adjust layer) and copy that half's `.uf2` to the USB drive that appears. If the halves won't connect, flash `settings_reset` to both halves, then flash the real firmware, then reset both halves together.
