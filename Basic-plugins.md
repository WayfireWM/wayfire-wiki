Each plugin is listed with its config section. To enable a plugin, add its name (the same as config section) to the plugins list in `[core]` section.

See the [configuration](https://github.com/WayfireWM/wayfire/wiki/Configuration) for more details on the bindings format.


## `[autostart]`

The autostart plugin lets the user specify what commands should be run whenever Wayfire starts.

All entries are in the form `program_id = <shell_command>`. The `program_id`'s don't matter, but must be
different for different commands. Default:

```
background = /usr/bin/wf-background
panel = /usr/bin/wf-panel
```

## `[command]`

The command plugin lets the user associate button/key/touch bindings with different commands.
The format is:

```
binding_id = <action binding>`
command_id = <command>
```

The id can consist of digits and letters, and doesn't have any special meaning. Some examples:

```
binding_1 = <super> KEY_D
command_1 = dmenu_run
binding_2 = <super> KEY_ENTER
command_2 = tilix
binding_5 = KEY_MUTE | BTN_EXTRA
command_5 = amixer -q sset Master toggle

binding_lock = <super> KEY_L                                                                                                                      
command_lock = swaylock
```

## `[move]`

A plugin to move windows by dragging them.

1. `activate = <your binding here>`

The button binding used to activate the move plugin. Default: `<super> BTN_LEFT`

2. `enable_snap = 0/1`

Enable snapping the currently moved window to an edge of the screen. Default: `1`

3. `snap_threshold = N`

The amount of pixels from the edge of the screen for which aero-snap gets triggered. Default: `10`

4. `enable_snap_off = 0/1`

Setting this to 0 disables moving a window after it has been snapped to a slot. Default: `1`

5. `snap_off_threshold = N`

Has effect only with `enable_snap_off = 1`. When attempting to move a snapped window, this option requires
the user to move at least `N` pixels before the window actually moves. Default: `0`

## `[resize]`
Provides a binding to start an interactive resize from any part of the window (not just edges).

1. `activate = <button binding>`

The button binding to start the interactive resize. Default: `<super> <shift> BTN_LEFT`

## `[vswitch]`

Switch workspaces in a grid.

1. Bindings and default values:
```
binding_down = <super> KEY_DOWN
binding_left = <super> KEY_LEFT                                                                                                                   
binding_right = <super> KEY_RIGHT
binding_up = <super> KEY_UP
binding_win_down = <super> <shift> KEY_DOWN
binding_win_left = <super> <shift> KEY_LEFT
binding_win_right = <super> <shift> KEY_RIGHT
binding_win_up = <super> <shift> KEY_UP
```

The first group of bindings just change the workspace in the indicated direction, and don't do anything if there is no neighbouring workspace in the given direction.

The second group (`binding_win_*`) change the workspace in the indicated direction, but also move the currently focused window to the new workspace.

2. `duration = msec`

The duration of the workspace switching animation. Default: `duration = 300`

TODO: add `fast-switch`, `grid`