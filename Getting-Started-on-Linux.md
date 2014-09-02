# Getting Started on Linux

(Please help us update the information below! :) Most of it refers to Gosu 0.7.x).

## Dependencies

To install Gosu 0.8.x on Linux, you will need the following packages, even though the names will be different in every distribution: `libsdl2-dev`, `libsdl2-ttf-dev`, `libpango1.0-dev`, `libgl1-mesa-dev`, `libfreeimage-dev`, `libopenal-dev`, `libsndfile-dev`.

## Ubuntu (last tested on Trusty Tahr (14.04), with Gosu 0.8.2)

```bash
# Gosu's dependencies for both C++ and Ruby
sudo apt-get install build-essential libsdl2-dev libsdl2-ttf-dev libpango1.0-dev \
                     libgl1-mesa-dev libfreeimage-dev libopenal-dev libsndfile-dev

# To install Ruby 1.9.x - if you are using rvm or rbenv, please skip this step
sudo apt-get install ruby-dev

# If you are using rvm or rbenv, do not use 'sudo'
sudo gem install gosu
```

## Manjaro Linux (last tested on 2014-09-02 with Gosu 0.8.3)

```bash
# Gosu's dependencies for both C++ and Ruby
sudo pacman -S freeglut freeimage libegl openal pango sdl2_ttf libsndfile libxinerama pkg-config

# To install Ruby 2.1.2
sudo pacman -S ruby
```

## Fedora (last tested on 20 with Gosu 0.7.x)

```bash
# Gosu's dependencies for both C++ and Ruby
sudo yum groupinstall --assumeyes "Development Tools"
sudo yum install --assumeyes freeglut-devel freeimage-devel mesa-libGL-devel openal-devel pango-devel SDL_ttf-devel libsndfile-devel libXinerama-devel libvorbis-devel gcc-c++

# To install Ruby 1.9
sudo yum install --assumeyes ruby-devel rubygems
```

## Arch Linux (last tested on 2012-09-13 with Gosu 0.7.x)

```bash
# Gosu's dependencies for both C++ and Ruby
sudo pacman -S freeglut freeimage libegl openal pango sdl_ttf libsndfile libxinerama pkg-config

# To install Ruby 1.9
sudo pacman -S ruby
```

## Gentoo Linux (last tested 2013-11-10 with Gosu 0.7.x)

```bash
# Gosu's dependencies for both C++ and Ruby
sudo emerge -atv media-libs/freeglut media-libs/freeimage media-libs/mesa media-libs/openal x11-libs/pango media-libs/sdl-ttf media-libs/libsndfile x11-libs/libXinerama

# To install Ruby 1.9
sudo emerge -atv ruby:1.9
```

## OpenSUSE (last tested on OpenSUSE 13.1 with Gosu 0.8.3)

```bash
# General development tools
sudo zypper install --type pattern devel_basis
# Add the 'games' repository for libfreeimage-devel
sudo zypper addrepo http://download.opensuse.org/repositories/games/openSUSE_12.1/ opensuse-games
# Gosu's dependencies for both C++ and Ruby
sudo zypper install libSDL2-devel libSDL2_ttf-devel pango-devel libfreeimage-devel libsndfile-devel openal-soft-devel libvorbis-devel

# To install the Ruby headers
sudo zypper install ruby-devel

# If you are using rvm or rbenv, do not use 'sudo'
sudo gem install gosu
```

## Compiling Gosu for C++ (last tested with Gosu 0.7.x)

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