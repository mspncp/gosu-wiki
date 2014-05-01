# Getting Started on Raspbian (Raspberry Pi)

In theory, Raspbian is 'just' another Linux distribution. However, its package manager is missing Gosu's (new) main dependency, SDL 2.0. There is a package called `libsdl2-dev` in the Debian Jessie repositories, but it comes without the `RPI` video driver and cannot be used to install Gosu.

You can follow these steps to install Ruby/Gosu anyway:

1. Install Raspbian on an SD card, if you haven't already ([downloads and instructions](http://www.raspberrypi.org/downloads/))

2. In Raspbian, go to the [SDL download page](http://www.libsdl.org/download-2.0.php) and download the latest version in `.tar.gz` format. If you click "Save", it will be downloaded into `/home/pi`, which is what I will assume in the steps below.

3. Open a terminal and run:
    ```bash
    sudo apt-get install ruby ruby-dev build-essential libfreeimage-dev libopenal-dev libpango1.0-dev libsndfile-dev
    ```

4. Now unpack and compile SDL. The last line will take roughly one hour to complete:

    ```bash
    tar zxvf SDL2-2.*.tar.gz
    cd SDL2-2.*
    ./configure --prefix=/opt/SDL2 --disable-video-x11 && make && sudo make install
    ```

5. WIP