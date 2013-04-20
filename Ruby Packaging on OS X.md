# Ruby Packaging on OS X

Do you want to share your game with other Mac users? Simply follow these steps:

  * Find the most recent Mac app wrapper in [the Gosu downloads folder](http://www.libgosu.org/downloads/)
  * Show the app’s package contents via the right-click menu in Finder
  * Edit the Info.plist file, and change the bundle identifier to match your game (`org.libgosu.UntitledGame` by default)
  * Copy your game files into the `Contents/Resources` subfolder
  * Rename your game’s main source file to `Main.rb`

And you’re done! You should now have a fully functional .app bundle.

The .app is a self-contained Ruby 1.9 installation with most of the standard library plus a few libraries that are often used together with Gosu.

## Using Releasy

There is a relatively new gem that can handle the packaging for you:

https://github.com/Spooner/releasy/

It really does nothing else than to automate the process outlined above.

## Troubleshooting

  * If the app does not start, the OS X Console app is your friend. Open it using Spotlight, start your game and look for any errors that appear.
  * If Console does not show enough information, open a Terminal and `cd` into the same directory in which the `.app` file is located. Then run `YourGame.app/Contents/MacOS/RubyGosu\ App`.
  * If it seems that everything is correct, but the app still does not start, try compressing it into a `.zip` file, deleting the `.app`, and unpacking the `.zip` file again. This will force OS X to forget any information that it may have cached about the app. (This is sometimes necessary for OS X to recognise changes made to the `Info.plist` file.)
  * Note that the app bundles Ruby 1.9, not 1.8 or 2.0. For example, Ruby 1.9 requires a comment `# Encoding: UTF-8` on the first line of every source file that uses non-ASCII characters.
  * Using bundler is a little hairy because the structure of the `.app` folder predates it. You might need to ask on the forum, or use `releasy` which understands bundler.
  * If you need to use libraries that are not included in the .app, copy them into the `lib` folder. If you need C extensions that are not included in the .app, you should ask on the Extending Gosu board.
