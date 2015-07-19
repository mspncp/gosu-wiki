# Getting Started on Linux

Please help us keep this information up-to-date! :)

## Dependencies

To install Gosu 0.8.x on Linux, you will need the following packages, even though the names will be different in every distribution: `libsdl2-dev`, `libsdl2-ttf-dev`, `libpango1.0-dev`, `libgl1-mesa-dev`, `libfreeimage-dev`, `libopenal-dev`, `libsndfile-dev`.

## Ubuntu (last tested on Trusty Tahr (14.10.1), with Gosu 0.8.6)

```bash
# Gosu's dependencies for both C++ and Ruby
sudo apt-get install build-essential libsdl2-dev libsdl2-ttf-dev libpango1.0-dev \
                     libgl1-mesa-dev libfreeimage-dev libopenal-dev libsndfile-dev

# To install Ruby - if you are using rvm or rbenv, please skip this step
sudo apt-get install ruby-dev

# If you are using rvm or rbenv, do not use 'sudo'
sudo gem install gosu
```

See also [this forum thread](http://www.libgosu.org/cgi-bin/mwf/topic_show.pl?tid=1137) for another detailed guide.

## Ubuntu 12.04 (or minor)

Install C++ dependencies not available by default:

### Imagefree

```bash
sudo apt-get install libfreeimage3 libfreeimage-dev
```

### Sndfile

Download link & instructions here: http://www.linuxfromscratch.org/blfs/view/svn/multimedia/libsndfile.html

### SDL2

Sources needed:
+ https://www.libsdl.org/download-2.0.php
+ https://www.libsdl.org/projects/SDL_ttf/
+ https://www.libsdl.org/projects/SDL_image/
+ https://www.libsdl.org/projects/SDL_mixer/

For each source you need to:
+ Download archive
+ Extract archive
+ Compile source (```./configure && make && sudo make install```)

## Manjaro Linux (last tested on 2014-09-02 with Gosu 0.8.3)

```bash
# Gosu's dependencies for both C++ and Ruby
sudo pacman -S freeglut freeimage libegl openal pango sdl2_ttf libsndfile libxinerama pkg-config

# To install Ruby 2.1.2
sudo pacman -S ruby
```

## Fedora (last tested on 21 with Gosu 0.8.6)

```bash
# Gosu's dependencies for both C++ and Ruby
sudo yum groupinstall --assumeyes "Development Tools"
sudo yum install --assumeyes freeglut-devel freeimage-devel mesa-libGL-devel openal-devel pango-devel SDL2_ttf-devel libsndfile-devel libXinerama-devel libvorbis-devel gcc-c++

# To install Ruby
sudo yum install --assumeyes ruby-devel rubygems
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
./create_deb_package.sh
xdg-open build/*.deb
```
On all other systems you can use this to install Gosu - but be aware, there is no uninstall target. Run it inside `build`, after running `make`.

```bash
sudo make install
```

## Using Gosu in C++ with cmake

Have a look at the examples, the example `CMakeLists.txt` are short, commented and straight forward.

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