Getting Started on the Raspberry Pi
Pre-release version of Gosu 0.8.0

Gosu 0.8.0 uses SDL 2.0 as its backend, which at the same time makes Gosu a lot more portable and light-weight.

If you want to install the pre-release version of Gosu 0.8.x on Linux, you will need the following packages: build-essential, libfreeimage-dev, libopenal-dev, libpango1.0-dev, libsdl2-dev, libsdl2-ttf2.0-dev, libsndfile-dev. (Successfully tested on Ubuntu 14.04)

On Raspbian, there is no package for SDL 2.x. However, you can extract the source tarball from libsdl.org and then run ./configure && make && sudo make install to install it. Afterwards you can install the --pre gem as on other Linux distributions.

Note: Please edit this wiki page if you know how to install SDL 2 in a better place than /usr/local and have Gosu find it

Note: There is a libsdl2-dev package in the 'jessie' testing repository, but it is useless as it does not come with the RPI video driver