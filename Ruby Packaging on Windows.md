#summary Ruby Packaging on Windows

[ ![Please post feedback and additions as comments to this page and visit the boards for questions outside the scope of a single wiki page. Thank you!](board_link.png) ][boards]

To compile your Ruby game into an executable on Windows, you need to run it through (this program)[http://github.com/larsch/ocra/tree/master] from the command line.


In theory, it should be as simple as these two lines in a command prompt:

    gem install ocra
    ocra my_ruby_game.rb

If you are using sound, you have to ship `fmod.dll` too. Other gems like `ruby-opengl` might require their own DLLs too. You can put them in a `lib` subdirectory and then include them on the command line:

    ocra my_ruby_game.rb lib\*

To let your game find the DLLs you have to change the PATH environment like this somewhere early in your game:

    ENV['PATH'] = File.join(GAMEROOT,"lib") + ";" + ENV['PATH']

If you have any trouble, feel free to ask on the Gosu boards. Ocra is still a project in development and everybody can benefit from sharing your experience.

If you run into problems with bundling fmod.dll, (please see this thread)[http://www.libgosu.org/cgi-bin/mwf/topic_show.pl?tid=426].

[boards]: http://www.libgosu.org/cgi-bin/mwf/forum.pl "Gosu Boards"
