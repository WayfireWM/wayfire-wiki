To create a functional desktop, more than a compositor is needed. In this page I've listed some useful programs that belong to a DE and I've described how I use them with Wayfire. Many of them require the `command` plugin, which is enabled by default.

# Screenshots, screen recording and screen casting

As a wlroots-based compositor Wayfire supports `wlr-screencopy-v1` and `wlr-export-dmabuf-v1` protocols, so any programs that use them should work. Here are some examples:

1. ### [grim](https://github.com/emersion/grim)

Grim lets you create screenshots. It can be bound to a keybinding, for ex. with the following in the `[command]` config section of Wayfire:

```
binding_screenshot = <super> KEY_S
command_screenshot = grim $HOME/Pictures/screenshot-$(date "+%Y-%m-%d-%H:%M:%S").png                                                                                                            
binding_slurp = <super> <shift> KEY_S
command_slurp = slurp | grim -g - ~/Pictures/slurped.png
```

Now you can take a screenshot with `<super> KEY_S` and it will be saved to `~/Pictures/`. The second binding demonstrates how to use grim together with slurp, for more info see grim's [README.md](https://github.com/emersion/grim) 

2. ### [wlstream](https://github.com/atomnuker/wlstream)

wlstream is a screen recorder using `ffmpeg >= 4.0`. It also supports streaming with audio (for example to twitch, youtube ...). Here's an example command for streaming to twitch:

```wlstream 17 vaapi /dev/dri/renderD128 libx264 nv12 12 rtmp://live-prg.twitch.tv/app/live_<your tokens here>```

Change the `17` to the output ID on your system (`wlstream` will print the info for you).
You may have to adjust the `/dev/dri/renderD` node to what is present on your system. You also might need to adjust the formats used by `wlstream` (the `libx264`, `nv12` and `12` parameters, if those aren't supported by your system).

3. ### [wf-recorder](https://github.com/ammen99/wf-recorder)

wf-recorder is a very simple screen recorder. In contrast to wlstream it doesn't support network streaming or audio, but it should be much more portable and easy to use. Follow the installation instructions in the readme, run `wf-recorder` and press `Ctrl-C` to stop recording.

# Sound volume control

1. ### amixer

More often than not we want to be able to control the sound volume with a keybinding. Set the following in the `[command]` section:

```
binding_volup   = KEY_VOLUMEUP | BTN_EXTRA
command_volup   = amixer -q sset Master 5%+
binding_voldown = KEY_VOLUMEDOWN | BTN_SIDE
command_voldown = amixer -q sset Master 5%-
binding_mute    = KEY_MUTE
command_mute    = amixer -q sset Master toggle                                   
```

I have also set up the `BTN_EXTRA`/`BTN_SIDE` buttons to also control sound volume, you can adjust bindings in any way you want.

2. ### [wf-sound-control](https://github.com/WayfireWM/wf-sound-control)

If you want a GUI indication for sound volume, there is a WIP here: https://github.com/WayfireWM/wf-sound-control. It supports increase/decrease of volume, also setting volume with the mouse, but doesn't support mute. How to use:
```
binding_volup   = KEY_VOLUMEUP | BTN_EXTRA
command_volup   = wf-sound-control inc 5
binding_voldown = KEY_VOLUMEDOWN | BTN_SIDE
command_voldown = wf-sound-control dec 5
```

3. ### Pulseaudio

```
binding_volup   = KEY_VOLUMEUP | BTN_EXTRA
command_volup   = pactl set-sink-volume 0 +5%
binding_voldown = KEY_VOLUMEDOWN | BTN_SIDE
command_voldown = pactl set-sink-volume 0 -5%
```

#  Set screen brightness

### [Light](https://github.com/haikarainen/light)
Light is a console program to control brightness. You can of course use any alternative programs, there are many, it is just that this one works best for me. It is useful to set this as a keybinding - go to the `[command]` section and add the following entries:

```
binding_brightness_down = KEY_BRIGHTNESSDOWN
command_brightness_down = sudo light -p -U 5
binding_brightness_up = KEY_BRIGHTNESSUP                                         
command_brightness_up = sudo light -p -A 5
```

Here I have installed `light` to `/usr/bin` and have configured `sudo` to not ask password for `light`. An alternative would be to properly manage brightness permissions. After it, you can use the brightness up/down keys on your keyboard to control brightness. Of course you can change the bindings to some other keys.





