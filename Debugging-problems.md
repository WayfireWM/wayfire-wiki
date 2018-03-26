First **identify which component causes the bug**. It can be:
1. A plugin - if the problem happens while using a plugin or it doesn't happen when a plugin is disabled
2. Libweston - If a program crashes or doesn't show up at all, try using it in Weston. If the bug is present also there, then it is quite possible that it is a bug in libweston, although this doesn't happen very often. To make sure this is the case, you can also run it with "stock" weston(without my patches).
3. Otherwise it is a general wayfire bug

**Important**: If the bug is actually a crash, recompile with debugging enabled:
```
cd build
cmake ../ -DCMAKE_BUILD_TYPE=Debug -DCMAKE_INSTALL_PREFIX=/usr -DUSE_GLES32=False
make && sudo make install
```

Then, when starting wayfire as follows: `/<path_to_wayfire_binary>/wayfire log.txt`. This will generate a log file named `log.txt`. Reproduce the bug and send the log file.