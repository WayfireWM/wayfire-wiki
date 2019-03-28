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

## Native webcam with gst-launch-1.0 (gstreamer)
Use the following command to show /dev/video0 in a native window. Note that glimagesink must be available.
```
gst-launch-1.0 -v v4l2src device=/dev/video0 ! glimagesink
```