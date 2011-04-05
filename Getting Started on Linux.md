# Getting Started on Linux

(or FreeBSD, as I am told!)

[ ![Please post feedback and additions as comments to this page and visit the boards for questions outside the scope of a single wiki page. Thank you!](board_link.png) ][boards]

## Dependencies

To install Gosu in any form, you will need the following packages (install via `sudo apt-get install <packagename>`):

  * g++
  * libgl1-mesa-dev
  * libpango1.0-dev
  * libboost-dev
  * libsdl-mixer1.2-dev
  * libsdl-ttf2.0-dev


*Copy-and-pastable command line* for Ubuntu, last tested on 10.10, should work across all versions:

    # For C++
    sudo apt-get install g++ libgl1-mesa-dev libpango1.0-dev libboost-dev libsdl-mixer1.2-dev libsdl-ttf2.0-dev
    # To install the gem for Ruby 1.8
    sudo apt-get install g++ libgl1-mesa-dev libpango1.0-dev libboost-dev libsdl-mixer1.2-dev libsdl-ttf2.0-dev ruby1.8-dev
    # To install the gem for Ruby 1.9.1/1.9.2(?)
    sudo apt-get install g++ libgl1-mesa-dev libpango1.0-dev libboost-dev libsdl-mixer1.2-dev libsdl-ttf2.0-dev ruby1.9.1-dev

*Please check* how to install all this software if you are on a different distribution.

## Ruby Gem

If you are only interested in using Gosu with the Ruby programming language, you can install it as a Ruby gem via `sudo gem install gosu`. You need to install the packages from above.

Afterwards, `gem install gosu` should work.

## Compiling Gosu for C++

To compile Gosu, `cd` into the `linux` subdirectory and run:

    ./configure
    make

There is a deprecated 'make install' command that will work for C++, but as most Linux distributions are using a package manager nowadays we recommend copying the resulting `linux/libgosu.a` file to your game's directory manually.

## Using Gosu in C++

(The following assumes that you have installed Gosu system-wide via `sudo make install`. If not, you will have to add paths as necessary.)

You have to compile with ``gosu-config --libs``` and -Igosu ```gosu-config --cxxflags``, so a simple Makefile could look like this:

    OBJS = main.o player.o
    CXXFLAGS += `gosu-config --cxxflags`
    LIBS = -lgosu `gosu-config --libs`

    myGame: $(OBJS) libgosu.a
            g++ -o myGame $(OBJS) libgosu.a $(LIBS)

[boards]: http://www.libgosu.org/cgi-bin/mwf/forum.pl "Gosu Boards"