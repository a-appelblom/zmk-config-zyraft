# zmk-config-zyraft

## Overview

ZMK configuration for **Zyra FT** (Sweep/Cradio) - minimalist ergonomic FalbaTech keyboard.

## Hardware

- Shield: `cradio` (official upstream ZMK shield)
- Controllers: 2x nice!nano v2
- No display, pin D1/P0.06 used by switch matrix
- 34 keys, 3 rows x 5 columns + 2 thumb keys per side
- Home-row mods enabled: Ctrl/Alt/Gui/Shift on the left, mirrored on the right

## Layers

| # | Name | Function |
|---|---|---|
| 0 | `default_layer` | QWERTY base + home-row mods, compensated for a **Swedish** OS keyboard layout (default) |
| 1 | `right_layer` | Numbers, navigation (arrows on `I`/`J`/`K`/`L`), compensated for Swedish, activated by the left thumb (`BSPC`) |
| 2 | `left_layer` | Symbols, brackets, Swedish letters, compensated for Swedish, activated by the left thumb (`TAB`), `Z` or `-` |
| 3 | `tri_layer` | System, BT controls, both left thumb keys together |
| 4 | `default_layer_en` | English OS-layout overlay of the base layer, toggled via `LANG` |
| 5 | `right_layer_en` | English OS-layout overlay of `right_layer` |
| 6 | `left_layer_en` | English OS-layout overlay of `left_layer` |

## Symbols layer access

The `left_layer`/`left_layer_en` symbols layer can be reached three ways:

- Hold the `TAB` thumb key (as usual).
- Hold `Z` (bottom-row, outermost key on the left half).
- Hold `-` (bottom-row, outermost key on the right half - this key used to be `/`;
  `/` now lives on the symbols layer instead, see below).

`Z` and `-` still tap their normal character when tapped briefly. Whichever key is
used to enter the layer, the `TAB` thumb key becomes free, so tapping it while the
layer is held sends **Escape**.

The symbols layer layout (based on the ZSA Voyager symbols layer):

- Top row: `!` `"` `'` `~` `*`  |  `{` `}` `#` `+` `?`
- Home row: (trans) `Å` `Ä` `Ö` `` ` ``  |  `[` `]` `$` `&` `|`
- Bottom row: `/` `^` `%` `\` `@`  |  `(` `)` `<` `>` (hold, entry key)

`Å`/`Ä`/`Ö` are only available on the Swedish symbols layer (`left_layer`); the
English one (`left_layer_en`) leaves those slots transparent since there's no
single-key way to type them on an English OS.

## Home-row mods

### Left hand

- `A` = Ctrl
- `S` = Alt
- `D` = Gui
- `F` = Shift

### Right hand

- `J` = Shift
- `K` = Gui
- `L` = Alt
- `=` = Ctrl

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
- hold the left thumb keys `TAB` and `BSPC` together
- the Tri layer activates automatically as a conditional layer

## Swedish/English OS-layout support

ZMK sends raw HID keycodes; the OS keyboard-language setting determines which character each
keycode produces. The keyboard **defaults to a Swedish OS keyboard layout** (layers 0-2 are
compensated so the same physical keys produce the expected Swedish symbols). `default_layer_en`,
`right_layer_en` and `left_layer_en` are a secondary set that instead compensate for an
**English (US)** OS keyboard layout.

- Press `LANG` on the `tri_layer` (top-left key of the right half) to toggle the English
  overlay on or off. Press it again to switch back to the Swedish default.
- Letters are unaffected - Swedish keyboards use the same QWERTY letter positions as US ones.
- `^`, `~` and `` ` `` are dead keys on the Swedish layout; the base layer sends a macro that
  presses the compensated combo followed by Space so the bare character still appears
  immediately.
- Mappings target **macOS's** Swedish layout (Option key = AltGr). Windows/Linux use
  different combinations for `{`, `}`, `|` and `\`, so those four keys would need adjusting
  if used with Windows or Linux set to Swedish.
- The Swedish `<`/`>` bindings use `GRAVE`/`Shift+GRAVE` to compensate for macOS
  swapping the ISO `NUBS` and `GRAVE` HID positions on this keyboard.
- Swedish letters `Å`, `Ä`, `Ö` are available on `left_layer` (symbols layer), on the
  home row. They're only mapped in the Swedish layer set, since the English layer set
  assumes an English OS layout with no single-key way to produce them.

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
