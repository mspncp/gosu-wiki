# C++ Tutorial

## Source Code

The code for the complete tutorial game, along with all required media files, can be found this git repository (`examples/Tutorial/Tutorial.cpp`). To run the game, setup a new project as seen in [[Getting Started on OS X]], [[Getting Started on Windows]], or [[Getting Started on Linux]], and use `Tutorial.cpp` as the only source file. Make sure that the compiled binary can find the images and sound effects used in this game (`examples/media`).

## The Tutorial

### 1. Overriding Window's callbacks

Every Gosu application starts with a class that derives from [Gosu::Window](https://www.libgosu.org/cpp/class_gosu_1_1_window.html). A minimal window class looks like this:

```cpp
// The complete Gosu library.
#include <Gosu/Gosu.hpp>
// Makes life a little easier when compiling the game in Visual C++.
#include <Gosu/AutoLink.hpp>

#include <cmath>
#include <cstdlib>
#include <list>
#include <memory>
#include <string>
#include <vector>
      
class GameWindow : public Gosu::Window
{
public:
    GameWindow()
    : Window(640, 480)
    {
        set_caption("Gosu Tutorial Game");
    }

    void update() override
    {
        // ...
    }

    void draw() override
    {
        // ...
    }
};

int main()
{
    GameWindow window;
    window.show();
}
```

The constructor initializes the `Gosu::Window` base class. The parameters shown here create a 640x480 pixels large window, then it changes the caption shown in the window's title bar. Note that Gosu accepts and returns `std::string` containing UTF-8 throughout its API.

`update()` and `draw()` are overrides of `Gosu::Window`'s member functions. `update()` is called 60 times per second by default, and should contain the main game logic, such as moving objects around, or testing for collisions.

`draw()` is usually called 60 times per second, but may be skipped for performance reasons. It should contain code to redraw the whole scene, but no game logic.

Then follows the main program. We create a window and call its `show()` member function, which does not return until the window has been closed by the user, or by calling `Gosu::Window::close()`.

A diagram of the main loop is shown on the [[Window Main Loop]] page.

### 2. Using Images

```cpp
class GameWindow : public Gosu::Window
{
    std::unique_ptr<Gosu::Image> background_image;

public:
    GameWindow()
    : Window(640, 480)
    {
        set_caption("Gosu Tutorial Game");

        std::string filename = Gosu::resource_prefix() + "media/Space.png";
        background_image.reset(new Gosu::Image(filename, Gosu::IF_TILEABLE));
    }

    void update() override
    {
        // ...
    }

    void draw() override
    {
        background_image->draw(0, 0, 0);
    }
};
```

(At this point, please download [Space.png](https://raw.githubusercontent.com/gosu/gosu/master/examples/media/Space.png) and ensure that your compiled binary can find it at `media/Space.png`.)

*Note:* `Gosu::Image` has no default constructor to prevent the creation of unusable 'zombie' images. You can use `std::unique_ptr`, `std::shared_ptr`, `std::optional`, or raw pointers if you need to delay the creation of an image.

`Gosu::Image`'s constructor takes two arguments, the filename of the image file and "image flags". Here we pass `IF_TILEABLE`, see [[Basic Concepts]] for an explanation. Basically, you should use this flag for map tiles and background images.

As mentioned in the last section, the Window's `draw()` member function is the place to draw everything, so this is where we draw the background image. The image is drawn at the position (0, 0) - the third image is the z position; see [[Basic Concepts]] for an explanation of Z ordering in Gosu.

#### 2.1. Player & Movement

Here comes a simple player class:

```cpp
class Player
{
    Gosu::Image image;
    Gosu::Sample beep;
    double pos_x, pos_y, vel_x, vel_y, angle;
    unsigned score;

public:
    Player()
    :   image(Gosu::resource_prefix() + "media/Starfighter.bmp")
    {
        pos_x = pos_y = vel_x = vel_y = angle = 0;
        score = 0;
    }

    void warp(double x, double y)
    {
        pos_x = x;
        pos_y = y;
    }

    void turn_left()
    {
        angle -= 4.5;
    }

    void turn_right()
    {
        angle += 4.5;
    }

    void accelerate()
    {
        vel_x += Gosu::offset_x(angle, 0.5);
        vel_y += Gosu::offset_y(angle, 0.5);
    }

    void move()
    {
        pos_x = Gosu::wrap(pos_x + vel_x, 0.0, 640.0);
        pos_y = Gosu::wrap(pos_y + vel_y, 0.0, 480.0);

        vel_x *= 0.95;
        vel_y *= 0.95;
    }

    void draw() const
    {
        image.draw_rot(pos_x, pos_y, 1, angle);
    }
};
```

(Please download [Starfighter.bmp](https://raw.githubusercontent.com/gosu/gosu/master/examples/media/Starfighter.bmp) and ensure that your compiled binary can find it at `media/starfighter.bmp`.)

There are a couple of things to note about this:

[[angles2.png|alt=Angles in Gosu]]

  * `Player::accelerate` makes use of the `offset_x`/`offset_y` functions. They are similar to the mathematical sin/cos functions: For example, if something moved 100 pixels per frame at an angle of 30°, it would move by `offset_x(30, 100)` pixels horizontally, and by `offset_y(30, 100)` pixels vertically each frame.
  * When loading BMP image files, Gosu replaces `#ff00ff` (fuchsia/magenta/'magic pink') with transparent pixels.
  * Note that `Image::draw_rot` puts the *center* of the image at `x, y` - *not* the upper left corner, as with `Image::draw`. Also, the player is drawn at `z = 1`, i.e. over the background. We'll replace this magic number with something better later. See [the C++ reference](https://www.libgosu.org/cpp/class_gosu_1_1_image.html) for the full list of arguments to `draw` and `draw_rot`.
  * `Gosu::wrap(what, min, max)` maps a value inside the *min..max* range. If the player leaves the screen on the left side, they will re-appear from the right side etc. If you want to disable this wraparound, use `Gosu::clamp(what, min, max)` instead.
  * The `Player` class loads the image straight in its initialiser list, unlike the Window which used a pointer.

#### 2.2. Integrating Player with the Window

```cpp
class GameWindow : public Gosu::Window
{
    std::unique_ptr<Gosu::Image> background_image;

    Player player;
        
public:
    GameWindow()
    : Window(640, 480), font(20)
    {
        set_caption("Gosu Tutorial Game");

        std::string filename = Gosu::resource_prefix() + "media/Space.png";
        background_image.reset(new Gosu::Image(filename, Gosu::IF_TILEABLE));

        player.warp(320, 240);
    }
    
    void update() override
    {
        if (Gosu::Input::down(Gosu::KB_LEFT) || Gosu::Input::down(Gosu::GP_LEFT)) {
            player.turn_left();
        }
        if (Gosu::Input::down(Gosu::KB_RIGHT) || Gosu::Input::down(Gosu::GP_RIGHT)) {
            player.turn_right();
        }
        if (Gosu::Input::down(Gosu::KB_UP) || Gosu::Input::down(Gosu::GP_BUTTON_0)) {
            player.accelerate();
        }
        player.move();
    }
    
    void draw()
    {
        player.draw();
        background_image->draw(0, 0, Z_BACKGROUND);
    }
    
    void button_down(Gosu::Button button) override
    {
        if (button == Gosu::KB_ESCAPE) {
           close();
        }
        else {
            Window::button_down(button);
        }
    }
};
```

Here we have introduced keyboard and gamepad input!

Similar to `update()` and `draw()`, `Gosu::Window` provides two virtual member functions `button_down(btn)` and `button_up(btn)` which can be overridden. The default implementation of `button_down` lets the user toggle between fullscreen and windowed mode with alt+enter (Windows, Linux) or cmd+F (macOS). Because we want to keep this default behaviour, we call `Window::button_down` if the user has not pressed anything that interests us.

In our implementation of `button_down`, we want to close the window when the user presses `Esc`. The list of button constants can be found in (the C++ reference)[https://www.libgosu.org/cpp/namespace_gosu.html#enum-members].

These two callbacks for pressed and released buttons are suitable for one-time events such as using an item. But they are not useful for actions that happen *while* a button is pressed — for example, moving the player. This is where the `update()` member function comes into play, which calls the player's movement, which in turn use `Gosu::Input::down`. This method will return `true` as long as a button is being held by the player.

If you run the code in this section, you should be able to fly around.

### 3. Simple animations

First, we are going to get rid of the magic numbers for Z positions from now on by replacing them with the following enumeration:

```cpp
enum ZOrder
{
    zBackground,
    zStars,
    zPlayer,
    zUI
};
```

What is an animation? A sequence of images. A simple Animation type might look like this:

    typedef std::vector<Gosu::Image> Animation;

For a real game, there is no way around writing some classes that fit the game's individual needs, but we'll get away with this solution for now.

Let's introduce the stars which are the central object of this lesson. Stars appear out of nowhere at a random place on the screen and live their animated lives until the player collects them. The definition of the Star class is rather simple:

```cpp
class Star
{
    Animation animation;
    Gosu::Color color;
    double posX, posY;

public:
    explicit Star(Animation animation)
    :   animation(animation)
    {
        color.setAlpha(255);
        double red = Gosu::random(40, 255);
        color.setRed(static_cast<Gosu::Color::Channel>(red));
        double green = Gosu::random(40, 255);
        color.setGreen(static_cast<Gosu::Color::Channel>(green));
        double blue = Gosu::random(40, 255);
        color.setBlue(static_cast<Gosu::Color::Channel>(blue));

        posX = Gosu::random(0, 640);
        posY = Gosu::random(0, 480);
    }

    double x() const { return posX; }
    double y() const { return posY; }

    void draw() const
    {
        const Gosu::Image& image =
            animation.at(Gosu::milliseconds() / 100 % animation.size());

        image.draw(posX - image.width() / 2.0, posY - image.height() / 2.0,
            zStars, 1, 1, color, Gosu::amAdd);
    }
};
```

Since we do not want each and every star to load the animation again, we cannot do that in its constructor, but rather pass it in from somewhere else. (The Window will load the animation in about three paragraphs.)

To show a different frame of the stars' animation every 100 milliseconds, the time returned by `Gosu::milliseconds()` is divided by 100 and then modulo-ed down to the number of frames. This very image is then additively drawn, centered at the star's position and modulated by a random color we generated in the constructor.

Now let's add easy code to the player to collect away stars from a list:

```cpp
class Player
{
    ...
    
    void collectStars(std::list<Star>& stars)
    {
        std::list<Star>::iterator cur = stars.begin();
        while (cur != stars.end())
        {
            if (Gosu::distance(posX, posY, cur->x(), cur->y()) < 35)
                cur = stars.erase(cur);
            else
                ++cur;
        }
    }
};
```

Let's extend Window to load the animation, spawn new stars, have the player collect them and draw the remaining ones:

```cpp
class GameWindow : public Gosu::Window
{
    std::auto_ptr<Gosu::Image> backgroundImage;
    Animation starAnim;
    
    Player player;
    std::list<Star> stars;
    
public:
    GameWindow()
    :   Window(640, 480)
    {
        setCaption(L"Gosu Tutorial Game");
        
        std::wstring filename = Gosu::resourcePrefix() + L"media/Space.png";
        backgroundImage.reset(new Gosu::Image(filename, Gosu::ifTileable));
        
        filename = Gosu::resourcePrefix() + L"media/Star.png";
        starAnim = Gosu::loadTiles(filename, 25, 25);
        
        player.warp(320, 240);
    }
    
    void update()
    {
        ...
        
        player.move();
        player.collectStars(stars);
        
        if (std::rand() % 25 == 0 && stars.size() < 25)
            stars.push_back(Star(starAnim));
    }
    
    void draw()
    {
        player.draw();
        backgroundImage->draw(0, 0, 0); 
        for (Star& star : stars)
            star.draw();
    }
    
    ...
};
```

(At this point, please download [Star.png](https://raw.githubusercontent.com/gosu/gosu/master/examples/media/Star.png) and ensure that it can be found at `media/Star.png`.)

Done! You can now collect stars.

### 4. Text and Sound

Finally, we want to draw the current score using a bitmap font and play a 'beep' sound every time the player collects a star. The Window will handle the text part, loading a font 20 pixels high:

```cpp
class GameWindow : public Gosu::Window
{
    std::auto_ptr<Gosu::Image> backgroundImage;
    Animation starAnim;
    Gosu::Font font;
    
    Player player;
    std::list<Star> stars;
      
public:
    ...
    
    GameWindow()
    :   Window(640, 480), font(20)
    {
        ...
    }
    
    ...
    
    void draw()
    {
        player.draw();
        backgroundImage->draw(0, 0, zBackground);
        
        for (Star& star : stars)
            star.draw();

        font.draw(L"Score: " + std::to_wstring(player.getScore()), 10, 10, zUI, 1, 1, Gosu::Color::YELLOW);
    }
};
```

What's left for the player? Right: A counter for the score, loading the sound and playing it.

```cpp
class Player
{
    Gosu::Image image;
    Gosu::Sample beep;
    double posX, posY, velX, velY, angle;
    unsigned score;
    
public:
    Player()
    :   image(Gosu::resourcePrefix() + L"media/Starfighter.bmp"),
        beep(Gosu::resourcePrefix() + L"media/Beep.wav")
    {
        posX = posY = velX = velY = angle = 0;
        score = 0;
    }
        
    unsigned getScore() const
    {
        return score;
    }

    ...

    void collectStars(std::list<Star>& stars, unsigned& score)
    {
        ...
            if (...)
            {
                cur = stars.erase(cur);
                score += 10;
                beep.play();
            }
            else
        ...
    }
...
```

(At this point, please download [Beep.wav](https://raw.githubusercontent.com/gosu/gosu/master/examples/media/Beep.wav) and ensure that it can be found at `media/Beep.wav`.)

As you can see, loading and playing sound effects could hardly be easier. See the reference for more powerful ways of playing back sounds.

That's it! Everything else is up to your imagination. If you want to see examples of other types of games being written in Ruby/Gosu, take a look at the great projects on the [Gosu Showcase board][boards.showcase].

[boards.showcase]: https://www.libgosu.org/cgi-bin/mwf/board_show.pl?bid=2 "Gosu Showcase Board"