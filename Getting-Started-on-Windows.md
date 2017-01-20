# Getting Started on Windows
## Creating a new Gosu game (Ruby)

Getting started with Ruby is very easy. Any Ruby version will work, either the Ruby Installer ones or the minimal builds from ruby-lang.org. In any case you will need RubyGems which comes with either version. Install Gosu:

```
gem install gosu
```

Then create a new file and try to run it:

```ruby
require 'gosu'

class MyWindow < Gosu::Window
  def initialize
    super 640, 480
    self.caption = 'Hello World!'
  end
end

window = MyWindow.new
window.show
```

You can work your way from here using the [[Ruby Tutorial]] if you want, or you can check out Gosu's own example games:

```
gem install gosu-examples
gosu-examples
```

## Gosu for C++ with MinGW

See this separate guide: [[Compiling in Windows using MinGW]]

## Setting up Visual C++ 2015

Download and extract the latest version of Gosu for Windows from the [releases page](https://github.com/gosu/gosu/releases).

The ZIP archive includes everything that is necessary for *using* Gosu (*compiling* Gosu requires a few more header files).

Now we need to let Visual C++ know where to find Gosu. First, change into "Expert Mode":

[[msvc10-expert.jpg|alt=MSVC++ 2010 "Expert Settings" menu]]

The "Property Manager" pane will appear behind the file list.

Then create a project as shown in the section below before continuing here. Unfold your project in the Property Manager:

[[msvc10-propsheet.png|alt=MSVC++ 2010 Property Manager]]

Click the Microsoft.Cpp.Win32.User entry, which contain, among others, the VC directories.

[[msvc10-directories.png|alt=MSVC++ 2010 directories]]

Here you can add the directory in which you have extracted Gosu as a header path, and the "lib" and directory as a library path:

[[msvc10-include.png|alt=MSVC++ 2010 include directories]]

Now you can go back and do the same for Microsoft.Cpp.x64.User, except this time you will need to add Gosu's "lib64" directory.

*Don't forget to save* your changes to the properties by clicking the floppy disk icon.

## Create a new Gosu game with Visual C++ 2015

Click File/New/Project and select 'Win32 project', then give it a name and in the application settings choose 'Empty project'.

[[msvc_3_proj.png|alt=MSVC++ new project window]]

[[msvc_4_proj2.png|alt=MSVC++ Application Wizard]]

You can then add C++ code files to your project, for example the one from the [[C++ Tutorial]].

Next, open the project options, select C/C++ options, Code Generation, and change the used library from "Multithreaded DLL" to "Multithreaded", and "Multithreaded Debug DLL" to "Multithreaded Debug", respectively, or you will get linker errors later. These options are only available *after* adding the first C++ source file.

[[msvc_5_rt.png|alt=MSVC++ code generation settings]]

To ensure that your EXE file can find SDL2.dll and your images and sound files, you should also change your project's output directory for both configurations (Release/Debug) so that all files end up in the same place. (In this case I have copied all DLLs from Gosu's "lib" folder into the "examples" folder, and am building Tutorial.exe into this folder so that it can find everything.)

[[msvc_6_outputdir.png|alt=MSVC++ output directory]]

Once you have everything set up, you can follow the [[C++ Tutorial]] to learn about Gosu.
