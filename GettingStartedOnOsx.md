# Getting Started on OS X

[ ![Please post feedback and additions as comments to this page and visit the boards for questions outside the scope of a single wiki page. Thank you!](board_link.png) ][boards]

## Installing Boost (required for using Gosu with C++ only)

[Boost][] is a collection of libraries that is used throughout Gosu. Many parts of Boost have been marked for inclusion in the next standard of C++, so it's definitely worth a look a its docs.

_If you are using MacPorts_, you can, in theory, simply run `sudo port install boost`. In practice however, MacPorts' version of Boost is usually broken and/or outdated. _For [Homebrew][] users_, `brew install boost` should install the latest version without a hitch, but be aware that it may take several minutes to compile.

For most tasks, the headers of the boost library will be enough, so the easiest way to install them would be:

	svn co http://svn.boost.org/svn/boost/trunk/boost boost
	sudo mkdir -p /usr/local/include
	sudo mv boost /usr/local/include

## Starting a new Gosu game (C++)

In Xcode, create a new 'Application/Cocoa Application' project.

Remove & trash the following files:

* `Resources/MainMenu.nib` (or `.xib`, depending on the version of Xcode)
* `Other Sources/main.m`

Then right-click "Other Frameworks" and add a reference to an existing framework, namely Gosu.framework. Make sure you didn't put Gosu.framework into a system directory like `/System/Library/Frameworks` because Xcode treats these directories with some magic.

[[xcode_files.png]]

In order to make the Boost headers accessible, select 'Project/Edit Active Project' from the top menu, search for 'Header Search Paths' in 'Build' and set it to `/usr/local/include`, or `/opt/local/include` if you used MacPorts to install Boost.

[[xcode_header_paths.png]]

Your application bundle also needs to contain the Gosu.framework bundle. To instruct Xcode to automatically copy it into your application, choose Project/New Build Phase and select "Frameworks" as the Copy Files' target directory. Then locate this new build phase in the targets list and add Gosu.framework to it as well. (Note: You may have to drag & drop the framework into the build phase from the finder, instead of adding it via a right-click.)

__Note__: My version of Xcode defaults to using the 10.5 SDK. Gosu also works with 10.4 if you just select 10.4 everywhere, but you can do that once you've verified everything works.

You can then add new code files, for example the ones from the tutorial or this minimal application code:

	#include <Gosu/Gosu.hpp>

	class MyWindow : public Gosu::Window
	{
	public:
	    MyWindow()
	    : Gosu::Window(640, 480, false)
	    {
	        setCaption(L"Hello World!");
	    }
	};

	int main(int argc, char* argv[])
	{
	    MyWindow win;
	    win.show();
	}

Note: Usually, you want to right-click your target, Get Info, select Build/All Configurations/Build Locations and _change the Per-configuration Build Products Path to '.'_ or something similar, so the application will have the correct position relative to your game's resources.

### 64-bit Support

Gosu supports 64-bit builds, but there is a catch. Custom TTF file font loading for 64-bit uses an API not yet available on 10.5. This means you should include a flag to keep 10.5 from starting your 64-bit build: To do this, edit the `.plist` file of your project to add this key:

	<key>LSMinimumSystemVersionByArchitecture</key>
	<dict>
		<key>x86_64</key>
		<string>10.6.0</string>
		<key>i386</key>
		<string>10.4.0</string>
		<key>ppc</key>
		<string>10.4.0</string>
	</dict>

If you edit the file through Xcode, the editing will be a bit more intuitive.

## Starting a new Gosu game (Ruby)

Getting started with Ruby is a lot easier (surprise). Just install the gem via `gem install gosu` on your operating system's command line.

To test if everything works, you can use this Hello World script:

	require 'rubygems' # only necessary in Ruby 1.8
	require 'gosu'

	class MyWindow < Gosu::Window
	  def initialize
	    super(640, 480, false)
	    self.caption = 'Hello World!'
	  end
	end

	w = MyWindow.new
	w.show

That's it -- have fun!

[boost]: http://www.boost.org/
[forum]: http://www.libgosu.org/cgi-bin/mwf/forum.pl
[homebrew]: http://mxcl.github.com/homebrew/
[boards]: http://www.libgosu.org/cgi-bin/mwf/forum.pl "Gosu Boards"
