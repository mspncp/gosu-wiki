This list of tasks is exported automatically from my OmniFocus projects.
(Last update: 2015-01-22)


## Gosu
  * Clean up & check in CMake fixes
  * SDL: Map analog trigger buttons, forgot about those last time.
  * Add/update third party licenses in depencencies/
  * Releasy Deployment Fixes
    * See if I can reproduce this Releasy issue
    * Try to reproduce Releasy's issue #44
  * Gosu 0.9.0-style Interface (get rid of Window references everywhere)
    * rename userDocs to userDocuments
    * Introduce one "0.9" style constructor as a proof of concept
    * Make things tileable by default but add :smooth and :pure or something like that
    * Rename needs\_x? to need\_x? in Ruby
    * Adjust Text Entities to line height
    * Add Gosu::StringArg (a variant type of char*/wchar*/string/wstring/C++11 strings)
    * Consequently throw exception for invalid font names
    * Get rid of quad/tri drawing in favor of quads
    * Use float instead of double
    * Use int instead of unsigned
    * Throw exception for multiple windows
    * Kill beginGL/endGL in favor of scheduleGL
    * Rename pimpl/Impl to p/Private
    * Rename SampleInstance to Channel
    * Remove the "from\_" from "from\_hsv" and "from\_ashv", and deprecate Color#initialize
    * Deprecate Image::getData, introduce Image::data
    * Make Window::needsCursor return true by default
    * Rename all those Ruby examples and feature\_tests
    * Change ImageData::toBitmap to toBlob(byte*, size\_t) and copy directly in RSTRING; add Image::toBitmap() instead
  * More awesome Vertex Arrays
    * Pre-transform all vertex arrays
    * Come up with a nice memory union of DrawOp and ArrayVertex
    * Split up macros into vertices when drawn inside record{} (allow nesting)
  * Improve Input
    * Investigate Gosu bug: TextInput doesn't stop KbP/KbB from being sent to button\_down on Windows
    * Fix/clarify TextInput vs. &lt;markup> and &entities;
    * GpButtonX must fire after GpYButtonX so that control setup screens receive the more specific ID first
    * Order USB devices alphabetically (so that gamepad 0 is always 0) - TODO: check if SDL already does that?
  * Improve text rendering
    * Add FontFlags support for SDL\_TTF Gosu/Text
    * Font#draw with given block that yields each character's Gosu::Image, x, and y to a block, rather than drawing them
    * Make &lt;c=> more efficient in Font::drawRel
    * Add &lt;s=> to text formatting
    * Fix Gosu::Font(…default, 20) with italics on Windows (see forum thread)
    * Fix Unicode support for SDL\_TTF port (see feature\_tests/UnicodeTest.rb, @loc\_test)
    * Fix exceptions being turned into segfaults on Linux (see GoogleCode issue)
    * Implement ffUnderline by hand in createText/Font
    * Creating a non-existent font should throw an exception on all platforms, test on which it does
    * Font should respect monospaced fonts and fonts with very weird kerning (Zapfino...): do research
    * Verify that "Daniel" font works properly in Font and Text
    * Mac: Use Core Text instead of ATSUI
    * Fix error when creating an Image from "\n" on OS X
    * Use Gosu text formatting in Tutorial.rb
    * TextField with clip\_to (update example)
  * Fix: :align=>:center doesn't work without also passing :width (not intuitive)
  * Expose Gosu Directories in Ruby
  * Make sure that Gosu::clamp prevents NaN whenever possible
  * Look at Jamer's commit re: improved image loading
  * Assure Gosu::File also creates directories as necessary
  * Find out why this could happen: 'RuntimeError: While calculating the width of a text, the following error occured: The operation completed successfully.'
  * Add Gosu::potential\_fps
  * Warning when relying on case sensitivity
  * See if clipping coordinate calculation is correct with all transformations considered (why is Terava off by one pixel?)
  * Gosu: try integer truncing of drawing positions
  * Remove setResolution and use transforms instead
  * Make C++'s Gosu::multiply available to Ruby
  * Add Numeric#clamp, Numeric#wrap to Ruby
  * Make OpenAL buffers in Mac port larger and make sure that update\_interval&lt;66 always plays running Songs without jitter
  * Document Gosu::interpolate, improve it too?
  * Add callback for the OS-supplied "close" button
  * Try to understand this benchmark on stackoverflow
  * Use big texture for LargeImage if possible
  * Add better error message for missing files on Linux/FreeImage
  * Improve C++ exception display
  * Find out why the attached file allows the image to exceed its boundaries (by a lot)
  * Apply colorKey AFTER splitting the bitmap into tiles, not before!

## Gosu .app Wrapper
  * Waiting for SDL 2.0.4...
  * Modify Rakefile to not ruin the installed ruby2.0.0 afterwards
  * Build 0.8 version (must bundle SDL!)
  * Add Rubygems to .app wrapper with RUBYLIB='' (so it doesn't use a local version), RUBYOPT = '', GEM\_PATH = 'runtime\_path/to/vendor'
  * Create Rakefile to put everything together
  * Build Retina-ready icns that still works on 10.5; see http://stackoverflow.com/questions/12772346/retina-ready-icns-icon-file-on-10-5-leopard-size-limit
  * Add more docs (e.g.: the Ruby.app lib dir can be cleaned up)

## Gosu iOS
  * Add \_\_attribute\_\_((aligned(16))) to Gosu::Transform and make it binary compatible with GLKits GLKMatrix4
  * Compare with OolongEngine for audio issues
  * See if xiph Tremor makes sense for Gosu Touch
  * See if there is a native/fastest OpenAL mixing rate on Mac/iPhone

## Gosu Android
  * Start a new project from scratch, try to port the SDL-based Gosu 0.8 to Android (should be easier!)
  * Take a look at Gradle for Android building - otherwise, setup maven
  * Look at OpenAL for NDK apps

## Gosu CI/Usability
  * Deactivate or fix Project of the Day script (durch Slideshow ersetzen?)
  * Explain how to compile Ruby/Gosu in CONTRIBUTING.md
  * Add build instructions for MSVC x64 build
  * Add Gosu & Ruby.app logos to github READMEs
  * More front page content
    * Make a three-col layout: (Ruby / C++ / more?)
    * UTF8 Support for PotD texts (see Florian Gro\_ß\_)
    * Show current version on libgosu.org front page
    * Create a dynamic screenshot page for all the topics in the Showcase
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
  * Move Gosu examples into separate project/gem
  * Extend RubyGosu.tmbundle: cmd+R -> runs main.rb
  * Mention copyright() in README
  * Document that the Gosu::Window might be smaller than expected
  * Document that record{} can be called anywhere
  * Fix Gosu docs: 'RGBA' octet == WRONG
  * Link video tutorials from front page
  * Document Gosu::\_release\_openal\_resources and how it could be useful in testing (or can I fix this in a better way?)
  * Comment &lt;b> etc. in Text functionality
  * Describe project structure in CONTRIBUTING.md
  * Document subimage and &entities;
  * Update the docs on how to setup C++ Gosu on Windows!
  * Split Gosu website into its own github project
  * Fork Gosu.tmbundle into its own git repository
  * Compare Gosu prefix() functions to SDL path helpers
  * Find out what Gosu::Song::play does when it's already playing, then clarify docs (i.e. does it start over or keep playing?)
