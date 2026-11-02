# Taira Keyboard ZMK config

This repository builds ZMK firmware (pinned to ZMK `v0.3`) for the [Taira Keyboard](https://github.com/strayer/taira-keyboard).

## Flashing

1. download the `firmware` artifact from the latest [Action run](https://github.com/austigon/austin-taira-keyboard-config/actions)
2. attach one Taira side to a computer by USB-C
3. put the Taira into flash mode by double-pressing the reset button, or by pressing `Boot` on the Adjust layer on that side
4. copy the relevant .uf2 file to the attached USB storage device to flash the nice!nano
5. repeat for the other side
6. fork this repository to customize the keymap.

If the halves won't connect to each other, flash `settings_reset` to both halves first, then flash the left and right firmware, reset both halves at about the same time, and re-pair with your computer.

TODO: let the Github Action create a new release with the firmware file to avoid the automatic deletion of Github Action artifacts.

## Keymap

The left half is the central (the one that connects to the computer). Hold `Lower` + `Raise` together, or hold the top-right `Del/Adj` key, for the Adjust layer.

### Default

```
.-------------------------------------------------------------------------------------------------------------------------------------.
| Esc  |  1   |  2   |  3   |  4   |  5   |                                                  |  6   |  7   |  8   |  9   |  0   |Del/Adj|
|------+------+------+------+------+------|                                                  |------+------+------+------+------+-------|
| Tab  |  Q   |  W   |  E   |  R   |  T   |                                                  |  Y   |  U   |  I   |  O   |  P   |  \    |
|------+------+------+------+------+------|                                                  |------+------+------+------+------+-------|
|Ctl/Es|  A   |  S   |  D   |  F   |  G   |                                                  |  H   |  J   |  K   |  L   |  ;   |  '    |
|------+------+------+------+------+------+------+------.                  .------+------+------+------+------+------+------+-------|
| Shift|  Z   |  X   |  C   |  V   |  B   |      | Vol- | Vol+ |  | Home | End  |      |  N   |  M   |  ,   |  .   |  /   | Shift |
|------+------+------+------+------+------+------+------+------|  |------+------+------+------+------+------+------+------+-------|
| Alt  | Play | Rwnd | FFwd |             | Meta |Space |Lower |  | Bspc |Sft/En|Raise |             | Left | Down |  Up  | Right |
'-------------------------------------------------------------------------------------------------------------------------------------'
```

`Ctl/Es` is Esc on tap and Ctrl on hold, `Sft/En` is Enter on tap and Shift on hold, and `Del/Adj` is Delete on tap and the Adjust layer on hold.

### Game (toggled with `Game` on the Adjust layer)

No hold-tap keys, so nothing is delayed or misfires mid-game.

```
.-------------------------------------------------------------------------------------------------------------------------------------.
|  `   |  1   |  2   |  3   |  4   |  5   |                                                  |  6   |  7   |  8   |  9   |  0   | PScr  |
|------+------+------+------+------+------|                                                  |------+------+------+------+------+-------|
| Tab  |  Q   |  W   |  E   |  R   |  T   |                                                  |  Y   |  U   |  I   |  O   |  P   |  \    |
|------+------+------+------+------+------|                                                  |------+------+------+------+------+-------|
| Esc  |  A   |  S   |  D   |  F   |  G   |                                                  |  H   |  J   |  K   |  L   |  ;   |  '    |
|------+------+------+------+------+------+------+------.                  .------+------+------+------+------+------+------+-------|
| Shift|  Z   |  X   |  C   |  V   |  B   |      | Del  | PgDn |  | PgUp | Home |      |  N   |  M   |  ,   |  .   |  /   | Enter |
|------+------+------+------+------+------+------+------+------|  |------+------+------+------+------+------+------+------+-------|
| Ctrl | Alt  | Meta | Alt  |             | Meta |Space |Lower |  |Raise | Bspc | RAlt |             | Left | Down |  Up  | Right |
'-------------------------------------------------------------------------------------------------------------------------------------'
```

### Lower

Blank keys fall through to the layer below (thumb keys and modifiers) or do nothing.

```
.-------------------------------------------------------------------------------------------------------------------------------------.
|      |  F1  |  F2  |  F3  |  F4  |  F5  |                                                  |  F6  |  F7  |  F8  |  F9  | F10  | F11   |
|------+------+------+------+------+------|                                                  |------+------+------+------+------+-------|
|  ~   |      |  ~   |  {   |  }   |      |                                                  | Home |Wd Lft|  Up  |Wd Rgt| End  | F12   |
|------+------+------+------+------+------|                                                  |------+------+------+------+------+-------|
|      |  -   |  +   |  (   |  )   |      |                                                  |  ^   | Left | Down |Right |      |       |
|------+------+------+------+------+------+------+------.                  .------+------+------+------+------+------+------+-------|
|      |  _   |  =   |  (   |  [   |      |      |      |      |  |      |      |      |      |      |      |      |      |       |
|------+------+------+------+------+------+------+------+------|  |------+------+------+------+------+------+------+------+-------|
|      |      | Prev | Next |             |      |      |      |  |      |      |      |             |      |      |      |       |
'-------------------------------------------------------------------------------------------------------------------------------------'
```

### Raise

```
.-------------------------------------------------------------------------------------------------------------------------------------.
|      |  F1  |  F2  |  F3  |  F4  |  F5  |                                                  |  F6  |  F7  |  F8  |  F9  | F10  | F11   |
|------+------+------+------+------+------|                                                  |------+------+------+------+------+-------|
|  `   |  1   |  7   |  8   |  9   |      |                                                  | Home |Wd Lft|  Up  |Wd Rgt| End  | F12   |
|------+------+------+------+------+------|                                                  |------+------+------+------+------+-------|
|  ~   |  !   |  4   |  5   |  6   |      |                                                  |  ^   | Left | Down |Right |      |       |
|------+------+------+------+------+------+------+------.                  .------+------+------+------+------+------+------+-------|
|      |  0   |  1   |  2   |  3   |      |      |      |      |  |      |      |      |  }   |  ]   |  )   |  +   |  _   |       |
|------+------+------+------+------+------+------+------+------|  |------+------+------+------+------+------+------+------+-------|
|      |  /   |  _   |  .   |             |      |      |      |  |      |      |      |             |      |      |      |       |
'-------------------------------------------------------------------------------------------------------------------------------------'
```

### Adjust (Lower + Raise, or hold `Del/Adj`)

```
.-------------------------------------------------------------------------------------------------------------------------------------.
| BT0  | BT1  | BT2  | BT3  | BT4  |      |                                                  | BT0  | BT1  | BT2  | BT3  | BT4  |       |
|------+------+------+------+------+------|                                                  |------+------+------+------+------+-------|
| Boot |      |      |      |      |      |                                                  |      |      |      |      |      | Boot  |
|------+------+------+------+------+------|                                                  |------+------+------+------+------+-------|
|Reset |      |      |      |      | Game |                                                  |      |      |      |      |      | Reset |
|------+------+------+------+------+------+------+------.                  .------+------+------+------+------+------+------+-------|
|      |      |      |      |      |      |      |      |      |  |      |      |      |      |      |      |      |      |       |
|------+------+------+------+------+------+------+------+------|  |------+------+------+------+------+------+------+------+-------|
|BT Clr|      |      |      |             |      |      |      |  |      |      |      |             |      |      |      |BTClrAl|
'-------------------------------------------------------------------------------------------------------------------------------------'
```

- `BT0`–`BT4` pick a Bluetooth profile (one per paired computer).
- `BT Clr` forgets the computer on the current profile; `BTClrAl` forgets all of them.
- `Boot` puts that half into flashing mode; `Reset` restarts that half. Each half has its own pair.
- `Game` toggles the Game layer on and off.
