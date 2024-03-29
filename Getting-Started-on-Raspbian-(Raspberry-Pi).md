# Getting Started on Raspbian (Raspberry Pi)

_Note: This guide only applies to the original Raspberry Pi and the Raspbian Linux distribution. If you use a Raspberry Pi 2 or 3, please [enable OpenGL](http://www.geeks3d.com/20160209/raspberry-pi-new-version-of-raspbian-jessie-with-opengl-2-1-support/) and then follow the ‘normal’ instructions for Ubuntu/Debian here: [[Getting Started on Linux]]. Please also install Gosu using `sudo gem install gosu --pre` for now; the current stable version will not work._

In theory, Raspbian is 'just' another Linux distribution. However, its package manager is missing Gosu's (new) main dependency, SDL 2. There is a package called `libsdl2-dev` in the Debian Jessie repositories, but it comes without the `RPI` video driver and cannot be used to install Gosu.

You can follow these steps to install Ruby/Gosu anyway:

1. Install Raspbian on an SD card, if you haven't already ([downloads and instructions](http://www.raspberrypi.org/downloads/))

2. In Raspbian, go to the [SDL 2 download page](http://www.libsdl.org/download-2.0.php) and download the latest version in `.tar.gz` format. If you click "Save", it will be downloaded into `/home/pi`, which is what I will assume in the steps below.

3. Also download the latest version of [SDL_ttf](https://www.libsdl.org/projects/SDL_ttf/) into the same directory.

3. Open a terminal and run:
    ```bash
    sudo apt-get install ruby ruby-dev build-essential libfreeimage-dev libopenal-dev libpango1.0-dev libsndfile-dev libudev-dev libasound2-dev
    ```

4. Unpack and compile SDL 2. This will take roughly one hour to complete:

    ```bash
    tar zxvf SDL2-2.*.tar.gz
    cd SDL2-2.*
    ./configure --prefix=/opt/SDL2 --disable-video-x11
    make
    sudo make install
    ```

    If you are already using *Raspbian Jessie*, try this variant of the `./configure` command instead:

    ```bash
    ./configure --host=armv7l-raspberry-linux-gnueabihf --disable-pulseaudio --disable-esd --disable-video-mir --disable-video-wayland --disable-video-x11 --disable-video-opengl
    ```

5. Unpack and compile SDL_ttf. This shouldn't take nearly as long.

    ```bash
    cd
    tar zxvf SDL2_ttf-2.*.tar.gz
    cd SDL2_ttf-2.*
    ./configure --prefix=/opt/SDL2 && make && sudo make install
    ```

6. Install Gosu with the following command:

   ```bash
   sudo gem install gosu -- --with-cflags=-I/opt/SDL2/include/SDL2 --with-cppflags=-I/opt/SDL2/include/SDL2 --with-ldflags=\"/opt/SDL2/lib/libSDL2.a /opt/SDL2/lib/libSDL2_ttf.a\"
   ```

7. Optional: Run the example games to verify that everything works.

   ```bash
   sudo gem install gosu-examples
   gosu-examples --fullscreen
   ```

8. Optional: Clean up by deleting the SDL folders and `.tar.gz` files in your home directory.

Congratulations, you should now be able to run Ruby/Gosu games!

*Note:* One unresolved issue in Raspbian is that games started from a terminal will leak keystrokes into the terminal, and you might accidentally trigger commands while playing games ([#213](https://github.com/gosu/gosu/issues/213)).
You can use [this handy tool](https://github.com/inoremap/shut-term-keys) to prevent this from happening.

*Note:* It is best to run all games in fullscreen mode on Raspbian, since windowed mode does not work as expected.