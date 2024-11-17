# Prospector ZMK Module

All the necessary stuff for Prospector to display things with ZMK. Currently functional albeit barebones.

## Features

- Highest active layer roller
- Peripheral battery
- Peripheral connection status

## Installation

Your ZMK keyboard should be set up with a dongle as central.

Add this module to your `config/west.yml` with these new entries under `remotes` and `projects`:

```
manifest:
  remotes:
    - name: zmkfirmware
      url-base: https://github.com/zmkfirmware
    - name: carrefinho                            # <--- add this
      url-base: https://github.com/carrefinho     # <--- and this
  projects:
    - name: zmk
      remote: zmkfirmware
      revision: main
      import: app/west.yml
    - name: prospector-zmk-module                 # <--- and these
      remote: carrefinho                          # <---
      revision: main                              # <---
  self:
    path: config
```

Then add the `prospector_adapter` shield to the dongle in your `build.yaml`:

```
---
include:
  - board: seeeduino_xiao_ble
    shield: [YOUR KEYBOARD SHIELD]_dongle prospector_adapter
```

## Usage

For split keyboards, since the peripheral battery widget uses the order in which peripherals were paired to arrange the sub-widgets, after flashing the dongle, pair the left side first and then the right side. With more than two peripherals, pair them in a left to right order.

The layer roller shows layers' `display-name` property whenever available, and will fall back to the layer index otherwise. To add a `display-name` property to a keymap layer:

```
keymap {
  compatible = "zmk,keymap";
  base {
    display-name = "Base";           # <--- add this
    bindings = <
      ...
    >;
  }
}
```

## Configuration
