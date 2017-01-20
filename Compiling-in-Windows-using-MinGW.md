_**Warning: This guide was kindly donated a while ago, but even the authors have experienced unexplainable problems using Gosu with MinGW. If you can fix/complete the guide, it would be very appreciated. Otherwise, I recommend using the free desktop version of Microsoft Visual C++ 2015.**_

--

In this tutorial we will compile Gosu using MinGW, the set of open source GNU compilers for Windows. There are a few steps involved and it's still a work-in-progress, so feedback is greatly appreciated.

## Installing MinGW
The first step is downloading and installing MinGW. The best way of doing this is using the new [Automated MinGW Installer](http://sourceforge.net/projects/mingw/files/Automated%20MinGW%20Installer/). 

Once you've installed MinGW, you should add the `bin` folder within MinGW to the Windows `PATH`.

## Downloading and compiling Gosu
Next, you should download Gosu's source code. Go to the [trunk repository](https://github.com/jlnr/gosu), click in _Downloads_ and get the `tar.gz` package. Then, uncompress it somewhere close to your project.

### Getting some dependencies
Before compiling you need to get some dependencies. The best way of handling these is creating a folder in the root of your hdd called `c:\lib`. This way, it will be easier to reach and reference the libraries.

* **SDL** -- [Website](http://www.libsdl.org). Get the development version for mingw32. Currently the latest version can be downloaded [here](http://www.libsdl.org/release/SDL-devel-1.2.14-mingw32.tar.gz).
* **SDL_Mixer** -- [Website](http://www.libsdl.org/projects/SDL_mixer/). Get the binary for Win32, which includes both the headers and the library.
* **FreeImage** -- [Website](http://freeimage.sourceforge.net/download.html). Get the binary distribution.
* **OpenAL** -- [Website](http://connect.creativelabs.com/openal/Downloads/Forms/AllItems.aspx). Get the OpenAL SDK.
* **Microsoft DirectX SDK** -- Pretty easy to find, use Google.

The DirectX's SDK will get installed in his own folder within Program Files, you're supposed to uncompress the rest of the dependencies in the `c:\lib` commented previously.

### Modifying the Makefile
Browse to the folder where you decompressed Gosu and create a new file within the gosu folder called `Makefile`. Then, paste the following code

```
SRCS = GosuImpl/Sockets/CommSocket.cpp GosuImpl/DirectoriesWin.cpp GosuImpl/FileWin.cpp GosuImpl/InputWin.cpp GosuImpl/Inspection.cpp GosuImpl/IO.cpp GosuImpl/Sockets/ListenerSocket.cpp GosuImpl/Math.cpp GosuImpl/Sockets/MessageSocket.cpp GosuImpl/Sockets/Socket.cpp GosuImpl/TextInputWin.cpp GosuImpl/TimingWin.cpp GosuImpl/Utility.cpp GosuImpl/WindowWin.cpp GosuImpl/WinMain.cpp GosuImpl/WinUtility.cpp GosuImpl/Graphics/Bitmap.cpp GosuImpl/Graphics/BitmapColorKey.cpp GosuImpl/Graphics/BitmapFreeImage.cpp GosuImpl/Graphics/BitmapUtils.cpp GosuImpl/Graphics/BlockAllocator.cpp GosuImpl/Graphics/Color.cpp GosuImpl/Graphics/Font.cpp GosuImpl/Graphics/Graphics.cpp GosuImpl/Graphics/Image.cpp GosuImpl/Graphics/LargeImageData.cpp GosuImpl/Graphics/TexChunk.cpp GosuImpl/Graphics/Text.cpp GosuImpl/Graphics/TextTTFWin.cpp GosuImpl/Graphics/Texture.cpp GosuImpl/Graphics/TextWin.cpp GosuImpl/Graphics/Transform.cpp GosuImpl/Audio/AudioSDL.cpp

OBJS = $(SRCS:.cpp=.o)

DXINCLUDE = "C:\Program Files (x86)\Microsoft DirectX SDK (June 2010)\Include"

CXXFLAGS  = -Wall -g -I. -I$(DXINCLUDE) -DUNICODE -D_UNICODE -DMINGW -DWIN32 -D_DEBUG
CXXFLAGS += -Ic:/lib/freeimage/Dist -Ic:/lib/SDL/include/SDL -Ic:/lib/SDL_mixer/include
CXXFLAGS += -Idependencies/libogg/include -Idependencies/libvorbis/include

all: $(OBJS)
	ar rcs lib/libgosu.a $(OBJS)

clean:
	del GosuImpl\*.o
```
In the line `DXINCLUDE = ...` you should put the correct path where DirectX SDK got installed. Also, if you didn't use `c:\lib` for the libraries, you should modify the second `CXXFLAGS` line accordingly.

Once you're done with this, open a MS-DOS prompt (Home -> Run -> cmd), go to the gosu folder and type `mingw32-make`. Gosu should get compiled without errors.

## Compiling your project
Once you're done compiling Gosu, the next step will be compiling your own project. The main regard here is the high amount of libraries you have to link against. These are the linkage flags for your Makefile

```
LDFLAGS   += -I. gosu/lib/libgosu.a -lintl
LDFLAGS   += -Lc:/lib/SDL_mixer/lib -lSDL_mixer 
LDFLAGS   += -Lc:/lib/freeimage/Dist -lfreeimage 
LDFLAGS   += -Lc:/lib/SDL/lib -llibsdl 
LDFLAGS   += -lopengl32 -lglu32 -lgdi32 -lwinmm -ldxguid -lws2_32 -ldinput8
LDFLAGS   += -Lc:/lib/openal/libs/Win64 -lOpenAl32
```

And these are the .dll you need to ship with your executable:

* SDL.dll
* SDL_mixer.dll
* libfreetype-6.dll
* zlib1.dll
* FreeImage.dll
* libvorbis-0.dll
* libvorbisfile-3.dll
* libogg-0.dll
* OpenAL32.dll
* libsndfile.dll if you are loading sounds other than Ogg Vorbis (e.g. WAV files)

# DISCLAIMER
This is still under heavy test. There may be extra things, there may be missing things. Any feedback is appreciated.