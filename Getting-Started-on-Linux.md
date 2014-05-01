# Getting Started on Linux

## Dependencies

To install Gosu 0.7.x on Linux, you will need the following packages: `build-essential`, `freeglut3-dev`, `libfreeimage-dev`, `libgl1-mesa-dev`, `libopenal-dev`, `libpango1.0-dev`, `libsdl-ttf2.0-dev`, `libsndfile-dev`, `libxinerama-dev`.

## Ubuntu (last tested on 12.10)

```bash
# Gosu's dependencies for both C++ and Ruby
sudo apt-get install build-essential freeglut3-dev libfreeimage-dev libgl1-mesa-dev \
                     libopenal-dev libpango1.0-dev libsdl-ttf2.0-dev libsndfile-dev \
                     libxinerama-dev

# To install Ruby 1.9 - if you are using rvm or rb-env, skip this step
sudo apt-get install ruby1.9.1-dev rubygems

# If you are using rvm or rb-env, do not use 'sudo'
sudo gem install gosu
```

## Fedora (last tested on 17)

```bash
# Gosu's dependencies for both C++ and Ruby
sudo yum groupinstall --assumeyes "Development Tools"
sudo yum install --assumeyes freeglut-devel freeimage-devel mesa-libGL-devel openal-devel pango-devel SDL_ttf-devel libsndfile-devel libXinerama-devel libvorbis-devel

# To install Ruby 1.9
sudo yum install --assumeyes ruby-devel rubygems
```

## Arch Linux (last tested on 2012-09-13)

```bash
# Gosu's dependencies for both C++ and Ruby
sudo pacman -S freeglut freeimage libegl openal pango sdl_ttf libsndfile libxinerama pkg-config

# To install Ruby 1.9
sudo pacman -S ruby
```

## Gentoo Linux (last tested 2013-11-10)

```bash
# Gosu's dependencies for both C++ and Ruby
sudo emerge -atv media-libs/freeglut media-libs/freeimage media-libs/mesa media-libs/openal x11-libs/pango media-libs/sdl-ttf media-libs/libsndfile x11-libs/libXinerama

# To install Ruby 1.9
sudo emerge -atv ruby:1.9
```

## OpenSuse (last tested on 2012-11-14 / 12.1)

```bash
sudo zypper addrepo http://download.opensuse.org/repositories/games/openSUSE_12.1/ opensuse-games
sudo zypper install libfreeimage-devel freeglut-devel libSDL_ttf libsndfile-devel openal-soft-devel libSDL_ttf-devel pango-devel libvorbis-devel

gem install gosu
```

*Please check* how to install all this software if you are on a different distribution.

## Compiling Gosu for C++

To compile Gosu, `cd` into the `cmake` subdirectory and run:

```bash
./build.sh
```

If you are using debian/ubuntu you can use 
```bash
./create_deb_package.sh
xdg-open build/*.deb
```
On all other systems you can run, but be aware, there is no uninstall target
```bash
cd build
sudo make install
```

## Using Gosu in C++ with cmake

Have a look at the examples, the example CMakeLists.txt are short, commented and straight forward.

```CMakeLists.txt
Find_Library(gosu REQUIRED)
```

## Using Gosu in C++ without cmake

(The following assumes that you have installed Gosu system-wide)

You have to compile with `` `pkg-config --cflags gosu` `` and `` `pkg-config --libs gosu` ``, so a simple Makefile could look like this:

```make
OBJS = main.o player.o
CXXFLAGS += `pkg-config --cflags gosu`
LIBS = `pkg-config --libs gosu`

myGame: $(OBJS) libgosu.a
        g++ -o myGame $(OBJS) libgosu.a $(LIBS)
```