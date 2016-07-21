# Getting Started on Linux

Please help us keep this information up-to-date! :)

## Dependencies

To install Gosu 0.8.x on Linux, you will need the following packages, even though the names will be different in every distribution: `libsdl2-dev`, `libsdl2-ttf-dev`, `libpango1.0-dev`, `libgl1-mesa-dev`, `libfreeimage-dev`, `libopenal-dev`, `libsndfile-dev`.

## Ubuntu (last tested on Xenial Xerus (16.04), with Gosu 0.10.6) / Linux Mint (last tested on Linux Mint 17.3)

```bash
# Gosu's dependencies for both C++ and Ruby
sudo apt-get install build-essential libsdl2-dev libsdl2-ttf-dev libpango1.0-dev \
                     libgl1-mesa-dev libfreeimage-dev libopenal-dev libsndfile-dev

# To install Ruby - if you are using rvm or rbenv, please skip this step
sudo apt-get install ruby-dev

# If you are using a Ruby version manager (i.e. : rvm or rbenv)
gem install gosu
# otherwise, you can add "sudo" at the beginning of the command
sudo gem install gosu

```

See also [this forum thread](http://www.libgosu.org/cgi-bin/mwf/topic_show.pl?tid=1137) for another detailed guide.

## Ubuntu 12.04 (or below)

Install C++ dependencies not available by default:

### Sndfile

Download link & instructions here: http://www.linuxfromscratch.org/blfs/view/svn/multimedia/libsndfile.html

### SDL 2

Sources needed:
+ https://www.libsdl.org/download-2.0.php
+ https://www.libsdl.org/projects/SDL_ttf/

For each source you need to:
+ Download archive
+ Extract archive
+ Compile source (```./configure && make && sudo make install```)

## Debian 8 with Nvidia GPU

Please see [this post on the Gosu forum](https://www.libgosu.org/cgi-bin/mwf/topic_show.pl?pid=8476#pid8476) if you run into trouble installing Gosu, or anything else that uses OpenGL.

## Manjaro Linux (last tested on 2014-09-02 with Gosu 0.8.3)

```bash
# Gosu's dependencies for both C++ and Ruby
sudo pacman -S freeglut freeimage libegl openal pango sdl2_ttf libsndfile libxinerama pkg-config

# To install Ruby 2.1.2
sudo pacman -S ruby
```

## Fedora (last tested on 23 with Gosu 0.10.4)

```bash
# Gosu's dependencies for both C++ and Ruby
sudo dnf groupinstall --assumeyes "Development Tools"
sudo dnf install --assumeyes freeglut-devel freeimage-devel mesa-libGL-devel openal-devel pango-devel SDL2_ttf-devel libsndfile-devel libXinerama-devel libvorbis-devel gcc-c++ redhat-rpm-config

# To install Ruby
sudo dnf install --assumeyes ruby-devel rubygems
```

## Arch Linux (last tested on 2014-12-09 with Gosu 0.8.x)

```bash
# Gosu's dependencies for both C++ and Ruby
sudo pacman -S freeglut freeimage libegl openal pango sdl_ttf libsndfile libxinerama pkg-config sdl2_ttf sdl2

# To install Ruby
sudo pacman -S ruby
```

## Gentoo Linux (last tested 2014-11-09 with Gosu 0.8.x)

```bash
# Gosu's dependencies for both C++ and Ruby, ensure you have the 'opengl' USE Flag set globally or at least for media-libs/libsdl2.
sudo emerge -av media-libs/freeglut media-libs/freeimage media-libs/mesa media-libs/openal x11-libs/pango media-libs/sdl2-ttf media-libs/libsndfile x11-libs/libXinerama

# To install Ruby
sudo emerge -av dev-lang/ruby
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

## Compiling Gosu for C++

To compile Gosu, `cd` into the `cmake` subdirectory and run:

```bash
mkdir -p build
cd build
cmake ..
make
```

If you are using Debian/Ubuntu, you can use this to install Gosu:

```bash
cd ..
./create_deb_package.sh
sudo dpkg -i libgosu-dev-0.10.7-Linux.deb
```
On all other systems you can use this to install Gosu - but be aware, there is no uninstall target. Run it inside `build`, after running `make`.  Warning:  This puts the object files in a different spot on the system and can cause problems when building a Gosu-based project with the `-lgosu` option passed to g++.

```bash
sudo make install
```

## Using Gosu in C++ with CMake

Have a look at the examples. The example `CMakeLists.txt` are short, commented and straight forward, and can be used as a starting point for your own Gosu C++ games:

https://github.com/gosu/gosu/blob/master/examples/Tutorial/CMakeLists.txt

## Using Gosu in C++ without CMake

(The following assumes that you have installed Gosu system-wide. Note: This hasn't been tested in a while...)

You have to compile with `` `pkg-config --cflags gosu` `` and `` `pkg-config --libs gosu` ``, so a simple Makefile could look like this:

```make
OBJS = main.o player.o
CXXFLAGS += `pkg-config --cflags gosu`
LIBS = `pkg-config --libs gosu`

myGame: $(OBJS)
        g++ -o myGame $(OBJS) libgosu.a $(LIBS)
```