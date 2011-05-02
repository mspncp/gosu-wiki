# To Do list

This list of tasks is exported automatically from my OmniFocus projects.
(Last update: 2011-05-02)

## Gosu 0.7.x
  * Make retrofication available in C++
  * Protect ALL Window callbacks & add call to close() in case of an error
  * See if image\_insert.rb works on iMac
  * Add Gosu::copyright()
  * Move GOSU\_VERSION into a Ruby file and out of SWIG
  * Throw exception for '' as a font name
  * Throw exception for multiple windows
  * Add Gosu::potential\_fps
  * Release 0.7.32
  * Start working on 0.8 interface… Reshuffle all tasks below this
  * Release a roadmap for 0.7, 0.8 & 0.9
  * Compare RubyGosu.app to https://github.com/steveklabnik/furoshiki
  * Use 10.4 SSH to compile truly universal RubyGosu App \o/
  * Get GLFW working on OS X
  * Get GLFW working on Linux
  * Try audio formats with Audiere
  * Find out what Gosu::Song::play does when it's already playing on all three platforms, then clarify docs
  * Add FontFlags support for SDL\_TTF Gosu/Text
  * Fix Unicode support for SDL\_TTF port (see feature\_tests/UnicodeTest.rb, @loc\_test)
  * Fix exceptions being turned into segfaults on Linux (see GoogleCode issue)
  * See if clipping coordinate calculation is correct with all transformations considered (why is Terava off by one pixel?)
  * Test Gosu&ocra with audiere.dll
  * See why Gosu::~Song with Ogg files sometimes causes other songs to stop
  * Ensure that Gosu::Song: currentSong is never 0'ed asynchronously (who is setting that variable anyway? Me right?)
  * Add m4a to audio\_formats.rb
  * Make <c=> more efficient in Font::drawRel
  * Add <s=> to text formatting
  * Make fuchsia work in BMPs in GosuTouch
  * See if I should fork out RubyGosu.app into Ruby App project
  * Gosu: try integer truncing of drawing positions
  * Remove setResolution and use transforms instead
  * Windows: Improve shrinking heuristics (get task bar size)
  * WindowX: add shrinking for oversized resolutions
  * Use Gosu text formatting in Tutorial.rb
  * Throw an exception when using multiple Windows
  * Make C++'s Gosu::multiply available to Ruby
  * Add Numeric#clamp, Numeric#wrap to Ruby
  * Test StandBy with Windows and a running Gosu app
  * See if really old games have problems running in current Gosu
  * The screen size/OpenGL stuff …
    * See if John Shea's talk had something about not being locked to pixel positions
    * Make initial window black instead of garbled on OS X (if it persists with glfw)
    * Screen size / fullscreen stuff
      * Iterate on first category of fullscreen tests
      * Add fullscreen accessors to make proper FS OpenGL possible
      * Add fullscreen stretching prevention
      * Re-Evaluate glfw for fixing the fullscreen mess
      * Think about adding cmd+F support for toggling fullscreen: Possible?
      * Think about adding alt+enter support for toggling fullscreen: Possible?
      * Try not to hide the mouse cursor outside of the main window on OS X
      * Test multiple screens on Windows
    * TextField with clip\_to (update example)
  * Make Gosu fun to use on OS X
    * Create C++ app template for Xcode
    * Create iPhone app template for Xcode
    * Create .pkg wrapper to install Gosu into /Developer/Gosu
  * More OpenAL niceties
    * See if there is a native/fastest mixing rate on Mac/iPhone
    * Make buffers in Mac port larger and make sure that update\_interval<66 always plays running Songs without jitter
  * Try harder to reproduce these bugs
    * Get rid of context selection error with driver set to always do FSAA (Windows)
    * OS X: Release all keys on battery notification dialog (?)
  * Finish the RMagick bundling thing
    * See what's new with ImageMagick, apparently there is a universal conf flag?!
    * Try to build RMagick.bundle against the 10.4 SDK
    * Link the all-in-one-bundle from the boards: http://rubyforge.org/forum/forum.php?thread\_id=26872&forum\_id=32
    * Test RMagick.bundle on Tiger
    * Test RMagick.bundle on PPC
  * Replace draw\_line by something that makes sense
  * Text quality
    * Implement ffUnderline by hand in createText/Font
    * Creating a non-existent font should throw an exception on all platforms, test on which it does
    * Font should respect monospaced fonts and fonts with very weird kerning (Zapfino...): do research
    * Verify that Daniel font works properly in Font and Text
    * Linux: Support other XKeySyms than Latin 1
    * Mac: Add dead keys to TextInput
    * Mac: Use Core Text instead of ATSUI
  * Polish/deployment
    * Make it possible to delete images while they are still referenced in the queue.
    * Make Gosu::Color more tolerant regarding its component values
    * Assure that files from doxygen task are considered for packaging
    * Compile all-in-one RMagick for Windows: http://rubyforge.org/forum/forum.php?thread\_id=26872&forum\_id=32
    * Get rid of quad/tri drawing in favor of textures
    * Review: http://rubyforge.org/tracker/index.php?func=detail&aid=21405&group\_id=375&atid=1504
    * Make sure README and LICENSE are appropriately named in the Gem
    * Collect Gosu YouTube videos and link them prominently
    * Create a dynamic screenshot page for all the topics in the Showcase
    * Mac OS: Mauszeiger wird im FS sichtbar bei Klick in obere linke Ecke: Warum?
    * Make examples discoverable
    * Deployment-Hilfe, Rakefile, Mac
    * Deployment-Hilfe, Rakefile, Win
    * Retry properly showing/hiding the mouse on OS X (immune to blocking main thread)
    * Make the wrapper's menu bar on OS X more complete
    * Now that the Rakefile works, stop doing every task every time (use file dependencies)
    * Make it easier to find the examples from the Gem
  * Re-introduce Async support
  * Look at http://freeimage.sourceforge.net/requirements.html
  * Look at http://slick.cokeandcode.com/index.php?entry=entry080426-213044
  * Experiment: resizing the window possible?
  * More alpha modes! http://www.adobe.com/devnet/pdf/pdfs/blend\_modes.pdf
  * Document Gosu::interpolate, improve it too?
  * Think: Possible to have beautiful quotation mark indenting?@Gosu Text
  * See if other libraries catch the release of the 'A' key in cmd+a
  * Add check for Caps Lock/Num Lock
  * KbBracketLeft and KbBracketRight for ÖÄ?
  * Make more stuff configurable like http://github.com/cout/rice/blob/98ba7098e2de5849f2e7272021340976a768456f/ruby.ac#L7-20
  * Try and see if Gosu can be made to correctly release pushed buttons when the keyboard is overloaded
  * Fix error when creating an Image from "\n" on OS X
  * Add callback for the OS-supplied "close" button
  * Correctly implement render-to-texture (render{})
  * Try to understand the benchmark on stackoverflow
  * Make MacUtility.hpp public
  * Fix attached example program
  * @ivar to Sample in SampleInstance, to Image in GLTexInfo to prevent GC desasters
  * Find out why glGetError apparently returns an error in Gosu (where? why?)
  * Image::insert/Bitmap::insert should memcpy if possible
## Gosu Touch
  * See if [UIScreen scale] really gives us a hint about zooming on the iPad - and if so, tell the user to STOP IT man!
  * Compare with OolongEngine for audio issues
  * See if xiph Tremor makes sense for Gosu Touch
  * Let resolution decide orientation
  * Integrate "fat" iPhone building from forum
  * Clear up GOSU\_IS\_MAC vs. GOSU\_IS\_OSX
  * Migrate WindowTouch.mm to CADisplayLink (3.1 SDK)
  * Make sure that iPhone VA vertices are small and well-aligned
  * Use getBytes instead of UTF8String
  * Testen, ob nicht alles besser ist, wenn ich graphics width/height die echten Daten des iPhone4 liefern lasse
  * Fix music stopping after locking the screen for a long time
  * Fix too-many-Fingers-bug
  * Unify drawQuad's effective triangularization on iOS and desktop
  * Try to compile FreeGemas for iOS
## Gosu CI/Usability
  * Document 64px minimum for reliable single-texture optimization
  * Mention Gosu's respectable age somewhere :)
  * Link to benkos example & Chingu regarding states
  * Put RubyTutorial into rdoc
  * Add some first eye catchers to front page
  * Add "What now?" link list to front page
  * Emphasize difference between button\_down and button\_down? somewhere
  * Link YouTube videos, and maybe blog tags like http://www.cuberick.com/search/label/gosu?
  * Make logo in forum clickable
  * Make logo in Rdoc clickable
  * Add OpenGL Wiki page
  * Add Unicode Support wiki page
  * Deployment wiki page/rdoc: Mention Icon resource support!
  * UTF8 Support for PotD texts(?)
  * Donate to allison's author
  * Explain SampleInstance vs. Sample somewhere
  * OR&G: Build simpler version
  * Check if DelphiGL wiki accepts donations
  * Tutorials: Mention where to find the final source code
  * Document MAX\_TEXTURE\_SIZE
  * .app'ify ippa's game after :retrofy is in and the wrapper can handle texplay
  * Consider libgosu.spreadshirt.com
  * Make sure that it is documented what happens to different drawing ops with same z-order
  * Update README.txt and website year
  * Include CptnCpp as sample game
  * Document alpha modes for Ruby
  * Add rdoc to Gosu gem
  * Make sure that WindowMainLoop states that the whole order is just about perceived performance
  * Document how Font roughly works (allow devs to cache chars by text\_width'ing the alphabet)
  * Say "you can attach files after posting" below input box in board
  * Fix download for all my LD games as soon as Mac wrapper is nicer :(
  * Point out that Font#text\_width is only relevant to Font#draw etc
  * Link to the FMOD MP3 licensing info page (or the page it refers to) publicly for MP3 clarification
  * Note: changing looping may restart song—clarify this? (audiere)
  * Insert http://www.libgosu.org/cgi-bin/mwf/default/nav\_up.png
  * Fix doxygen's fugliness (what's up there?!)
  * Refresh SupportedAudioFormats on Linux
## Gosu 0.8.x (preliminary)
  * Rename gl\_tex\_info to gl\_info and make it an array for Image
  * Rename needs\_x? to need\_x? in Ruby
  * Change color constant format
  * Let Image() lazy-load its file using Gosu::File (which keeps the file alive until it is really needed), add Gosu::loading\_progress and Gosu::load\_more for easy loading bars
  * Make Window::needsCursor return true by default for Windowed games
  * Make Image, Sample, Song, Font use an intrusive\_ptr internally
  * Make things tileable by default but add :smooth and :pure or something like that
  * Add :padding=>N argument to constructor for mega zooming without problems
  * Experimentation: In Ruby, can the window be a singleton and still provide the ability to inherit from it? (Singleton standard class)
  * Use float instead of double everywhere (see note)
  * Rename pimpl/Impl to p/Private
  * Add accelerometer support for OS X; maybe find a way to use UniMotion
  * Redesign (see forum) drawing interface
  * Rewrite Gosu::Input with support for multiple gamepads and analog joysticks, serializable button IDs, …
  * Windows: Input will regularly query devices which are not currently attached, thereby causing the game to halt every few seconds - think about this
  * FSAA/mipmap experiments
  * Provide C++ application templates where possible, maybe even installers for the templates
  * Apple remote support would rule.
  * Assure Gosu::File also creates directories as necessary
  * more C++ examples
  * simplify Gosu's IO philosophy (C++)
  * document Gosu's Sockets
  * Gosu::Scope instead of beginGL/endGL etc.
  * Change ImageData::toBitmap to toBlob(byte*, size\_t) and copy directly in RSTRING; add Image::toBitmap() instead
  * Remove the "from\_" from "from\_hsv" and "from\_ashv", and deprecate Color#initialize
  * Deprecate Image::getData, introduce Image::data
  * Experimentation with new drawing syntax
  * Make plans for an official Scene/State system
  * If there ever is functionality to 'and' and 'or' Gosu::Button, how would one check in buttonDown?
  * Deprecate beginGL/endGL in favor of scheduleGL
  * Add QuickLook support to image loading on 10.5+ via QLThumbnailImageCreate :D
  * Add Gosu::StringArg (a variant of char*/wchar*/string/wstring)
  * How would a TexturePacker like thingie work for Gosu?
  * Order USB devices alphabetically (so gamepad 0 is always 0)
  * Rename SampleInstance to Channel
