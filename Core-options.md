## `[core]`

1. `plugins = viewport_impl move resize wobbly cube ...`

A space-separated list of enabled plugins. Due to current limitations, the `viewport_impl` plugin is required and must always be the first in the list.

2. `vwidth/vheight = 1,2,3,...`

Integer options, the number of horizontal/vertical workspaces. For now it can't be changed at runtime.

## `[input]`

1. `natural_scroll/tap_to_click/disable_while_typing = 1/0`

Touchpad-related options, self-explanatory.

2. `xkb_layout/xkb_option/xkb_variant`

Options to control the keyboard layout, they follow the same format as the corresponding `setxkbmap` options. Example:
```
xkb_layout = us,bg
xkb_option = grp:win_space_toggle,compose:ralt
xkb_variant = ,phonetic
```

3. `kb_repeat_rate/kb_repeat_delay = N`

Control keyboard repeat rate/delay. Example:

```
kb_repeat_rate = 40.000000
kb_repeat_delay = 400.000000
```

4. `cursor_size/cursor_theme`

Control the cursor size and theme. Example:
```
cursor_size = 24
cursor_theme = Bibata_Ice
```

5. Binding input devices to outputs

Some devices like built-in touchscreens should be mapped to exactly one output (e.g they apply only for that output). Find out the device name and the output name (usually by inspecting the log), then create a section as follows:

```
[device_name]
output = <output_name>

## Example:
[SYNA7501:00 06CB:16CA]
output = eDP-1
```