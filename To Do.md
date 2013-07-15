# To Do list

This list of tasks is exported automatically from my OmniFocus projects.
(Last update: 2013-07-15)


## Gosu
  * Document subimage
  * Update the docs on how to setup C++ Gosu on Windows!
  * Fix release process
    * Publicly discontinue Gosu.framework / gosu-mac archives
    * Fix app wrapper
    * Automate swig generation again (Rakefile)
  * Switch Mac Gosu to using full-desktop windows, not resolution switching!!
  * GpButtonX must fire after GpYButtonX so that control setup screens receive the more specific ID first - Mac
  * GpButtonX must fire after GpYButtonX so that control setup screens receive the more specific ID first - Win
  * Order USB devices alphabetically (so that gamepad 0 is always 0) - Mac
  * Order USB devices alphabetically (so that gamepad 0 is always 0) - Win
  * More awesome Vertex Arrays
    * Pre-transform all vertex arrays
    * Come up with a nice memory union of DrawOp and ArrayVertex
    * Split up macros into vertices when drawn inside record{} (allow nesting)
  * Automatically create OpenGL context when Image is first created (half done - see old working copy from 10.6)
  * Introduce one "0.8" style constructor as a proof of concept
  * Gosu 0.8.0
    * Make things tileable by default but add :smooth and :pure or something like that
    * Rename needs\_x? to need\_x? in Ruby
    * Adjust Text Entities to line height
    * Add Gosu::StringArg (a variant type of char*/wchar*/string/wstring/C++11 strings)
    * Consequently throw exception for invalid font names
    * Throw exception for multiple windows
    * Kill beginGL/endGL in favor of scheduleGL
    * Rename pimpl/Impl to p/Private
    * Rename SampleInstance to Channel
    * Remove the "from\_" from "from\_hsv" and "from\_ashv", and deprecate Color#initialize
    * Deprecate Image::getData, introduce Image::data
    * Make Window::needsCursor return true by default
    * Rename all those Ruby examples and feature\_tests
    * Change ImageData::toBitmap to toBlob(byte*, size\_t) and copy directly in RSTRING; add Image::toBitmap() instead
  * Make sure that Gosu::clamp prevents NaN whenever possible
  * Look at Jamer's commit re: improved image loading
  * Fix implicit requirement to have "../gosu == ." in rake/linux.rb
  * Automatically create 'pkg' folder since git can't handle empty folders
  * Meditate: Imagine a Window::baseTransform that will affect Graphics *and* (inversed) Input - would this help games? Or rather add input un-transforming in general? Hmm!
  * Fix/clarify TextInput vs. <markup> and &entities;
  * See if Gosu can be made to use BGRA again because it is apparently faster on OSX/iOS
  * Get rid of quad/tri drawing in favor of quads
  * Use float instead of double
  * Use int instead of unsigned
  * Cleanup glBegin, Graphics::begin etc.
  * Fork Gosu.tmbundle into its own git repository
  * Fork website into its own git repository
  * Fix Gosu::Font(…default, 20) with italics on Windows (see forum thread)
  * Add more #inspect strings (easier to use with irb/Pry)
  * Get GLFW working on OS X
  * Get GLFW working on Linux
  * Add accelerometer support for OS X; maybe find a way to use UniMotion
  * Windows: Input will regularly query devices which are not currently attached, thereby causing the game to halt every few seconds - think about this
  * FSAA/mipmap experiments
  * Provide C++ application templates where possible, maybe even installers for the templates
  * Assure Gosu::File also creates directories as necessary
  * more C++ examples
  * Look at wox-Gem to refactor rake/mac.rb
  * Font#draw with given block that yields each character's Gosu::Image, x, and y to a block, rather than drawing them
  * Find out why this could happen: 'RuntimeError: While calculating the width of a text, the following error occured: The operation completed successfully.'
  * Add Gosu::potential\_fps
  * Fix Song#volume with short songs
  * Find out what Gosu::Song::play does when it's already playing with each implementation, then clarify docs
  * Add FontFlags support for SDL\_TTF Gosu/Text
  * Fix Unicode support for SDL\_TTF port (see feature\_tests/UnicodeTest.rb, @loc\_test)
  * Fix exceptions being turned into segfaults on Linux (see GoogleCode issue)
  * See if clipping coordinate calculation is correct with all transformations considered (why is Terava off by one pixel?)
  * Make <c=> more efficient in Font::drawRel
  * Add <s=> to text formatting
  * Gosu: try integer truncing of drawing positions
  * Remove setResolution and use transforms instead
  * Use Gosu text formatting in Tutorial.rb
  * Make C++'s Gosu::multiply available to Ruby
  * Add Numeric#clamp, Numeric#wrap to Ruby
  * Screen mess
    * Iterate on first category of fullscreen tests
    * Add fullscreen accessors to make proper FS OpenGL possible
    * Add fullscreen stretching prevention
    * Think about adding cmd+F support for toggling fullscreen: Possible?
    * Think about adding alt+enter support for toggling fullscreen: Possible?
    * Try not to hide the mouse cursor outside of the main window on OS X
    * Test multiple screens on Windows
  * TextField with clip\_to (update example)
  * Create C++ app template for Xcode4
  * Create iPhone app template for Xcode4
  * Make OpenAL buffers in Mac port larger and make sure that update\_interval<66 always plays running Songs without jitter
  * Text quality
    * Implement ffUnderline by hand in createText/Font
    * Creating a non-existent font should throw an exception on all platforms, test on which it does
    * Font should respect monospaced fonts and fonts with very weird kerning (Zapfino...): do research
    * Verify that Daniel font works properly in Font and Text
    * Linux: Support other XKeySyms than Latin 1
    * Mac: Add dead keys to TextInput
    * Mac: Use Core Text instead of ATSUI
  * Polish/deployment
    * Assure that files from doxygen task are considered for packaging
    * Review: http://rubyforge.org/tracker/index.php?func=detail&aid=21405&group\_id=375&atid=1504
    * Make sure README and LICENSE are appropriately named in the Gem
    * Now that the Rakefile works, stop doing every task every time (use file dependencies)
  * Make examples discoverable
  * Retry properly showing/hiding the mouse on OS X (immune to blocking main thread)
  * Mac OS: Mauszeiger wird im FS sichtbar bei Klick in obere linke Ecke: Warum?
  * Look at http://slick.cokeandcode.com/index.php?entry=entry080426-213044
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
  * Expose Gosu Directories in Ruby
  * Document Text Entities
  * COMMON\_CPP\_FILES in Rakefile should contain the headers!
  * Fix: Mouse position on Linux is always reported to be inside the window
  * Use big texture for LargeImage if possible
  * Add better error message for missing files on Linux/FreeImage
  * See if this page helps with fullscreen on OS X
  * rename userDocs to userDocuments
  * Fix: :align=>:center doesn't work without also passing :width (not intuitive)
  * Investigate Gosu bug: TextInput doesn't stop KbP/KbB from being sent to button\_down on Windows
  * Improve C++ exception display
  * Try rake-compiler
  * Find out why the attached file allows the image to exceed its boundaries (by a lot)
  * Fix Memory leaks in WindowX shareContext
  * Image::insert/Bitmap::insert should memcpy if possible
  * Apply colorKey AFTER splitting the bitmap into tiles, not before!
  * simplify Gosu's IO philosophy (C++)
  * Make plans for an official Scene/State system
  * How would a TexturePacker like thingie work for Gosu?
  * Redesign (see forum) drawing interface

## Gosu .app Wrapper
  * Fork RubyGosu.app into its own git repository
  * Create Xcode project to build the very shallow core only
  * Create Rakefile to put everything together
  * Add Rubygems to .app wrapper with  RUBYLIB='' (so it doesn't use a local version), RUBYOPT = '', GEM\_PATH = 'runtime\_path/to/vendor'
  * Compare RubyGosu.app to https://github.com/steveklabnik/furoshiki
  * Make the wrapper's menu bar on OS X more complete

## Gosu iOS
  * Add \_\_attribute\_\_((aligned(16))) to Gosu::Transform and make it binary compatible with GLKits GLKMatrix4
  * Compare with OolongEngine for audio issues
  * See if xiph Tremor makes sense for Gosu Touch
  * Let resolution decide orientation
  * Clear up GOSU\_IS\_MAC vs. GOSU\_IS\_APPLE vs. GOSU\_IS\_IPHONE vs. GOSU\_IS\_OPENGLES
  * Use getBytes instead of UTF8String
  * Migrate WindowTouch.mm to CADisplayLink (3.1 SDK)
  * Return pixel(!) resolution in screenWidth()/screenHeight()
  * Fix music stopping after locking the screen for a long time
  * Fix too-many-Fingers-bug
  * Make screenWidth()/screenHeight() return real pixels
  * Unify drawQuad's effective triangularization on iOS and desktop
  * See if there is a native/fastest mixing rate on Mac/iPhone
  * Split Macros at 65k images for iOS
  * Experiment with UIKit & GOSUView
  * Fix rotation hell; at least shouldAutorotate should return YES for one value.
  * Fix vsync blank at PC.ipa startup
  * Gosu Image from CGImage constructor?
  * Warnung über Root View Controller beheben

## Gosu Android
  * Move code from main.cpp into Gosu
  * Investigate into OpenAL for NDK apps
  * Structure
    * Move Gosu into a separate .so with the help of a project template
    * Merge gosu/android into gosu/master

## Gosu CI/Usability
  * Split up Gosu todo task into its own github project
  * More front page content
    * Make a three-col layout: (Ruby / C++ / more?)
    * UTF8 Support for PotD texts (see Florian Gro\_ß\_)
    * Show current version on libgosu.org front page
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
  * Update README.txt and website year
  * Extend RubyGosu.tmbundle: cmd+R -> runs main.rb
  * Mention copyright() in README
  * Document that the Gosu::Window might be smaller than expected
  * Document that record{} can be called anywhere
  * Mention releasy on Windows packaging wiki page
  * Create Gosu docset for Dash
  * Fix missing Headers in To Do Wiki page
  * Update github docs for Xcode4
  * Fix Gosu docs: 'RGBA' octet == WRONG
  * Link video tutorials from front page
  * Document Gosu::\_release\_openal\_resources and how it could be useful in testing (or can I fix this in a better way?)
