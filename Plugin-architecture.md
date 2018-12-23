## Architecture
In wayfire, each output is independent of the others and runs its own set of plugin instances. This for example lets you watch a video on a second monitor and use Expo/Cube/whatever on your main monitor without interrupting the video.

## Interaction with the core
Most plugins interact with core in one of the following ways:
1. Through a key/button/touch binding
2. Responding to/emitting a signal
3. Attaching a hook to the rendering loop.
4. Attaching a view transformer

### Bindings
Bindings are actually callbacks executed when the user presses a key combination, a specific button or touches the screen.
These are generally created during the `init()` phase. A plugin can read the configuration options(the config parameter) and add the according bindings. This happens with the `output->add_{key,button,touch,gesture,activator, axis}()` APIs.

### Signals
Signals are events generated either by the core or other plugins, for example when a window has been created/destroyed or an output was resized. The event is accompanied with a pointer to a signal_data_t, which should be casted to the appropriate derived class. Each plugin can emit signals and add/remove listeners for signals using the `output->{emit,connect,disconnect}_signal()` APIs. Some signals are also provided by the core itself, such as `output-added` or `output-removed`.

### Hooks
There are two types of hooks - render hooks and effect hooks.

Render hooks are used to override the default renderer and thus allow plugins like Cube and Expo to draw the scene in any way they want to.

Effect hooks are a way to execute certain actions at different stages of the render loop. `pre` hooks for example are executed right before starting to repaint the current frame, `overlay` ones happen after the scene is rendered, `post` hooks happen after the buffers were swapped. These are most useful when creating an animation.

### View transformers
Those are the cornerstone of the various window effects. A view transformer takes the view texture, and renders it to another texture or to the screen. It has complete freedom in how to draw the view, how it can modify the view's visible size, etc. For example, the fire transformer draws a fire over the view, others may rotate it, etc. The whole motivation for transformers comes from the fact that in this way, a plugin implementing its own transformer has to worry less about side effects, because each transformer is like a "black box" in a sense it just gets a texture and returns another one.

## Writing a plugin
Most of the functionality of Wayfire is implemented as plugins. The easiest way to write a plugin is to fork this repo and create a new file in `plugins/single_plugins/<your-plugin.cpp>`, and add it in the `CMakeLists.txt` in the same directory. To avoid writing boilerplate code, you can copy the command plugin and erase all functions except the init() and newInstance().

For each output, wayfire will call the newInstance() function. It must return a bare pointer to a new wayfire_plugin_t - the base class of all plugins. The returned pointer must point to a valid instance of the plugin which will be used on the current output. The base class is defined in `plugin.hpp` in the `src/api/` folder. There you can also find definitions for most of the callbacks.

To initialize the plugin, the core will call the init() function, passing also the configuration options. Apart from setting up bindings, signals and/or renderer, the init function must firstly initialize its grab_interface, specifying the its name and abilities mask. For more information, check the source code of the plugins. Don't hesitate to ask questions in Gitter:[![https://gitter.im/Wayfire-WM/Lobby](https://badges.gitter.im/Wayfire-WM/Lobby.svg)](https://gitter.im/Wayfire-WM/Lobby?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge) or in #wayfire at freenode.net