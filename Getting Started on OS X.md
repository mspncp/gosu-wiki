# Getting Started on OS X

## Ruby

### Prerequisites

Gosu 0.8.x+ relies on the SDL 2 library. I recommend installing [Homebrew](http://brew.sh) and then running `brew install sdl2 libogg libvorbis`.

Note: If you are adventurous, you can also install the Mercurial version of SDL: `brew install sdl2 --HEAD`. This has fixed a few HiDPI-related bugs for me.

### System Ruby vs rvm vs rbenv

OS X ships with a decent version of Ruby, and Gosu works just fine with it after you install either Apple's command-line tools (`xcode-select --install`) or Xcode (from the Mac App Store).

But if you are running **OS X 10.9 and have installed Xcode 6.1**, you will need to install Apple's command-line tools on top of Xcode: `xcode-select --install`; [Apple bug](https://github.com/Homebrew/homebrew/issues/33431). Also, **OS X 10.9.0 – 10.9.2** have shipped with a broken `rbconfig` file that prevented Gosu and other C extensions from being built, simply update OS X in this case; [Apple bug](https://github.com/flori/json/issues/200).

**rbenv** seems to work just as well. **rvm doesn't** - it sometimes works, but the next day, it will use homebrew to install bizarre compilers behind your back, which will then fail at compiling C++ or Objective C. Please try to use rbenv or Apple's Ruby instead. For example, to simply switch to Apple's Ruby use `rvm use system`.

### Installing the gem

Just install the gem via `sudo gem install gosu`. (Omit the `sudo` if you use rvm or rbenv to manage your Ruby installations.)

To test whether everything works as expected, you can use this Hello World script:

```ruby
require 'rubygems' # only necessary in Ruby 1.8
require 'gosu'

class MyWindow < Gosu::Window
  def initialize
   super(640, 480, false)
   self.caption = 'Hello World!'
  end
end

window = MyWindow.new
window.show
```

## Creating a New C++ Gosu Project

*TO DO: This does not yet explain how resource loading works; TL;DR add your resources to the Xcode project and use `Gosu::resource_path` to find them.*

Gosu uses [CocoaPods](http://cocoapods.org/) to streamline the Xcode project setup. Even though CocoaPods calls itself an "Objective C library manager", it is a great tool to integrate the C++ based Gosu library into your project along with all its dependencies.

### Prerequisites

* Xcode 4+ from the Mac App Store
* In Xcode, make sure to visit the preferences and install the Command Line Tools
* CocoaPods, which can be installed using `sudo gem install cocoapods`

### Creating the project

Start Xcode and create a new project. Use the template 'OS X/Application/Cocoa Application':

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
# Gosu should work with versions as low as OS X 10.5
platform :osx, '10.8'

pod 'Gosu', :git => 'https://github.com/jlnr/gosu.git'
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
    :   Gosu::Window(640, 480, false)
    {
        setCaption(L"Hello World!");
    }
};

int main()
{
    MyWindow window;
    window.show();
}
```

If you "Build & Run" the project now (cmd+R), you should see an empty, black window with the caption "Hello World".