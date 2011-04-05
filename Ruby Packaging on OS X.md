#summary How to wrap up Ruby/Gosu games for deployment on Mac OS X.

[ ![Please post feedback and additions as comments to this page and visit the boards for questions outside the scope of a single wiki page. Thank you!](board_link.png) ][boards]

The Mac package of Gosu (on the Downloads list) comes with a mysterious `RubyGosu App.app` bundle. All you have to do to share your game with the public is following these easy steps:

  * Duplicate this bundle, open its contents via the right-click menu
  * Edit the Info.plist file, and change at least the bundle identifier.
  * Copy your game files into the `Contents/Resources` subfolder (Gosu libraries are not necessary, they are built in)
  * Rename your game's main source file to `Main.rb`

And you're done! You now have a fully functional .app bundle.

The .app is a self-contained Ruby 1.9.2 (core) installation. This especially means that you need to put comments of the form `# Encoding: UTF -8` on the first line of every source file that uses non-ASCII characters. If you need to use libraries other than Ruby's core and Gosu, see the Extending Gosu forum for advice.

*Update:* Sadly the results will only work on 10.6 right now. (See this forum thread for details)[http://www.libgosu.org/cgi-bin/mwf/topic_show.pl?tid=456].

[boards]: http://www.libgosu.org/cgi-bin/mwf/forum.pl "Gosu Boards"