#summary How to set up Gosu on Windows.

[http://www.libgosu.org/cgi-bin/mwf/forum.pl http://www.libgosu.org/wiki_images/board_link.png]

= Creating a new Gosu game (Ruby) =

Getting started with Ruby is a lot easier. Any Ruby version will work, either the Ruby Installer ones or the minimal builds from ruby-lang.org. In any case you will need Rubygems which comes with either version. Install Gosu:

`gem install gosu`

Then create a new file and try to run it:

{{{
require 'rubygems'
require 'gosu'

class MyWindow < Gosu::Window
  def initialize
    super 640, 480, false
    self.caption = 'Hello World!'
  end
end

w = MyWindow.new
w.show
}}}

You can work your way from here using the RubyTutorial if you want.

= Adding Header/Library Paths (for C++ with Visual C++ 2008) =

The only dependency for using Gosu is [http://www.boost.org/ boost]. Many parts of boost have been marked for inclusion in the next standard of C++, so you'd better look at it anyway! :) Download the latest release and extract it into a separate directory. *You do not have to compile anything* for Gosu, the boost headers are enough and cover most of its libraries.

In Visual C++, go to Tools/Options/Projects and Solutions/VC++ Directories. Select the list of directories for include files and add the two directories you extracted boost and Gosu into—not the contained 'boost' or 'Gosu' subfolders.

http://www.libgosu.org/wiki_images/msvc_1_include.png

Also, select library files, and add the 'lib' subfolder from Gosu so MSVC can find Gosu.lib.

http://www.libgosu.org/wiki_images/msvc_2_lib.png

= Adding Header/Library Paths (for C++ with Visual C++ 2010 / Upgrading to Visual C++ 2010 =

In Visual C++ 2010, the process of adding libraries is way more complicated. First, change into "Expert Mode":

http://www.libgosu.org/wiki_images/msvc10-expert.jpg

The "Property Manager" pane will appear behind the file list.

Then create a project as shown in the section below before continuing here. Unfold your project in the Property Manager:

http://www.libgosu.org/wiki_images/msvc10-propsheet.png

Then click the Microsoft.Cpp.Win32.User entry, which contain, among others, the VC directories.

http://www.libgosu.org/wiki_images/msvc10-directories.png

Here you can add the header and library directories as shown for Visual C++ 2008:

http://www.libgosu.org/wiki_images/msvc10-include.png

*Don't forget to save* the property sheet changes by clicking the floppy disk icon.

If these steps are unclear, refer to http://blogs.msdn.com/b/vcblog/archive/2010/03/02/visual-studio-2010-c-project-upgrade-guide.aspx

= Creating a new C++ Gosu game (with Visual C++ 2008 or 2010) =

Click File/New/Project and select 'Win32 project', then give it a name and in the application settings choose 'Empty project'.

http://www.libgosu.org/wiki_images/msvc_3_proj.png

http://www.libgosu.org/wiki_images/msvc_4_proj2.png

*Note:* In the Express edition of MSVC, only "Win32 console application" is available. In this case, choose this and just add the following line somewhere in your source code. It should not affect building your source code on other platforms. (Thanks for the tip, anza!)

{{{
#pragma comment(linker, "/SUBSYSTEM:windows /ENTRY:mainCRTStartup")
}}}

You can then add new code files, for example the one from the tutorial.

Next, you need to go into the project options, select C/C++ options, then Code Generation and change the used library from "Multithreaded DLL" to "Multithreaded", and "Multithreaded Debug DLL" to "Multithreaded Debug", respectively—or you will get linker errors. These options are usually only available after adding the first C++ source file.

http://www.libgosu.org/wiki_images/msvc_5_rt.png

*In Visual C++ 2010*, you will also need to change the compiler toolset to vc90 on the project's first property page. Gosu is not built for the vc100 toolset.

To ensure that your EXE file can find fmod.dll and your project's resources, you should also change its output directory for both configurations. (In this case I have put fmod.dll into the examples folder and built straight to that as I was testing the Tutorial game.)

http://www.libgosu.org/wiki_images/msvc_6_outputdir.png

If you need a starting point or want to test if everything is correctly set up, select File/New, add a new C++ source file and use this code to compile and run:

{{{
#include <Gosu/AutoLink.hpp>
#include <Gosu/Window.hpp>

class MyWindow : public Gosu::Window
{
public:
    MyWindow()
    : Gosu::Window(640, 480, false, 20)
    {
        setCaption(L"Hello World!");
    }
};

int main(int argc, char* argv[])
{
    MyWindow win;
    win.show();
    return 0;
}
}}}

You can work your way from here using the CppTutorial if you want.