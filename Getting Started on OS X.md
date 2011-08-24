# Getting Started on OS X

## Starting a new Gosu game (C++)

*Note: The guide and screenshots are talking about Xcode 3. I am not sure if anyone has tried this with Xcode 4.*

In Xcode, create a new 'Application/Cocoa Application' project.

Remove & trash the following files:

* `Resources/MainMenu.nib` (or `.xib`, depending on the version of Xcode)
* `Other Sources/main.m`
* `Classes/...AppDelegate.h` and `Classes/...AppDelegate.m`

*Note:* You can remove & trash the precompiled prefix header too. You will need to remove it from the target settings as well then; just right-click your application target and look for 'prefix' in the search field.

Then right-click "Other Frameworks" and add a reference to an existing framework, namely Gosu.framework. Make sure you did not put Gosu.framework into a system directory like `/System/Library/Frameworks` because Xcode treats these directories differently.

[[xcode_files.png]]

Your application bundle also needs to *contain* the Gosu.framework bundle. To instruct Xcode to automatically copy it into your application, choose Project/New Build Phase and select "Frameworks" as the Copy Files' target directory. Then locate this new build phase in the targets list and add Gosu.framework to it as well. (Note: You may have to drag & drop the framework into the build phase from the finder, instead of adding it via a right-click.)

*Note:* If you want to be backwards compatible with 10.4, you will have to fiddle with the framework settings. Gosu supports 10.4, 32-bit and powerpc just fine.)

## Your application code

You can then add new code files, for example the ones from the tutorial or this minimal application code:

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

*Note:* Usually, you want to right-click your target, Get Info, select Build/All Configurations/Build Locations and _change the Per-configuration Build Products Path to '.'_ or something similar, so the application will have the correct position relative to your game's resources.

### 64-bit Support

Gosu supports 64-bit builds, but there is a catch. Custom TTF file font loading for 64-bit uses an API not yet available on 10.5. This means you should include a flag to keep 10.5 from starting your 64-bit build: To do this, edit the `.plist` file of your project to add this key:

```xml
<key>LSMinimumSystemVersionByArchitecture</key>
<dict>
	<key>x86_64</key>
	<string>10.6.0</string>
	<key>i386</key>
	<string>10.4.0</string>
	<key>ppc</key>
	<string>10.4.0</string>
</dict>
```

If you edit the file through Xcode, the editing will be a bit more intuitive.

## Starting a new Gosu game (Ruby)

Getting started with Ruby is a lot easier (surprise). Just install the gem via `sudo gem install gosu`. If you are using Ruby 1.8 or Ruby 1.9, this will installed the precompiled gem for your and you *do not even need Xcode*.
If you are using MacRuby or Rubinius, you will need to explicitly `sudo gem install ruby --platform=ruby`, which requires Xcode to be installed on your system.

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

That's it -- have fun!