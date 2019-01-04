
<b> This page is incomplete. For a complete description of plugins, see the default config file, wayfire.ini.default </b>

# Wayfire configuration

Wayfire is managed through a config file, typically located in `~/.config/wayfire.ini`. The location can be overriden using the `-c <config file>` argument when staring Wayfire.

Probably the easiest way to edit the configuration options is the WIP [Wayfire config manager (WCM)](https://github.com/WayfireWM/wcm). However, it is still missing many important options (like output configuration and the `command` plugin), so for the time being you most probably want to edit the config file directly.

## Config file structure
The configuration file follows a simple `ini` file format. It is divided into sections, which consist of multiple options, for ex.

```
[example-section]
example_option1 = value1
example_option2 = value2
....
```

There are several types of values:

1. ### Integer, double, string
Examples: `option = 1.0`, `option = your string`

2. ### Colors
They are represented by of four floating point numbers in RGBA format. <br/>
Example: `option = 0.5 0.5 0.5 1.0` means a fully opaque grey color.

3. ### Key- and buttonbindings
These represent a combination of modifier + key/button.<br/>
Modifiers can be `<shift>`, `<ctrl>`, `<alt>` and/or `<super>`. <br/>
Keys and buttons have names as defined in `/usr/include/linux/input-event-codes.h`. <br/>

Examples: `option = <super> <shift> KEY_F`, `option = <ctrl> BTN_RIGHT`

4. ### Touch and axis bindings
These are represented via a modifier combination, for ex. `option = <alt>` means alt+scroll for an axis binding.

5. ### Touch gesture bindings
Represent a touchscreen gesture (in the future also touchpad support is planned)

Examples:
```
option = swipe 3 up        #swipe up with 3 fingers <br/>
option = pinch 3 in        # pinch in(can also be set with out) with 3 fingers <br/>
option = edge-swipe 4 left # swipe left with 4 fingers, starting from the edge of the screen <br/>
```
6. ### Activator bindings
Activator bindings combine multiple key/button/touch bindings, so that a single action can be triggered from multiple bindings. Example: `toggle = <alt> BTN_EXTRA | pinch out 3 | <alt> KEY_E`

# Currently available options

The documentation for individual options has been split into multiple pages:

TODO: add pages

