# Getting Started on Linux

Please help us keep this information up-to-date! :)

## Dependencies

To install and use Gosu on Linux, you need the following packages (the names will be slightly different in every distribution):

`libsdl2-dev`, `libgl1-mesa-dev`, `libopenal-dev`, `libsndfile-dev`, `libmpg123-dev`, `libgmp-dev`, `libfontconfig1-dev`

## Ubuntu (last tested on Ubuntu 18.04 with Gosu 0.14.5) / Linux Mint (last tested on Linux Mint 17.3) / elementary OS

```bash
# Dependencies for both C++ and Ruby
sudo apt-get install build-essential libsdl2-dev libgl1-mesa-dev libopenal-dev \
                     libsndfile-dev libmpg123-dev libgmp-dev libfontconfig1-dev

# To install Ruby itself - if you are using rvm or rbenv, please skip this step
sudo apt-get install ruby-dev

# If you are using a Ruby version manager (i.e. rvm or rbenv)
gem install gosu
# If you are using system Ruby, you will need "sudo" to install Ruby libraries (gems)
sudo gem install gosu
```

See [this forum thread](http://www.libgosu.org/cgi-bin/mwf/topic_show.pl?tid=1137) for another detailed guide.

## Debian 8 with Nvidia GPU

Please see [this post on the Gosu forum](https://www.libgosu.org/cgi-bin/mwf/topic_show.pl?pid=8476#pid8476) if you run into trouble installing Gosu or anything else that uses OpenGL.

## Arch Linux/Manjaro (last tested on 2016-04-26 with Gosu 0.12.0)

```bash
# Gosu's dependencies for both C++ and Ruby
sudo pacman -S openal pango sdl2 sdl2_ttf libsndfile pkg-config mpg123

# To install Ruby
sudo pacman -S ruby
```

## Fedora (last tested on Fedora 30 with Gosu 0.14.5)

```bash
# Gosu's dependencies for both C++ and Ruby
sudo dnf groupinstall --assumeyes "Development Tools"
sudo dnf install --assumeyes mpg123-devel mesa-libGL-devel openal-devel libsndfile-devel gcc-c++ redhat-rpm-config SDL2-devel

# To install Ruby
sudo dnf install --assumeyes ruby-devel rubygems

# Install Gosu
gem install gosu
```

## Gentoo Linux (last tested 2017-11-14 with Gosu 0.12.1)

```bash
# Gosu's dependencies for both C++ and Ruby.
# Ensure you have the 'opengl' USE flag set globally or at least for media-libs/libsdl2.
sudo emerge -av media-libs/mesa media-libs/openal media-libs/libsndfile media-sound/mpg123

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
sudo zypper install libSDL2-devel libsndfile-devel openal-soft-devel

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

Have a look at the examples. The example `CMakeLists.txt` are short, commented and straightforward, and can be used as a starting point for your own Gosu C++ games:

https://github.com/gosu/gosu/blob/master/examples/Tutorial/CMakeLists.txt

## Using Gosu in C++ without CMake

(The following assumes that you have installed Gosu system-wide. Note: This hasn't been tested in a while.)

You have to compile with `` `pkg-config --cflags gosu` `` and `` `pkg-config --libs gosu` ``, so a simple Makefile could look like this:

```make
OBJS = main.o player.o
CXXFLAGS += `pkg-config --cflags gosu`
LIBS = `pkg-config --libs gosu`

myGame: $(OBJS)
        g++ -o myGame $(OBJS) libgosu.a $(LIBS)
```