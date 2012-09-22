# Getting Started on Linux

(Gosu supposedly also works on FreeBSD if you adapt these steps.)

## Dependencies

To install Gosu in any form, you will need the following packages `build-essential`, `freeglut3-dev`, `libfreeimage-dev`, `libgl1-mesa-dev`, `libopenal-dev`, `libpango1.0-dev`, `libsdl-mixer1.2-dev`, `libsdl-ttf2.0-dev`, `libsndfile-dev`, `libxinerama-dev`

*Copy-and-pastable command line* for Ubuntu, last tested on 10.10, should work across all versions:

```bash
# For C++ or Ruby
sudo apt-get install build-essential freeglut3-dev libfreeimage-dev libgl1-mesa-dev libopenal-dev libpango1.0-dev libsdl-mixer1.2-dev libsdl-ttf2.0-dev libsndfile-dev libxinerama-dev

# Unless using RVM/rbenv or similar to install Ruby, you might want to install system Ruby:
# If you install Ruby 1.9 (may install 1.9.1, 1.9.2 or 1.9.3 depending on your distro).
sudo apt-get install ruby1.9.1-dev rubygems
# If you need to install Ruby 1.8 for some reason (deprecated)
sudo apt-get install ruby1.8-dev rubygems

```

*Copy-and-paste command line* for Fedora, last tested on 17, should work across all versions:

```bash
# For C++ or Ruby
sudo yum groupinstall --assumeyes "Development Tools"
sudo yum install --assumeyes freeglut-devel freeimage-devel mesa-libGL-devel openal-devel pango-devel SDL_mixer-devel SDL_ttf-devel libsndfile-devel libXinerama-devel

# To install Ruby 1.9
sudo yum install --assumeyes ruby-devel rubygems
```

*Copy-and-paste command line* for Arch Linux, last tested on 2012-09-13:

```bash
# For C++ or Ruby
sudo pacman -S freeglut freeimage libegl openal pango sdl_mixer sdl_ttf libsndfile libxinerama

# To install Ruby 1.9
sudo pacman -S ruby
```

*Copy-and-paste command line* for Gentoo Linux, last tested 2012-09-21:
```Bash
# For C++ or Ruby
sudo emerge -atv media-libs/freeglut media-libs/freeimage media-libs/mesa media-libs/openal x11-libs/pango media-libs/sdl-mixer media-libs/sdl-ttf media-libs/libsndfile x11-libs/libXinerama

# To install Ruby 1.9
sudo emerge -atv ruby:1.9

# For me, I had to install gosu like this:
gem install gosu -- --with-ldflags=-lXinerama
```

*Please check* how to install all this software if you are on a different distribution.

## Ruby Gem

If you are only interested in using Gosu with the Ruby programming language, you can install it as a Ruby gem via `sudo gem install gosu`. You need to install the packages from above.

Afterwards, `gem install gosu` should work.

## Compiling Gosu for C++

To compile Gosu, `cd` into the `linux` subdirectory and run:

```bash
./configure
make
```

There is a deprecated `make install` command that will work for C++, but as most Linux distributions are using a package manager nowadays we recommend copying the resulting `linux/libgosu.a` file to your game's directory manually.

## Using Gosu in C++

(The following assumes that you have installed Gosu system-wide via `sudo make install`. If not, you will have to add paths as necessary.)

You have to compile with `` `gosu-config --cxxflags` `` and `` `gosu-config --libs` ``, so a simple Makefile could look like this:

```make
OBJS = main.o player.o
CXXFLAGS += `gosu-config --cxxflags`
LIBS = `gosu-config --libs`

myGame: $(OBJS) libgosu.a
        g++ -o myGame $(OBJS) libgosu.a $(LIBS)
```