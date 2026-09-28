# zmk-config-zyraft

## Overview

ZMK configuration for **Zyra FT** (Sweep/Cradio) - minimalist ergonomic FalbaTech keyboard.

## Hardware

- Shield: `cradio` (official upstream ZMK shield)
- Controllers: 2x nice!nano v2
- No display, pin D1/P0.06 used by switch matrix
- 34 keys, 3 rows x 5 columns + 2 thumb keys per side
- Home-row mods enabled, Shift/Alt/Ctrl/Gui

## Layers

| # | Name | Function |
|---|---|---|
| 0 | `default_layer` | QWERTY base + home-row mods |
| 1 | `right_layer` | Numbers, navigation, activated by right thumb |
| 2 | `left_layer` | Symbols, brackets, activated by left thumb |
| 3 | `tri_layer` | System, BT controls, both thumbs together |

## Home-row mods

### Left hand

- `A` = Shift
- `S` = Alt
- `D` = Ctrl
- `F` = Gui

### Right hand

- `J` = Gui
- `K` = Ctrl
- `L` = Alt
- `'` = Shift

Parameters:
- Tapping-term: 220ms
- Quick-tap: 150ms
- Require-prior-idle: 100ms

## ZMK Studio

ZMK Studio is enabled.

The unlock procedure is the same across all FalbaTech FT keyboards:

> Hold both thumb keys activating system layers, TAB + BSPC, and press the top left key.

After unlocking, the keyboard can be configured from your browser:

https://zmk.studio

## Bluetooth - 5 device support

The keyboard supports 5 independent Bluetooth profiles. Control is handled in the `tri_layer`.

| Key | Function |
|---|---|
| `Z` | BT Profile 0 |
| `X` | BT Profile 1 |
| `C` | BT Profile 2 |
| `V` | BT Profile 3 |
| `B` | BT Profile 4 |
| `N` | Clear active profile |
| `M` | Clear all profiles |
| `,` | USB mode |
| `.` | Bluetooth mode |

System layer activation:
- hold the left thumb `TAB` and right thumb `BSPC` together
- the Tri layer activates automatically as a conditional layer

## Build

GitHub Actions builds 3 firmware files:

- `zyra_left-nice_nano-zmk.uf2`
- `zyra_right-nice_nano-zmk.uf2`
- `settings_reset-nice_nano-zmk.uf2`

## Flashing

1. Connect the left half via USB.
2. Press RESET twice quickly.
3. Drag `zyra_left-...uf2` onto the `NICENANO` drive.
4. Connect the right half via USB.
5. Press RESET twice quickly.
6. Drag `zyra_right-...uf2`.
7. Connect both halves using a TRRS cable.
8. Pair the keyboard as "Zyra FT" over Bluetooth.

## Support

FalbaTech  
https://falbatech.click
