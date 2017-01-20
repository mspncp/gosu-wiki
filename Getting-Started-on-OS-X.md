# Getting Started on macOS

## Prerequisites

Gosu depends on the [SDL 2 library](http://www.libsdl.org/). Please install [Homebrew](http://brew.sh) and run `brew install sdl2`.

If you have not installed Ruby yet, I recommend also running `brew install ruby`. The problem with Apple's built-in Ruby is that it is often outdated and/or broken. The popular `rvm` tool is not compatible with Gosu. Ruby from Homebrew and `rbenv` are both good choices.

### Installing Ruby/Gosu

Install the Gosu gem via `gem install gosu`.

To test whether everything works as expected, you can use this one-liner, which should open a window:

```bash
ruby -rgosu -e 'w = Gosu::Window.new(200, 150); w.caption = "It works!"; w.show'
```

Or you can install and run the [`gosu-examples` gem](https://github.com/gosu/gosu-examples):

```bash
gem install gosu-examples
gosu-examples
```

## Creating a New C++ Gosu Project with Xcode

*TODO: This does not yet explain how resource loading works: Add your resources to the Xcode project and use `Gosu::resource_path` to find them.*

Gosu uses [CocoaPods](http://cocoapods.org/) to streamline the Xcode project setup. Even though CocoaPods calls itself an "Objective C library manager", it is a great tool to integrate the C++ based Gosu library into your project along with all its dependencies. This is the recommended way to use Gosu if you want to port your game to iOS later.

### Prerequisites

* Xcode from the Mac App Store
* In Xcode, make sure to visit the preferences and install the Command Line Tools
* CocoaPods, which can be installed using `gem install cocoapods`

### Creating the project

Start Xcode and create a new project. Use the template 'macOS/Application/Cocoa Application':

[[xcode_new_app.png]]

None of the settings in the following dialog are required, so you can leave them all unchecked:

[[xcode_new_app_settings.png]]

Remove & trash the following files:

* `Classes/AppDelegate.h`
* `Classes/AppDelegate.m`
* `Resources/MainMenu.xib`

[[xcode_delete_these_files.png]]

Now close the project, open your text editor of choice and create a file called `Podfile` in the same directory as your `.xcodeproj`:

```ruby
platform :osx, '10.7'

pod 'Gosu', :git => 'https://github.com/gosu/gosu.git'
```

On the command line, navigate to the folder in which you created the `Podfile` and run `pod install`. This will create an `.xcodeworkspace` file that contains your project, Gosu and all of its dependencies.

### Adding Code and Resources

At this point, your project still contains the `main.m` file that Xcode has generated for you. Rename it to `main.cpp` and replace its contents by the following code:

```cpp
#include <Gosu/Gosu.hpp>

class MyWindow : public Gosu::Window
{
public:
    MyWindow()
    : Gosu::Window(640, 480)
    {
        set_caption("Hello World!");
    }
};

int main()
{
    MyWindow window;
    window.show();
}
```

If you "Build & Run" the project now (cmd+R), you should see an empty, black window with the caption "Hello World".

## Using Gosu for C++ without CocoaPods

If you are not keen on using Xcode and/or CocoaPods, you can also install Gosu as a "normal" library using Homebrew:

`brew install libgosu` ([formula here])

You can then use Gosu with CMake or pkg-config as demonstrated in [[Getting Started on Linux]].

This is the recommended way to use Gosu for desktop games because it makes it easy to build on Linux.