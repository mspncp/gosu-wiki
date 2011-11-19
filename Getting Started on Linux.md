# Getting Started on Linux

(Gosu supposedly also works on FreeBSD if you adapt these steps.)

## Dependencies

To install Gosu in any form, you will need the following packages (install via `sudo apt-get install <packagename>`):

  * `build-essential`
  * `freeglut3-dev`
  * `libboost-all-dev`
  * `libfreeimage-dev`
  * `libgl1-mesa-dev`
  * `libpango1.0-dev`
  * `libopenal-dev`
  * `libsdl-mixer1.2-dev`
  * `libsdl-ttf2.0-dev`
  * `libsndfile-dev`
  * `libxinerama-dev`

*Copy-and-pastable command line* for Ubuntu, last tested on 10.10, should work across all versions:

```bash
# For C++
sudo apt-get install build-essential freeglut3-dev libboost-all-dev libfreeimage-dev libgl1-mesa-dev libpango1.0-dev libopenal-dev libsdl-mixer1.2-dev libsdl-ttf2.0-dev libsndfile-dev libxinerama-dev
# To install the gem for Ruby 1.8
sudo apt-get install build-essential freeglut3-dev libboost-all-dev libfreeimage-dev libgl1-mesa-dev libpango1.0-dev libopenal-dev libsdl-mixer1.2-dev libsdl-ttf2.0-dev libsndfile-dev libxinerama-dev ruby1.8-dev rubygems
# To install the gem for Ruby 1.9.1/1.9.2(?)
sudo apt-get install build-essential freeglut3-dev libboost-all-dev libfreeimage-dev libgl1-mesa-dev libpango1.0-dev libopenal-dev libsdl-mixer1.2-dev libsdl-ttf2.0-dev libsndfile-dev libxinerama-dev ruby1.9.1-dev rubygems
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

