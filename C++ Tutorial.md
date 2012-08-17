# C++ Tutorial

## Source Code

The code for the complete game, together with the required media files, can be found in the Gosu distribution of your choice ('examples/Tutorial.cpp'). To run the game, setup a new project as seen in [[Getting Started on OS X]], [[Getting Started on Windows]] or [[Getting Started on Linux]], respectively, and use `Tutorial.cpp` as the only source file. Take care so that the resulting game can find the resource files in the same folder (`examples/media`).

## The Tutorial
### 1. Overriding Window's callbacks

The easiest way to create a complete Gosu application is to write a new class that derives from `Gosu::Window` (see the reference for a complete description of its interface). Here's how a minimal GameWindow class might look like:

```cpp
// All of Gosu.
#include <Gosu/Gosu.hpp>
// To safely include std::tr1::shared_ptr
#include <Gosu/TR1.hpp> 
// Makes life easier for Windows users compiling this.
#include <Gosu/AutoLink.hpp>

#include <cmath>
#include <cstdlib>
#include <list>
#include <sstream> // For int <-> string conversion
#include <vector>
      
class GameWindow : public Gosu::Window
{
public:
    GameWindow()
    :   Window(640, 480, false)
    {
        setCaption(L"Gosu Tutorial Game");
    }

    void update()
    {
        // ...
    }

    void draw()
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

The constructor initializes the `Gosu::Window` base class. The parameters shown here create a 640x480 pixels large, non-fullscreen window. Then it changes the caption, which is empty until then. Note that Gosu uses `std::wstring` almost everywhere.

`update()` and `draw()` are overrides of `Gosu::Window`'s member functions. `update()` is (by default) called 60 times per second and should contain the main game logic, such as moving objects around and testing for collisions.

`draw()` is called afterwards or whenever the window needs redrawing for other reasons. It should contain code to redraw the whole scene, but no logic. Think of it as an side-effect free mapping from the game state to the video output.

Then follows the main program. A window is created and its `show()` member function is called, which does not return until the window has been closed by the user or its own code. Tada — now you have a small black window with a title of your choice!

A diagram of the main loop is shown on the [[Window Main Loop]] page.

### 2. Using Images

```cpp
class GameWindow : public Gosu::Window
{
    std::auto_ptr<Gosu::Image> backgroundImage;

public:
    GameWindow()
    :   Window(640, 480, false),
        font(graphics(), Gosu::defaultFontName(), 20),
        player(graphics())
    {
        setCaption(L"Gosu Tutorial Game");

        std::wstring filename = Gosu::sharedResourcePrefix() + L"media/Space.png";
        backgroundImage.reset(new Gosu::Image(graphics(), filename, true));
    }

    void update()
    {
        // ...
    }

    void draw()
    {
        // ...
    }
};
```

*Note:* `Image` has no default constructor as Gosu does not support empty zombie images. An `auto_ptr` is used here so we can delay the actual creation of the image. The new `unique_ptr`in C++0x or `boost::optional` from the Boost library do the trick as well, or you could just use the Image as a direct member and initialize it in the initializer list, as we will do in another class.
Of course, if you want to use a raw pointer and `new`/`delete`, we cannot stop you either.

`Gosu::Image`'s constructor takes three arguments. First, it is tied to a Graphics instance (`graphics()` yields the Window's embedded Graphics object). Second, the filename of the image file is given. Note the `sharedResourcePrefix` function, which returns The Right Thing; see the reference for more information. The third argument specifies whether the image is to be created with hard or soft borders when tiling. See [[BasicConcepts]] for an explanation. It is ignored in this Tutorial. When in doubt, pass true.

As mentioned in the last section, the Window's `draw()` member function is the place to draw everything, so this is the place for us to draw our background image. The arguments are almost obvious. The image is drawn at `0, 0` - the third image is the Z position; again, see [[BasicConcepts]].

#### 2.1. Player & Movement

Here comes a simple player class:

```cpp
class Player
{
    Gosu::Image image;
    double posX, posY, velX, velY, angle;
        
    public:
        explicit Player(Gosu::Graphics& graphics)
        :   image(graphics, Gosu::sharedResourcePrefix() + L"media/Starfighter.bmp")
        {
            posX = posY = velX = velY = angle = 0;
        }
        
        void warp(double x, double y)
        {
            posX = x;
            posY = y;
        }
        
        void turnLeft()
        {
            angle -= 4.5;
        }
        
        void turnRight()
        {
            angle += 4.5;
        }
        
        void accelerate()
        {
            velX += Gosu::offsetX(angle, 0.5);
            velY += Gosu::offsetY(angle, 0.5);
        }
        
        void move()
        {
            posX += velX;
            posX = Gosu::wrap(posX, 0.0, 640.0);
            posY += velY;
            posY = Gosu::wrap(posY, 0.0, 480.0);

            velX *= 0.95;
            velY *= 0.95;
        }
        
        void draw() const
        {
            image.drawRot(posX, posY, 1, angle);
        }
    };
```

There are a couple of things to say about this:

[[angles2.png|alt=Angles in Gosu]]

  * `Player::accelerate` makes use of the `offsetX`/`offsetY` functions. They are similar to what some people use sin/cos for: For example, if something moved 100 pixels per frame at an angle of 30°, it would pass `offsetX(30, 100)` pixels horizontally and `offsetY(30, 100)` pixels vertically per frame.
  * When loading BMP files, Gosu replaces `#ff00ff` (fuchsia/magenta; that really ugly pink) with transparent pixels.
  * Note that `drawRot` puts the *center* of the image at `x, y` - *not* the upper left corner, as with draw. Also, the player is drawn at `z = 1`, i.e. over the background. We'll replace these magic numbers with something better later. Also, see the reference for all the drawing methods and arguments.
  * `Gosu::wrap(what, min, max)` maps a value inside the *min..max* range. If the player leaves the screen on the left side, he will enter it from the right side etc. -- if you wanted to disable this "wraparound" feature, you could use `Gosu::clamp(what, min, max)` instead.
  * The player just loads the image straight in the initializer list, unlike the Window which did it a bit more complicated.

#### 2.2. Integrating Player with the Window

```cpp
class GameWindow : public Gosu::Window
{
    std::auto_ptr<Gosu::Image> backgroundImage;

    Player player;
        
public:
    GameWindow()
    :   Window(640, 480, false),
        player(graphics())
    {
        setCaption(L"Gosu Tutorial Game");
        
        std::wstring filename = Gosu::sharedResourcePrefix() + L"media/Space.png";
        backgroundImage.reset(new Gosu::Image(graphics(), filename, true));
        
        player.warp(320, 240);
    }
    
    void update()
    {
        if (input().down(Gosu::kbLeft) || input().down(Gosu::gpLeft))
            player.turnLeft();
        if (input().down(Gosu::kbRight) || input().down(Gosu::gpRight))
            player.turnRight();
        if (input().down(Gosu::kbUp) || input().down(Gosu::gpButton0))
            player.accelerate();
        player.move();
    }
    
    void draw()
    {
        player.draw();
        backgroundImage->draw(0, 0, 0);
    }
    
    void buttonDown(Gosu::Button btn)
    {
        if (btn == Gosu::kbEscape)
           close();
    }
};
```

As you can see, we have introduced keyboard and gamepad input!

Similar to `update()` and `draw()`, `Gosu::Window` provides two virtual member functions `buttonDown(btn)` and `buttonUp(btn)` which can be overridden. They do nothing by default. We do this here to close the window when the user presses `Esc`. For a list of predefined button constants, see the reference.

While getting feedback on pushed buttons is suitable for one-time events such as UI interaction, jumping or typing, it is rather useless for actions that span several frames — for example, moving by holding buttons down. This is where the `update()` member function comes into play, which calls the player's movement methods. If you run this section's code, you should be able to fly around!

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

For historical reasons, this Tutorial still uses a more complicated type:

    typedef std::vector<std::tr1::shared_ptr<Gosu::Image> > Animation;

For a real game, there is no way around writing some classes that fit the game's individual needs, but we'll get away with this solution for now.

Let's introduce the stars which are the central object of this lesson. Stars appear out of nowhere at a random place on the screen and live their animated lives until the player collects them. The definition of the Star class is rather simple:

```cpp
class Star
{
    Animation& animation;
    Gosu::Color color;
    double posX, posY;

public:
    explicit Star(Animation& animation)
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
        Gosu::Image& image =
            *animation.at(Gosu::milliseconds() / 100 % animation.size());

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
    :   Window(640, 480, false),
        player(graphics())
    {
        setCaption(L"Gosu Tutorial Game");
        
        std::wstring filename = Gosu::sharedResourcePrefix() + L"media/Space.png";
        backgroundImage.reset(new Gosu::Image(graphics(), filename, true));
        
        filename = Gosu::sharedResourcePrefix() + L"media/Star.png";
        Gosu::imagesFromTiledBitmap(graphics(), filename, 25, 25, false, starAnim);
        
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
        for (std::list<Star>::const_iterator i = stars.begin();
            i != stars.end(); ++i)
        {
            i->draw();
        }
    
    }
    
    ...
};
```

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
    :   Window(640, 480, false),
        font(graphics(), Gosu::defaultFontName(), 20),
        player(graphics())
    {
        ...
    }
    
    ...
    
    void draw()
    {
        player.draw();
        backgroundImage->draw(0, 0, zBackground);
        
        for (std::list<Star>::const_iterator i = stars.begin();
            i != stars.end(); ++i)
        {
            i->draw();
        }

        std::wstringstream score;
        score << L"Score: "; 
        score << player.getScore();
        font.draw(score.str(), 10, 10, zUI, 1, 1, Gosu::Colors::yellow);
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
    Player(Gosu::Graphics& graphics)
    :   image(graphics, Gosu::sharedResourcePrefix() + L"media/Starfighter.bmp"),
        beep(Gosu::sharedResourcePrefix() + L"media/Beep.wav")
    {
        posX = posY = velX = velY = angle = 0;
        score = 0;
    }
        
    unsigned getScore() const
    {
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

As you can see, loading and playing sound effects could hardly be easier. See the reference for more powerful ways of playing back sounds - fiddle around with volume, position and pitch.

That's it! Everything else is up to your imagination. If you cannot imagine how this is enough to create games, see the games on the [Gosu Showcase board][showcase].

[showcase]: http://www.libgosu.org/cgi-bin/mwf/board_show.pl?bid=2 "Gosu Showcase Board"
