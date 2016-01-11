# Getting Started on OS X

## Ruby

### Prerequisites

Gosu is built on top of the SDL 2 library. I recommend installing [Homebrew](http://brew.sh) and then running `brew install sdl2`.

### System Ruby (good) vs rbenv (good) vs rvm (bad)

OS X ships with a decent version of Ruby, and Gosu works just fine with it after you install either Apple's command-line tools (`xcode-select --install`) or Xcode (from the Mac App Store).

Note: If you are running **OS X 10.9 and have installed Xcode 6.1**, you will need to install Apple's command-line tools, Xcode won't work: `xcode-select --install` ([Apple bug](https://github.com/Homebrew/homebrew/issues/33431)).

**rbenv** seems to work just as well. **rvm doesn't** - it sometimes works, but the next day, it will use Homebrew to install bizarre compilers behind your back, which will then fail to compile C++ or Objective C. Please try to use rbenv or Apple's Ruby instead. `rvm use system`!

### Installing the gem

Install the gem via `sudo gem install gosu`. Omit the `sudo` if you use rvm or rbenv to manage your Ruby installations.

To test whether everything works as expected, you can use this Hello World script:

```ruby
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

* Xcode from the Mac App Store
* In Xcode, make sure to visit the preferences and install the Command Line Tools
* CocoaPods, which can be installed using `sudo gem install cocoapods` (again, omit `sudo` if you are using rbenv)

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
platform :osx, '10.7'

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