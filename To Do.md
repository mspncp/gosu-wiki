# To Do list

This list of tasks is exported automatically from my OmniFocus projects.
(Last update: 2011-12-08)

## Gosu 0.8.x
  * Understand and merge tuiq's commit
  * Fix base transform being reset
  * Try to fix loadTiles alpha problem by another applyColorKey(0x00\_00\_00\_00)?
  * Test if Carmack's allocation algorithm can handle deallocation well enough
  * Come up with a nice memory union of DrawOp and ArrayVertex
  * Add special case: Macro::draw in record{} must split up the old Macro again (whew...)
  * Make record/transforms superficially independent of Window
  * See if Gosu can be made to use BGRA again because it is apparently faster on OSX/iOS
  * Look into Windows DLL issue (release hotfix gem if possible)
  * Get rid of quad/tri drawing in favor of quads
  * Release 0.8.0a1 --pre
  * Use float instead of double
  * Use int instead of unsigned
  * Consider using new color literal format now
  * Cleanup glBegin, Graphics::begin etc.
  * Release 0.8.0a2 --pre
  * Fork Gosu.tmbundle into its own git repository
  * Fork website into its own git repository
  * Fork RubyGosu.app into its own git repository
  * Fix Gosu::Font(…default, 20) with italics on Windows (see forum thread)
  * Add more #inspect strings (easier to use with irb/Pry)
  * Until first public version (which may break C++)…
    * Make things tileable by default but add :smooth and :pure or something like that
    * Rename needs\_x? to need\_x? in Ruby
    * Make MacUtility.hpp public
    * Adjust Text Entities to line height
    * Add Gosu::StringArg (a variant type of char*/wchar*/string/wstring)
    * Consequently throw exception for invalid font names
    * Throw exception for multiple windows
    * Kill beginGL/endGL in favor of scheduleGL
    * Rename pimpl/Impl to p/Private
    * Order USB devices alphabetically (so gamepad 0 is always 0)
    * Rename SampleInstance to Channel
    * Remove the "from\_" from "from\_hsv" and "from\_ashv", and deprecate Color#initialize
    * Deprecate Image::getData, introduce Image::data
    * Make Window::needsCursor return true by default
    * Rename all those Ruby examples and feature\_tests
    * Change ImageData::toBitmap to toBlob(byte*, size\_t) and copy directly in RSTRING; add Image::toBitmap() instead
  * Release 0.8.0
  * Get GLFW working on OS X
  * Get GLFW working on Linux
  * Make Image, Sample, Song, Font, Texture use an intrusive\_ptr internally (frees Texture from lots of args)
  * Experimentation: In Ruby, can the window be a singleton and still provide the ability to inherit from it? (Singleton standard class)
  * Add accelerometer support for OS X; maybe find a way to use UniMotion
  * Windows: Input will regularly query devices which are not currently attached, thereby causing the game to halt every few seconds - think about this
  * FSAA/mipmap experiments
  * Provide C++ application templates where possible, maybe even installers for the templates
  * Assure Gosu::File also creates directories as necessary
  * more C++ examples
  * document Gosu's Sockets
  * Look at wox-Gem to refactor rake/mac.rb
  * Font#draw with given block that yields each character's Gosu::Image, x, and y to a block, rather than drawing them
  * Find out why this could happen: 'RuntimeError: While calculating the width of a text, the following error occured: The operation completed successfully.'
  * Add Gosu::potential\_fps
  * See if image\_insert.rb works on iMac
  * Fix Song#volume with short songs
  * Compare RubyGosu.app to https://github.com/steveklabnik/furoshiki
  * Check if every SWIG C++ exception causes the segfault on Linux (alternatively, it is likely Gosu's fault!)
  * Try audio formats with Audiere
  * Find out what Gosu::Song::play does when it's already playing on all three platforms, then clarify docs
  * Add FontFlags support for SDL\_TTF Gosu/Text
  * Fix Unicode support for SDL\_TTF port (see feature\_tests/UnicodeTest.rb, @loc\_test)
  * Fix exceptions being turned into segfaults on Linux (see GoogleCode issue)
  * See if clipping coordinate calculation is correct with all transformations considered (why is Terava off by one pixel?)
  * Ensure that Gosu::Song: currentSong is never 0'ed asynchronously (who is setting that variable anyway? Me right?)
  * Make <c=> more efficient in Font::drawRel
  * Add <s=> to text formatting
  * Gosu: try integer truncing of drawing positions
  * Remove setResolution and use transforms instead
  * Windows: Improve shrinking heuristics (get task bar size)
  * WindowX: add shrinking for oversized resolutions
  * Use Gosu text formatting in Tutorial.rb
  * Make C++'s Gosu::multiply available to Ruby
  * Add Numeric#clamp, Numeric#wrap to Ruby
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
    * Create C++ app template for Xcode4
    * Create iPhone app template for Xcode4
    * Create .pkg wrapper to install Gosu into /Developer/Gosu
  * Make OpenAL  buffers in Mac port larger and make sure that update\_interval<66 always plays running Songs without jitter
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
    * Assure that files from doxygen task are considered for packaging
    * Review: http://rubyforge.org/tracker/index.php?func=detail&aid=21405&group\_id=375&atid=1504
    * Make sure README and LICENSE are appropriately named in the Gem
    * Make the wrapper's menu bar on OS X more complete
    * Now that the Rakefile works, stop doing every task every time (use file dependencies)
  * Make examples discoverable
  * Retry properly showing/hiding the mouse on OS X (immune to blocking main thread)
  * Mac OS: Mauszeiger wird im FS sichtbar bei Klick in obere linke Ecke: Warum?
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
  * @ivar to Sample in SampleInstance, to Image in GLTexInfo to prevent GC desasters
  * Image::insert/Bitmap::insert should memcpy if possible
  * Expose Gosu Directories in Ruby
  * Rename maxWidth argument to width in createText
  * Document Text Entities
  * COMMON\_CPP\_FILES in Rakefile should contain the headers!
  * Fix: Mouse position on Linux is always reported to be inside the window
  * Use big texture for LargeImage if possible
  * Add better error message for missing files on Linux/FreeImage
  * See if this page helps with fullscreen on OS X
  * Apply colorKey AFTER splitting the bitmap into tiles, not before!
## Gosu 0.9.x+
  * Redesign (see forum) drawing interface
  * Rewrite Gosu::Input with support for multiple gamepads and analog joysticks, serializable button IDs, …
  * simplify Gosu's IO philosophy (C++)
  * Make plans for an official Scene/State system
  * Add QuickLook support to image loading on 10.5+ via QLThumbnailImageCreate :D
  * How would a TexturePacker like thingie work for Gosu?
  * If there ever is functionality to 'and' and 'or' Gosu::Button, how would one check in buttonDown?
## Gosu Touch
  * First: see if the zooming is still an issue at all! Then: See if [UIScreen scale] really gives us a hint about zooming on the iPad - and if so, tell the user to STOP IT man!
  * Compare with OolongEngine for audio issues
  * See if xiph Tremor makes sense for Gosu Touch
  * Let resolution decide orientation
  * Clear up GOSU\_IS\_MAC vs. GOSU\_IS\_APPLE
  * Migrate WindowTouch.mm to CADisplayLink (3.1 SDK)
  * Use getBytes instead of UTF8String
  * Testen, ob nicht alles besser ist, wenn ich graphics width/height die echten Daten des iPhone4 liefern lasse
  * Fix music stopping after locking the screen for a long time
  * Fix too-many-Fingers-bug
  * Unify drawQuad's effective triangularization on iOS and desktop
  * See if there is a native/fastest mixing rate on Mac/iPhone
  * Add iCade support
  * Split Macros at 65k images on iOS if necessary
  * Add \_\_attribute\_\_((aligned(16))) to Gosu::Transform and make it binary compatible with GLKits GLKMatrix4
  * Experiment with UIKit & GTView (Gosu Touch?)
## Gosu CI/Usability
  * More front page content
    * UTF8 Support for PotD texts (see Florian Gro\_ß\_)
    * Show version on libgosu.org front page
    * Create a dynamic screenshot page for all the topics in the Showcase
    * Put tmbundle on front page
    * Link to benkos example & Chingu regarding states
    * Mention Panda Canvas as a good educational application of Gosu
    * Add some first eye catchers to front page
    * Add "What now?" link list to front page
    * Link YouTube videos, and maybe blog tags like http://www.cuberick.com/search/label/gosu?
  * More docs
    * Emphasize difference between button\_down and button\_down? somewhere
    * Make sure that it is documented what happens to different drawing ops with same z-order
    * Deployment wiki page/rdoc: Mention Icon resource support!
    * Explain SampleInstance vs. Sample somewhere
    * Tutorials: Mention where to find the final source code
    * Document MAX\_TEXTURE\_SIZE
    * Document alpha modes for Ruby
    * Add OpenGL Wiki page
    * Make sure that WindowMainLoop states that the whole order is just about perceived performance
    * Add "Feature Pack" to requirements for MSVC
    * Add a note: FreeImage 3.9.3-3 is not good enough
    * Document how Font roughly works (allow devs to cache chars by text\_width'ing the alphabet)
    * Point out that Font#text\_width is only relevant to Font#draw etc
    * Point out that the RubyGosu.app lib dir can be cleaned up
    * Link to the FMOD MP3 licensing info page (or the page it refers to) publicly for MP3 clarification
    * Add Unicode Support wiki page
  * New unified layout
    * Design new layout…
    * Skin YARD for new layout
    * Merge doxygen header w/ website (tabs)
    * Make logo in forum clickable
  * Polish existing games
    * OR&G: Build simpler version
    * Include CptnCpp as sample game
    * Fix download for all my LD games
    * .app'ify ippa's game after :retrofy is in and the wrapper can handle texplay
  * Update README.txt and website year
  * Extend RubyGosu.tmbundle: cmd+R -> runs main.rb
  * Automatically include Wiki pages in rdoc
  * Mention copyright() in README
