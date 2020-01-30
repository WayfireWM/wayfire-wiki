## Run xwayland apps as root

This is a small wrapper script that uses `xhost` and `sudo` to launch x11 clients as root under xwayland. Save to a file, make executable and use in place of sudo to run an x11 client with privileges in wayfire.

```
#!/bin/bash
# small script to enable root access to x-windows system

# enable root access
xhost +SI:localuser:root

sudo -E $@

# disable root access after application terminates
xhost -SI:localuser:root
```

## Wine
If you are having trouble with wine applications, such as input not responding, tearing windows, or buggy mouse behavior in some fullscreen games check the following:
- Make sure xwayland is enabled in wayfire meson configure output and in wayfire.ini [core] xwayland = 1
- In winecfg in the Graphics tab, enable 'Automatically capture mouse in full screen mode', disable 'Allow the window manager to decorate the windows', disable 'Allow the window manager to control the windows' and enable 'Emulate a virtual desktop'

## Screensavers
The Idle plugin offers a built in screensaver for wayfire. It has options to choose either DPMS or screensaver timeout. If the cube plugin is enabled, the Idle screensaver timeout will rotate the cube based on settings found in the Idle plugin. Otherwise, the screen will just become black on timeout. There is also [swayidle](https://github.com/swaywm/swayidle) which can be used in conjunction with a [special version of xscreensaver](https://github.com/soreau/xscreensaver). It is recommended to install this version of xscreensaver to a nonstandard prefix because it will not work correctly with X. To use it, make two entries in the Autostart plugin like so:
```
a2 = /opt/xscreensaver/bin/xscreensaver -nosplash
a3 = swayidle timeout 60 '/opt/xscreensaver/bin/xscreensaver-command -activate' resume '/opt/xscreensaver/bin/xscreensaver-command -deactivate'
```
Change the prefix accordingly. The first will start the daemon and the second will activate the screensaver after 60 seconds of inactivity. You may change this value to your liking but the timeout specified must be less than that specified in xscreensaver settings via xscreensaver-demo. Note that swayidle timeout is in seconds and xscreensaver timeout is in minutes.