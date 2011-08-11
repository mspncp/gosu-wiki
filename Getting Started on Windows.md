# Getting Started on Windows
## Creating a new Gosu game (Ruby)

Getting started with Ruby is very easy. Any Ruby version will work, either the Ruby Installer ones or the minimal builds from ruby-lang.org. In any case you will need RubyGems which comes with either version. Install Gosu:

    gem install gosu

Then create a new file and try to run it:

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

You can work your way from here using the RubyTutorial if you want.

## Adding Header/Library Paths (for C++ with Visual C++ 2008)

Gosu has no dependencies, unless you want to compile it yourself. However, we recommend (boost)[http://www.boost.org/], which the Gosu Tutorial game also uses. Simply download the latest release and extract it into a separate directory (you don't need to compile anything except for a few select parts of boost).

In Visual C++, go to Tools/Options/Projects and Solutions/VC++ Directories. Select the list of directories for include files and add the two directories you extracted boost and Gosu into—not the contained 'boost' or 'Gosu' subfolders.

[[msvc_1_include.png|alt=MSVC++ 2008 include directories]]

Also, select library files, and add the 'lib' subfolder from Gosu so MSVC can find Gosu.lib.

[[msvc_2_lib.png|alt=MSVC++ 2008 library directories]]

## Adding Header/Library Paths (for C++ with Visual C++ 2010) / Upgrading to Visual C++ 2010

In Visual C++ 2010, the process of adding libraries is way more complicated. First, change into "Expert Mode":

[[msvc10-expert.jpg|alt=MSVC++ 2010 "Expert Settings" menu]]

The "Property Manager" pane will appear behind the file list.

Then create a project as shown in the section below before continuing here. Unfold your project in the Property Manager:

[[msvc10-propsheet.png|alt=MSVC++ 2010 Property Manager]]

Then click the Microsoft.Cpp.Win32.User entry, which contain, among others, the VC directories.

[[msvc10-directories.png|alt=MSVC++ 2010 directories]]

Here you can add the header and library directories as shown for Visual C++ 2008:

[[msvc10-include.png|alt=MSVC++ 2010 include directories]]

*Don't forget to save* the property sheet changes by clicking the floppy disk icon.

If these steps are unclear, refer to the [Visual Studio 2010 C++ Project Upgrade Guide][msdn.upgrade]

## Creating a new C++ Gosu game (with Visual C++ 2008 or 2010)

Click File/New/Project and select 'Win32 project', then give it a name and in the application settings choose 'Empty project'.

[[msvc_3_proj.png|alt=MSVC++ new project window]]

[[msvc_4_proj2.png|alt=MSVC++ Application Wizard]]

*Note:* In the Express edition of MSVC, only "Win32 console application" is available. In this case, choose this and just add the following line somewhere in your source code. It should not affect building your source code on other platforms. (Thanks for the tip, anza!)

    #pragma comment(linker, "/SUBSYSTEM:windows /ENTRY:mainCRTStartup")

You can then add new code files, for example the one from the tutorial.

Next, you need to go into the project options, select C/C++ options, then Code Generation and change the used library from "Multithreaded DLL" to "Multithreaded", and "Multithreaded Debug DLL" to "Multithreaded Debug", respectively—or you will get linker errors. These options are usually only available after adding the first C++ source file.

[[msvc_5_rt.png|alt=MSVC++ code generation settings]]

*In Visual C++ 2010*, you will also need to change the compiler toolset to vc90 on the project's first property page. Gosu is not built for the vc100 toolset.

To ensure that your EXE file can find audiere.dll and your project's resources, you should also change its output directory for both configurations so that all files end up in the same place. (In this case I have put audiere.dll into the examples folder and built straight to that as I was testing the Tutorial game.)

[[msvc_6_outputdir.png|alt=MSVC++ output directory]]

If you need a starting point or want to test if everything is correctly set up, select File/New, add a new C++ source file and use this code to compile and run:

    #include <Gosu/AutoLink.hpp>
    #include <Gosu/Window.hpp>
    
    class MyWindow : public Gosu::Window
    {
    public:
        MyWindow()
        :   Window(640, 480, false, 20)
        {
            setCaption(L"Hello World!");
        }
    };
    
    int main()
    {
        MyWindow window;
        window.show();
    }

You can work your way from here using the [[C++ Tutorial]] if you want.

## Getting rid of DLL requirements

Gosu links against FreeImage.dll and OpenAL32.dll. However, if your image formats are covered by Windows' system libraries (PNG, BMP, JPG, GIF and more), then you don't need FreeImage.dll. Similarly, if you don't play any audio, you don't need OpenAL32.dll.

To get rid of the linker errors in this case, go to the properties of your project, "Linker/Input", and add "OpenAL32.dll;FreeImage.dll" to the list of "Delay Loaded DLLs" (empty by default).

(Gosu also needs libsndfile.dll to play audio, but this file is *always* lazily linked and you can just omit it if your app is silent.)

[msdn.upgrade]: http://blogs.msdn.com/b/vcblog/archive/2010/03/02/visual-studio-2010-c-project-upgrade-guide.aspx