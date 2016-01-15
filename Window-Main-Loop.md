# Window Main Loop

Usually, you create a subclass of `Gosu::Window` and override the parts that you need. Then, you create an instance of this class and call `show` on it. What happens then is this:

[[main_loop.png]]

Examples of what you can do in these events are shown on the [[Ruby Tutorial]] and [[C++ Tutorial]] pages.

There are details that you may be interested in:

  * `draw` is _very_ flexible. The usual flow is shown above, but `draw` is generally called whenever the OS wants to redraw the window. This may be directly upon calling `show`, or even twice between `update` calls, or not at all during a frame if the window is obscured.
  * It follows that _you cannot know_ at all which callback will be called first. `initialize` (or the constructor in C++) _must_ set up a valid state. If update contains `if player == nil then respawn()`, then `initialize` should also contain `respawn()`. You can just call `update()` as the last call in `initialize`/the constructor if it helps.
  * Because `draw` is so flexible, it should really only render the current state of things and not change anything, not even advance animations. If you write `draw` in a functional, read-only style then you are safe.
  * In `update`, you may want to check `button_down?` (or `input().down()` in C++) to poll the most recent state of a button. Because the input events should logically be fired _before_ `button_down?` is updated, it follows that they all have to happen before `update`. This sadly means that you cannot directly react to the very latest button events in `draw`; an `update` call will always happen inbetween.
  * Because `TextInput` may call back into the game (`filter` callback), it is not buffered and can happen at any place during the loop. You cannot rely on `text()` being the same between `update` and `draw` either.
  * Don't be scared though, nothing in Gosu is multi-threaded and no callback is ever interrupted for another!

# Performance Degradation

What if the system is too slow to run the game at its intended framerate? There are two major solutions.

## Discrete Logic

First, you can write your game logic in the style of the example games. In every logical frame (`update`), the player moves by a fixed amount of pixels forward. Animations also advance with every logical frame etc. This will result in rather integer-based, discrete game code. The CPU may like it too, especially in Ruby or on ARM processors.

However, if the system is too slow for your game, you are very limited in your options:

  * You can spawn less particles or reduce eye candy in other ways. This only works if there is much eye candy to begin with.
  * You can drop frames by returning false in the `needs_redraw? `/`needsRedraw()` callback. You have to be careful not to skip too many frames in a row though.

## Delta-Time Physics

You can also write your games by checking `Gosu::milliseconds()` between one `update` call and another, then update your game state based on the time different (delta time, dt). This allows physics to be written in a style that matches school physics (position += speed*dt) and is very common when working with physics engines.

This style naturally works better with a low framerate, but may need more up-front thinking, and the calculations may be slower in general because floating-point values are a more natural fit here.

This is definitely a by-case choice and Gosu tries to support both styles of programming.