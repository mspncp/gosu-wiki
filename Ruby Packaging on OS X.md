# Ruby Packaging on OS X

All you have to do to share your game with the public is following these easy steps:

  * Find the most recent Mac app wrapper in [the Gosu downloads](http://www.libgosu.org/downloads/)
  * Open the app's contents via the right-click menu in Finder
  * Edit the Info.plist file, and change at least the bundle identifier.
  * Copy your game files into the `Contents/Resources` subfolder (Gosu libraries are not necessary, they are built in)
  * Rename your game's main source file to `Main.rb`
  * Delete unneeded parts of the Ruby standard library from `Resources/lib`

And you're done! You now have a fully functional .app bundle.

The .app is a self-contained Ruby 1.9 installation with most of the standard library, in case you need it. This means that you have to obey all the rules of Ruby 1.9 if you aren't already, e.g. you need to put comments of the form `# Encoding: UTF-8` on the first line of every source file that uses non-ASCII characters. If you need to use libraries that are not included in the .app, copy them into the `lib` folder. If you need C extensions that are not included in the .app, you should ask on the Extending Gosu board.

## Why bundle a complete Ruby 1.9 installation?

This all may seem overkill because OS X has been shipping with a working installation of Ruby 1.8 for a long time. In fact, Gosu has tried to use it with a very lightweight wrapper. But:

  * Ruby 1.9 is much faster and it shows in game development.
  * If the next OS version ships with Ruby 1.9, your .app will break if it contains C extensions built for 1.8.
  * Even minor system upgrades may break your .app overnight. Patchlevel upgrades to Ruby 1.8.6 have broken Gosu and other binary gems before. The Ruby development process is too fuzzy to rely upon.