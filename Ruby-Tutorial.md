# Ruby Tutorial

## Translations

For links to translations of this tutorial (Traditional Chinese, Spanish, French) see the [[Home]] page.

## Source code

This and other example games can be found in the [gosu-examples](https://github.com/gosu/gosu-examples) Ruby gem.

## Down to Business
### 1. Overriding Window's callbacks

The easiest way to create a complete Gosu application is to write a new class that derives from Gosu::Window (see the reference for a complete description of its interface). Here's how a minimal GameWindow class might look like:

```ruby
require 'gosu'

class GameWindow < Gosu::Window
  def initialize
    super 640, 480
    self.caption = "Gosu Tutorial Game"
  end
  
  def update
  end
  
  def draw
  end
end

window = GameWindow.new
window.show
```
The constructor initializes the `Gosu::Window` base class. The parameters shown here create a 640x480 pixels large window. It also sets the caption of the window, which is displayed in its title bar. You can create a fullscreen window by passing `:fullscreen => true` after the width and height.

`update()` and `draw()` are overrides of `Gosu::Window`'s member functions. `update()` is called 60 times per second (by default) and should contain the main game logic: move objects, handle collisions, etc.

`draw()` is called afterwards and whenever the window needs redrawing for other reasons, and may also be skipped every other time if the FPS go too low. It should contain the code to redraw the whole screen, but no updates to the game's state.

Then follows the main program. We create a window and call its `show()` member function, which does not return until the window has been closed by the user or by calling `close()`.

A diagram of the main loop is shown on the [[Window Main Loop]] page.

### 2. Using Images

```ruby
require 'gosu'

class GameWindow < Gosu::Window
  def initialize
    super 640, 480
    self.caption = "Gosu Tutorial Game"
    
    @background_image = Gosu::Image.new("media/Space.png", :tileable => true)
  end
  
  def update
  end
  
  def draw
    @background_image.draw(0, 0, 0)
  end
end

window = GameWindow.new
window.show
```

`Gosu::Image#initialize` takes two arguments, the filename and an (optional) options hash. Here we set `:tileable` to `true`, see [[Basic Concepts]] for an explanation. Basically, you should use `:tileable => true` for background images and map tiles.

As mentioned in the last lesson, the window's `draw()` member function is the place to draw everything, so we override it and draw our background image.

The image is drawn at (0;0) - the third argument is the Z position; again, see [[Basic Concepts]].

#### 2.1 Player & movement

Here comes a simple player class:

```ruby
class Player
  def initialize
    @image = Gosu::Image.new("media/Starfighter.bmp")
    @x = @y = @vel_x = @vel_y = @angle = 0.0
    @score = 0
  end

  def warp(x, y)
    @x, @y = x, y
  end
  
  def turn_left
    @angle -= 4.5
  end
  
  def turn_right
    @angle += 4.5
  end
  
  def accelerate
    @vel_x += Gosu::offset_x(@angle, 0.5)
    @vel_y += Gosu::offset_y(@angle, 0.5)
  end
  
  def move
    @x += @vel_x
    @y += @vel_y
    @x %= 640
    @y %= 480
    
    @vel_x *= 0.95
    @vel_y *= 0.95
  end

  def draw
    @image.draw_rot(@x, @y, 1, @angle)
  end
end
```

There are a couple of things to say about this:

![Angles in Gosu][FIG:angles]

  * Player#accelerate makes use of the `offset_x`/`offset_y` functions. They are similar to what some people use sin/cos for: For example, if something moved 100 pixels at an angle of 30°, it would move a distance of `offset_x(30, 100)` pixels horizontally and `offset_y(30, 100)` pixels vertically.
  * When loading BMP files, Gosu replaces `#ff00ff` (fuchsia/magenta; that really ugly pink) with transparent pixels.
  * Note that `draw_rot` puts the *center* of the image at (x; y) - *not* the upper left corner as draw does! This can be controlled by the `center_x`/`center_y` arguments if you want.
  * The player is drawn at z=1, i.e. over the background (obviously). We'll replace these magic numbers with something better later.
  * Also, see the [RDoc][] for all drawing methods and arguments.

#### 2.2 Using our Player class inside Window

```ruby
class GameWindow < Gosu::Window
  def initialize
    super 640, 480
    self.caption = "Gosu Tutorial Game"

    @background_image = Gosu::Image.new("media/Space.png", :tileable => true)

    @player = Player.new
    @player.warp(320, 240)
  end

  def update
    if Gosu::button_down? Gosu::KbLeft or Gosu::button_down? Gosu::GpLeft then
      @player.turn_left
    end
    if Gosu::button_down? Gosu::KbRight or Gosu::button_down? Gosu::GpRight then
      @player.turn_right
    end
    if Gosu::button_down? Gosu::KbUp or Gosu::button_down? Gosu::GpButton0 then
      @player.accelerate
    end
    @player.move
  end

  def draw
    @player.draw
    @background_image.draw(0, 0, 0);
  end

  def button_down(id)
    if id == Gosu::KbEscape
      close
    end
  end
end

window = GameWindow.new
window.show
```

As you can see, we have introduced keyboard and gamepad input!
Similar to `update()` and `draw()`, `Gosu::Window` provides two member functions `button_down(id)` and `button_up(id)` which can be overridden, and do nothing by default. We do this here to close the window when the user presses ESC. (For a list of predefined button constants, see the [RDoc][]).
While getting feedback on pushed buttons via `button_down` is suitable for one-time events such as UI interaction, jumping or typing, it is not place to implement actions that span several frames - for example, moving by holding buttons down. This is where the `update()` member function comes into play, which calls the player's movement methods depending on which buttons are held down during this frame. If you run this lesson's code, you should be able to fly around!

### 3. Simple animations

First, we are going to get rid of the magic numbers for Z positions from now on by replacing them with the following constants:

```ruby
module ZOrder
  Background, Stars, Player, UI = *0..3
end
```

What is an animation? A sequence of images - so we'll use Ruby's built in `Array` to store them. (Feel free to write utility classes for animations in your game.)

Let's introduce the stars which are the central object of this lesson. Stars appear out of nowhere at a random place on the screen and live their animated lives until the player collects them. The definition of the Star class is rather simple:

```ruby
class Star
  attr_reader :x, :y

  def initialize(animation)
    @animation = animation
    @color = Gosu::Color.new(0xff_000000)
    @color.red = rand(256 - 40) + 40
    @color.green = rand(256 - 40) + 40
    @color.blue = rand(256 - 40) + 40
    @x = rand * 640
    @y = rand * 480
  end

  def draw  
    img = @animation[Gosu::milliseconds / 100 % @animation.size];
    img.draw(@x - img.width / 2.0, @y - img.height / 2.0,
        ZOrder::Stars, 1, 1, @color, :add)
  end
end
```

Since we don't want each and every star to load the animation again, we can't do that in its constructor, but rather pass it in from somewhere else. (The Window will load the animation in about three paragraphs.)

To show a different frame of the stars' animation every 100 milliseconds, the time returned by `Gosu::milliseconds` is divided by 100 and then modulo-ed down to the number of frames. This very image is then additively drawn, centered at the star's position and modulated by a random colour we generated in the constructor.

Now let's add easy code to the player to collect away stars from an array:

```ruby
class Player
  ...
  def score
    @score
  end

  def collect_stars(stars)
    if stars.reject! {|star| Gosu::distance(@x, @y, star.x, star.y) < 35 } then
      @score += 1
    end
  end
end
```

Now let's extend Window to load the animation, spawn new stars, have the player collect them and draw the remaining ones:

```ruby
...
class Window < Gosu::Window
  def initialize
    super 640, 480
    self.caption = "Gosu Tutorial Game"

    @background_image = Gosu::Image.new("media/Space.png", :tileable => true)

    @player = Player.new
    @player.warp(320, 240)

    @star_anim = Gosu::Image::load_tiles("media/Star.png", 25, 25)
    @stars = Array.new
  end

  def update
    ...
    @player.move
    @player.collect_stars(@stars)

    if rand(100) < 4 and @stars.size < 25 then
      @stars.push(Star.new(@star_anim))
    end
  end

  def draw
    @background_image.draw(0, 0, ZOrder::Background)
    @player.draw
    @stars.each { |star| star.draw }
  end
  ...
```

Done! You can now collect stars.

### 4. Text and sound

Finally, we want to draw the current score using a bitmap font and play a 'beep' sound every time the player collects a star. The Window will handle the text part, loading a font 20 pixels high:

```ruby
class Window < Gosu::Window
  def initialize
    ...
    @font = Gosu::Font.new(20)
  end

  ...

  def draw
    @background_image.draw(0, 0, ZOrder::Background)
    @player.draw
    @stars.each { |star| star.draw }
    @font.draw("Score: #{@player.score}", 10, 10, ZOrder::UI, 1.0, 1.0, 0xff_ffff00)
  end
end
```

What's left for the player? Right: A counter for the score, loading the sound and playing it.

```ruby
class Player
  attr_reader :score

  def initialize
    @image = Gosu::Image.new("media/Starfighter.bmp")
    @beep = Gosu::Sample.new("media/Beep.wav")
    @x = @y = @vel_x = @vel_y = @angle = 0.0
    @score = 0
  end

  ...

  def collect_stars(stars)
    stars.reject! do |star|
      if Gosu::distance(@x, @y, star.x, star.y) < 35 then
        @score += 10
        @beep.play
        true
      else
        false
      end
    end
  end
end
```

As you can see, loading and playing sound effects couldn't be easier! See the [RDoc][] for more powerful ways of playing back sounds - fiddle around with volume, position and pitch.

That's it! Everything else is up to your imagination. If you want to see examples of other types of games being written in Ruby/Gosu, take a look at the great projects on the [Gosu Showcase board][boards.showcase].

[boards.showcase]: https://www.libgosu.org/cgi-bin/mwf/board_show.pl?bid=2 "Gosu Showcase Board"
[RDoc]: https://www.libgosu.org/rdoc "Gosu RDoc Reference Documentation"
[FIG:angles]: https://raw.githubusercontent.com/wiki/jlnr/gosu/angles2.png