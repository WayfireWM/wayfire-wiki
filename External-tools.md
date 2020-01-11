To create a functional desktop, more than a compositor is needed. In this page I've listed some useful programs that belong to a DE and I've described how I use them with Wayfire. Many of them require the `command` plugin, which is enabled by default.

## Screenshots, screen recording and screen casting

As a wlroots-based compositor Wayfire supports `wlr-screencopy-v1` and `wlr-export-dmabuf-v1` protocols, so any programs that use them should work. Here are some examples:

1. ### [grim](https://github.com/emersion/grim)

Grim lets you create screenshots. It can be bound to a keybinding, for ex. with the following in the `[command]` config section of Wayfire:

```
binding_screenshot = <super> KEY_S
command_screenshot = grim $HOME/Pictures/screenshot-$(date "+%Y-%m-%d-%H:%M:%S").png
binding_slurp = <super> <shift> KEY_S
command_slurp = slurp | grim -g - ~/Pictures/slurped.png
```

Now you can take a screenshot with `<super> KEY_S` and it will be saved to `~/Pictures/`. The second binding demonstrates how to use grim together with slurp to interactively select a subregion of the screen to screenshot, for more info see grim's [README.md](https://github.com/emersion/grim)

2. ### [wf-recorder](https://github.com/ammen99/wf-recorder)

wf-recorder's goal is to be a very simple recording client, while working out-of-the-box on as many setups as possible. Follow the installation instructions in the readme, run `wf-recorder` and press `Ctrl-C` to stop recording.

3. ### [wlstream](https://github.com/atomnuker/wlstream)

wlstream is a bit more complex screen recorder using `ffmpeg >= 4.0`, however it can be a bit difficult to use and might not work on all setups. It supports screen recording, and streaming with audio (for example to twitch, youtube ...). Here's an example command for streaming to twitch:

```
wlstream 17 vaapi /dev/dri/renderD128 libx264 nv12 12 rtmp://live-prg.twitch.tv/app/live_<your tokens here>
```

Change the `17` to the output ID on your system (`wlstream` will print the info for you).
You may have to adjust the `/dev/dri/renderD` node to what is present on your system. You also might need to adjust the formats used by `wlstream` (the `libx264`, `nv12` and `12` parameters, if those aren't supported by your system).

## Sound volume control

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

##  Set screen brightness

### [Light](https://github.com/haikarainen/light)
Light is a console program to control brightness. You can of course use any alternative programs, there are many, it is just that this one works best for me. It is useful to set this as a keybinding - go to the `[command]` section and add the following entries:

```
binding_brightness_down = KEY_BRIGHTNESSDOWN
command_brightness_down = sudo light -p -U 5
binding_brightness_up = KEY_BRIGHTNESSUP
command_brightness_up = sudo light -p -A 5
```

Here I have installed `light` to `/usr/bin` and have configured `sudo` to not ask password for `light`. An alternative would be to properly manage brightness permissions. After it, you can use the brightness up/down keys on your keyboard to control brightness. Of course you can change the bindings to some other keys.

### [brightnessctl](https://github.com/Hummer12007/brightnessctl)
brightnessctl is an alternative to light that functions the same way.

The different is that [brightness
permissions](https://github.com/Hummer12007/brightnessctl#permissions) are managed out
of the box, so you normally do not have to deal with `sudo`.

Put the following entries to the `[command]` section in `wayfire.ini`.

```
binding_brightness_down = KEY_BRIGHTNESSDOWN
command_brightness_down = brightnessctl set 5%-
binding_brightness_up = KEY_BRIGHTNESSUP
command_brightness_up = brightnessctl set +5%

```

Check out `man brightnessctl` for other uses of the program.

## Notifications

### [Mako](https://github.com/emersion/mako)

Setting this up is really simple, just run `mako` in the `[autostart]` section:

```
[autostart]
mako = /usr/bin/mako
...
```
Of course, adjust the `/usr/bin` part to where the `mako` binary on you system is.

## Screen color temperature (gamma correction)

### [Redshift](https://github.com/jonls/redshift/pull/663)

Redshift-like functionality requires special protocols, support for those still hasn't been merged in upstream `redshfit`, so use the version from the link above. Setup is similar to mako:

```
[autostart]
redshift = redshift -m wayland # -m tells it to use the wayland backend
...
```
