## `Run xwayland apps as root`

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
## `Java applications in xwayland`
The following needs to be set for certain java applications to display correctly when run in wayfire.
```
_JAVA_AWT_WM_NONREPARENTING=1
```