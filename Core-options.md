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

## `[workarounds]`

This is a section which contains some hacks that might be required to make things work. Fortunately there is only a single option supported for now.

1. `app_id_mode = stock/gtk-shell/full`

TL;DR: if you use only `wf-dock` as task manager/dock, set to `full`. Otherwise, try `stock` and `gtk-shell`, and use whichever works better for you.

In contrast to X, in wayland clients like taskbars, docks, etc. can't just query the icon of a window. They need to obtain it by using some heuristics involving the app-id. However, in GTK3 there is a bug where the application sometimes reports the wrong app-id. There is a custom protocol(`gtk-shell1`) which can be used to get the correct app-id. The situation will get better in GTK4 where the bug is fixed, but in the meantime we somehow need to supply the dock/taskmanager with both app-ids (the potentially wrong one and the potentially missing one from `gtk-shell1`). This isn't possible with the regular protocols, that's why `wayfire` and `wf-dock` use a custom format (when `app_id_mode=full`) so that both app-ids can be sent at the same time. This would unfortunately break clients that are unaware of this hack. That's why it's up to the user of Wayfire to select whichever mode works best for them, depending on what clients they use.

