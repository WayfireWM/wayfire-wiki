First **identify which component causes the bug**. It can be:
1. A plugin - if the problem happens while using a plugin or it doesn't happen when a plugin is disabled
2. Wayfire core - when the bug is not related to a plugin
2. Wlroots - Doesn't happen very often, but if the bug is connected to some application that is misbehaving in wayfire, you can also try to see if this app works in Sway or Rootston (the example wlroots compositor). If the bug is present there, too, then please tell so in the issue.

Another thing to bear in mind: If you have tried wayfire awhile ago (before August 2018 actually) you are very likely to have an outdated config file. If this is the case, update it using the new example. Otherwise many of the options may not work or some old plugin might crash the compositor.

**Important**: If the bug is actually a crash, please send me a stack trace. You can either:
1. Generate a core dump and send me the backtrace
or
2. Run wayfire nested (e.g under another wayland compositor or in X11) and use gdb
or
3. Compile with full debugging support and then capture the log (which will have a backtrace):
```
meson debugbuild --prefix=/usr --buildtype=debug -Db_sanitize=address,undefined
ninja -C debugbuild && sudo ninja -C debugbuild install

wayfire &> log.txt
```

The last command will create a file `log.txt` in the current directory, containing the debug logs and the backtrace.