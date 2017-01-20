# Window Main Loop

Every Gosu game contains a subclass of `Gosu::Window` which overrides all the callback methods it is interested in. When you call `window.show()`, Gosu enters this loop:

[[main_loop.png]]

The [[Ruby Tutorial]] and [[C++ Tutorial]] explain how to use these callbacks.

Some more details:

  * `draw` is _very_ flexible. The usual flow is shown above, but `draw` might be called if the OS decides to redraw the window, or calls to `draw` might be dropped if the window is hidden, etc. Your game logic should never rely on `draw` being called in perfect lockstep with `update`, even if that is the normal case.
  * _You cannot know_ which callback will be called first. `initialize` (or the constructor in C++) _must_ set up a valid state that will work no matter if `update` or `draw` will be called first.
  * You cannot rely on `Gosu::TextInput::text()` being the same between `update` and `draw`.
  * Nothing in Gosu is multi-threaded, and no callback is ever interrupted for another.

# Performance Degradation

If you want to make sure that your game works on slow computers, there are two solutions.

## Discrete Logic

First, you can write your game logic in the style of the tutorial game. In every logical frame (`update`), the player moves by a fixed amount of pixels. This is usually the easiest way to write code.

If the system is too slow to run your game at 60 FPS, movement will appear *slower* than intended. You should try to stay near the 60 FPS target by reducing visual effects when `Gosu::fps()` drops below 60, and you can use the special callback `Gosu::Window::needs_redraw` ( `needs_redraw?` in Ruby) to skip calls to `Window::draw` (e.g. every second frame).

## Delta-Time Physics

You can call `Gosu::milliseconds()` in every `update` call, then update your game state based on the time difference between two calls (delta time, dt). This allows physics to be written in a style that matches school physics (position += speed*dt), and ensures that everything will move at the same speed regardless of the game's current framerate. However, it usually requires more code.

Gosu supports both styles of programming.
