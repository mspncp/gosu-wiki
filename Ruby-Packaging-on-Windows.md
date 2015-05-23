# Ruby Packaging on Windows

To compile your Ruby game into an executable on Windows, you can manually use [Ocra](http://github.com/larsch/ocra/) on the command line. The new & awesome (but still experimental way) is to use Spooner's [Releasy](https://github.com/Spooner/releasy/) - see the documentation there.

In theory, ocra should be as simple as these two lines in a command prompt:

    gem install ocra
    ocra my_ruby_game.rb

Other gems like `chipmunk` and `opengl` might require their own DLLs too. You can put them in a `lib` subdirectory and then include them on the command line:

    ocra my_ruby_game.rb lib\*

To let your game find the DLLs, you have to change the `PATH` environment variable like this somewhere early in your game:

    ENV['PATH'] = File.join(GAMEROOT, "lib") + ";" + ENV['PATH']

If you have any questions, feel free to ask on the Gosu boards.