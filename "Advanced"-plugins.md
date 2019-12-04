## `[simple-tile]`

The simple-tile plugin provides some tiling features in Wayfire, inspired by i3. The plugin is meant to contain only the basics. If you want something fancier, you're welcome to build your own tiling WM as a Wayfire plugin.

**simple-tile requires matcher plugin!**

simple-tile has several options:

1. `tile_by_default = any`

Controls which windows are added to the tiling grid by default. A matcher expression.

2. `button_move = <super> BTN_LEFT`

With this button, you can drag and drop tiled windows to reorder them and to change the tiling direction (for ex. create new vertical or horizontal splits).

3. `button_resize = <super> BTN_RIGHT`

With this button, you can drag a tiled window to resize it. Adjacent windows will also be resized.

4. `key_toggle = <super> KEY_T`

Toggle tiling enabled for the currently focused window, that is:
If the window is already tiled, it will be untiled (it becomes floating)
If the window isn't tiled, it will be added to the tiling grid.

5. `key_toggle_fullscreen = <super> KEY_M`

Toggle the currently focused tiled window fullscreen state.

6.
```
key_focus_left  = <super> KEY_H
key_focus_right = <super> KEY_L
key_focus_above = <super> KEY_K
key_focus_below = <super> KEY_J
```
If a tiled window is currently focused, focus the next tiled window in the given direction.

7. `keep_fullscreen_on_adjacent = 1`

Controls what happens when the `key_focus_*` bindings are executed but the currently focused tiled view is fullscreen. If `keep_fullscreen_on_adjacent` is `1`, then the next focused window will also get fullscreen. Otherwise all windows will get unfullscreened.