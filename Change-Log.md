# Change Log

This page is obsolete. Changes in recent versions of Gosu are explained on the [releases page](https://github.com/gosu/gosu/releases).

## 0.10.8
* 2016-08-15: Mac: Fix several compilation issues
* 2016-08-15: All: Map analog trigger buttons in SDL_GameController API to `GpButton` constants
* 2016-07-02: Ruby: Gosu::Color can now safely be used as a Hash key (thanks to @shawn42 for the contribution)

## 0.10.7
* 2016-04-24: Windows: Support for Ruby 2.3.0
* 2016-04-23: Linux: Improve mouse getters/setters
* 2016-04-18: Ruby: Fix Gosu::random not being random
* 2016-04-18: All: Update stb_image, stb_image_write, stb_vorbis
* 2016-04-17: Mac: Reduce Gosu::Font artefacts
* 2016-03-15: Ruby: Fix compilation issues with Ruby 1.9.3

## 0.10.6
* 2016-02-14: Windows: Fix wrong viewport size in fullscreen

## 0.10.5
* 2016-01-11: All: Update SDL to 2.0.4 stable. Finally!! <3
* 2016-01-11: All: Update stb_image, stb_imagewrite and stb_vorbis dependencies
* 2016-01-11: Ruby: Update SWIG to 3.0.8 - who knows what this will break
* 2015-12-19: All: Support clockwise coordinates in `Macro#draw`
* 2015-11-11: Ruby: Use `sdl2-config` on OS X, not only on X11-based systems

## 0.10.4 (Ruby only)
* 2015-10-04: Ruby: Fix compatibility with Gosu 0.8 interface (`Gosu::Image#initialize`; issue #360)

## 0.10.3
* 2015-09-30: All: Fix black/white empty window before `Gosu::Window#show` is called (issue #280)

## 0.10.2
* 2015-09-15: All: Fix many common text rendering artefacts
* 2015-09-15: Mac: Fix compilation error on OS X 10.11 El Capitan
* 2015-09-13: All: Add experimental `Window#tick` method to potential integration with GUI toolkits
* 2015-09-07: Windows: Update to SDL 2.0.4 RC 2

## 0.10.1
* 2015-08-20: Windows/Linux: Fix audio playback of stereo, non-Ogg-Vorbis files (https://github.com/gosu/gosu/issues/237)
* 2015-08-20: Ruby: Fix `:retro` parameter in `Image.load_tiles` and `Image.from_text`

## 0.10.0
* 2015-08-20: Xcode: The `Gosu.podspec` for OS X and iOS is now versioned, instead of being stuck at v0.0.1
* 2015-08-19: Windows: Upgrade to Visual C++ 2015 (the free Express Desktop edition works)
* 2015-08-19: C++: Sockets have been extracted to https://github.com/jlnr/Sockets; RIP!
* 2015-08-17: All: Use stb_image(_write) for image I/O instead of GDI+, FreeImage, UIImage/NSImage etc.
* 2015-08-15: All: Use stb_vorbis for OGG decoding instead of libogg/libvorbis/libvorbisfile
* 2015-07-26: Unix: Fix CMake build files
* 2015-07-22: All: Add new `ifRetro`/`:retro` parameter to image constructors
* 2015-07-15: Ruby: Fix mouse position getter/setter interaction

## 0.9.2
* 2015-05-24: Windows: Support for Ruby 2.2.x
* 2015-05-24: All: Allow macro recording outside of Window::draw
* 2015-05-23: All: Use new SDL_GetGlobalMouseState function if available

## 0.9.1
* 2015-05-17: Ruby: Fixes freeze-at-exit bug (thanks to RunnerPack for reporting this)
* 2015-05-17: Ruby: Fixes one uninitialised variable that could affect text alignment
* 2015-05-16: Ruby: Fixes backwards compatibility in Font#initialize

## 0.9.0
* 2015-05-16: All: New interface where almost everything is independent from Gosu::Window

## 0.8.7
* 2015-01-17: All: Improve gamepad support by using the SDL_GameController API
* 2015-01-17: Windows: Fix LoadError in Ruby 2.1.x x64 gem

## 0.8.6
* 2014-12-10: Windows: Add support for Ruby 2.1.x x64
* 2014-12-10: Windows: Update FreeImage to v3.16.0 (64-bit release only)
* 2014-12-10: Windows: Update OpenAL soft to v1.16.0 (64-bit release only)
* 2014-12-06: Windows: Add support for Ruby 2.1.x
* 2014-11-09: All: Check SDL 2 return values when creating the window

## 0.8.5
* 2014-09-28: Linux/Mac: Fix compilation with recent versions of Ruby
* 2014-09-09: Mac: Fix compilation in rvm

## 0.8.4
* 2014-09-03: All: `Gosu::available_width` & `Gosu::available_height` can now be used to calculate the available space for a non-fullscreen window. (The return value is only accurate on OS X and Windows for now.)
* 2014-09-03: All: `Gosu::Window::show` now respects `needsRedraw`/`needs_redraw?` again.
* 2014-08-31: Mac: Fix scaling errors on Retina displays, caused by a regression in Gosu 0.8.3.

## 0.8.3
* 2014-08-28: Linux: Fix compilation errors on OpenSuSE 13.1 and other distributions which do not provide the latest version of SDL.
* 2014-08-28: All: Fixed `MsWheelUp`/`MsWheelDown` being swapped (thanks to @d3vkit for reporting)

## 0.8.2
* 2014-08-24: Windows: Gosu now supports Ruby 2.0.0.
* 2014-08-20: All: `Gosu::screen_width`/`screen_height` incorrectly returned 0 before a `Gosu::Window` was constructed.

## 0.8.1
* 2014-08-19: Windows: Fix a non-deterministic crash when loading TTF files.
* 2014-08-19: Windows: Fix audio crashes caused by updating to an unmodified OpenAL Soft 1.16.0.
* 2014-08-19: All: Fix a bug where the mouse wheel would either trigger `button_up` or `button_down`, but not both.

## 0.8.0
* 2014-08-18: Gosu now uses SDL 2.x as its backend. This implicitly fixes Mac fullscreen support, and makes it possible to use Gosu on the Raspberry Pi.
* 2014-08-11: All: Refactor (fix) `GOSU_COPYRIGHT_NOTICE`.

## 0.7.50
* 2013-11-06: Ruby: Fix various glitches in the SWIG-generated Ruby interface

## 0.7.49
* 2013-09-27: Mac: Fix compilation on OS X 10.9 Mavericks
* 2013-09-23: Linux: Add cmake build files
* 2013-07-16: Mac: Update Ruby.app to Ruby 2.0.0

## 0.7.48
* 2013-07-12: Linux: Fix compilation bug with Ruby 2.0 (#181)
* 2013-06-24: Mac: Use full Retina resolution where available
* 2013-06-24: All: Add `Image#subimage(x,y,w,h)` / `ImageData::subimage(x,y,w,h)` (#178)

## 0.7.47
* 2013-04-01: All: Add msOther0 - msOther7 constants for extra mouse buttons
* 2013-04-01: All: Add constants: kbBacktick, kbMinus, kbEqual, kbBracketLeft, kbBracketRight, kbBackslash, kbSemicolon, kbApostrophe, kbComma, kbPeriod, kbSlash
* 2013-04-01: Windows: Add support for up to four gamepads
* 2013-04-01: Linux: Fix `button_down`/`button_up`/`TextInput` (thanks @oli-obk)
* 2013-04-01: Linux: Enable optimizations in CMake build files (thanks @oli-obk)
* 2013-04-01: Mac: Work around crashes in C++ exception handling
* 2013-04-01: Mac: Fix some gamepad bugs (e.g. unplugging when Gosu is running)
* 2013-04-01: Mac: Fix a bug where Gosu processes would not terminate while a song is running

## 0.7.46
* 2013-03-31: Mac: Drop support for OS X 10.4
* 2013-03-30: Linux: Use scancodes as button IDs on Linux, just like on Windows (thanks @oli-obk!)
* 2013-02-24: Mac: Disable fullscreen mode for now, as it is broken on 10.7/10.8 (will fix after May)
* 2013-02-24: Mac: Add support for up to 4 gamepads
* 2013-01-13: Mac: Allow window to use more desktop real estate
* 2013-01-10: Mac: Fix bizarre crash on OS X with Ruby 1.9
* 2012-11-13: Linux/MinGW: Add CMake build files (thanks again @oli-obk)
* 2012-09-29: Windows: Fix bug where Gosu would not run in a directory with spaces in its filename
* 2012-09-25: Windows/C++: Show error and shut down when draw() throws an exception (thanks @quit)
* 2012-09-16: Mac: Fix Image::save
* 2012-09-16: Mac: Fix a crash in font rendering
* 2012-09-09: C++: Add Socket example game (huge thanks to @oli-obk!)
* 2012-08-13: All: Fix integer truncation of clipping rectangles (thanks @jamer)
* 2012-07-21: Ruby: Fix `gl(z) {}` memory leak

## 0.7.45 (Ruby gem only)
* 2012-07-19: Mac: Added missing binary for Ruby 1.9
* 2012-07-19: Ruby: The Gosu gem now correctly builds rdoc on installation (if enabled)

## 0.7.44
* 2012-07-17: Linux: Fix compilation (thanks @nat1192)
* 2012-07-16: Windows: Fix OpenAL crash at shutdown, get rid of custom OpenAL32.dll
* 2012-07-16: All: Macros and enqueued draw() calls are unaffected by released Images
* 2012-07-16: All: Max out at 255 AL sources on all systems except iOS
* 2012-05-31: Linux/Windows: milliseconds() returns time since first call of milliseconds() (thanks @quit)
* 2012-05-20: Windows: Require MSVC 2010 (thanks to @quit for the support)
* 2012-04-15: Mac: Fixed some minor memory leaks

## 0.7.43
* 2012-03-18: All: Recorded macros can be arbitrarily rotated or `draw_as_quad`-ed
* 2012-03-16: Ruby: Internal `gosu/zen` progress & example, you should check it out (thanks @erisdiscord)
* 2012-03-15: Ruby: Internal `gosu/preview` progress, production-ready if you use Bundler responsibly
* 2012-02-25: Ruby: Fix GC of enqueued `Window#gl` blocks (thanks to RavensKrag for reporting)
* 2012-01-19: Linux: Fix colors having swapped channels in SDL text (thanks to Spooner for reporting)
* 2012-01-12: Linux: Added constants for meta keys (thanks to Hanmac)
* 2012-01-17: Windows: Fix debugging chaos when an assertion in `Window::draw` is raised (thanks to tuiq)

## 0.7.42
* 2012-04-01: This release requires a Gosu Gold account.

## 0.7.41
* 2011-12-16: All: Fixed several subtle bugs in the transform stack
* 2011-11-29: All: Fixed flush() when inside transforms/clipping
* 2011-11-20: Linux: Fixed another PNG loading bug (thanks again, Jamer!)

## 0.7.40
* 2011-11-19: All: Fixed interaction between recording and transforms
* 2011-11-19: Linux: `screenWidth`/`screenHeight` also returns the size of the primary screen only (thanks again, JayThirtySeven)
* 2011-11-19: Linux/Ruby: Fixed Xinerama linker error

## 0.7.39
* 2011-11-18: All: Added Window#record(width, height)
* 2011-11-14: All: Removed an overcautious assert() from OGG file reading
* 2011-11-14: All: Fixed OGG files' destructor stopping unrelated songs
* 2011-11-14: Linux: Fullscreen only covers one screen now (thanks JayThirtySeven!)
* 2011-11-01: Ruby: Switched from rdoc to YARD

## 0.7.38
* 2011-10-25: Mac/iPhone: Fixed alpha channels
* 2011-10-23: All: Renamed 'additive' to 'add' to be consistent with 'multiply'
* 2011-10-08: Ruby: Made all Color accessors less annoying (will clip & truncate given values)
* 2011-09-19: Ruby: Fixed some C++ exceptions not being translated properly

## 0.7.37
* 2011-09-11: All: Added Gosu::language() that retrieves the user's current language
* 2011-09-08: Linux: Using X11 Expose event instead of crashy XDamage event (thanks Jamer)
* 2011-09-04: All: Added Font::setImage/Font#[]=(char, image) to set up a custom image for a character

## 0.7.36
* 2011-08-24: Win/Ruby: Fixed unhelpful Image loading errors
* 2011-08-22: Linux: Lots of configure & Rubygem fixes (thanks again here, Jamer)
* 2011-08-17: Win/Ruby: Fixed crashing or hanging Ruby process on exit after using audio

## 0.7.35 (yanked)
* 2011-08-11: Fixed some bugs that had snuck into the 0.7.34 release.

## 0.7.34 (yanked, broken on all platforms)
* 2011-08-11: Mac/Ruby: Rebuilt the Mac .app to support 10.4+ (three-way universal)
* 2011-08-07: Linux: Changed audio backend to OpenAL/libsndfile (thanks again to Jamer)
* 2011-07-24: Linux: Redraw the window on window damage (thanks Jamer)
* 2011-07-14: Windows: Changed audio backend to OpenAL/libsndfile
* 2011-06-26: C++: Removed dependency on boost (uses TR1/C++03 instead) (thanks to tuiq for a hotfix here)
* 2011-06-23: C++: Changed signature of loadImageFile to reduce heap bloat
* 2011-06-18: Windows: Started to add MinGW compatibility (thanks Jamer & Seisatsu)

## 0.7.33
* 2011-06-13: Windows: Fixed potential GDI+ initialization problem (thanks tuiq)
* 2011-06-08: Ruby: Fixed exception error (e.g. at shutdown)
* 2011-06-06: Ruby: Fixed possible crashes with invalid arguments (thanks Spooner)

## 0.7.32
* 2011-06-04: Mac/Ruby: Added chipmunk back to .app wrapper
* 2011-06-04: All: Added GOSU_COPYRIGHT_NOTICE to make it easier for game devs to fulfill BSD requirements
* 2011-06-04: Ruby: Lots of work towards making exceptions transparent to the main UI message loop
* 2011-06-04: Windows/Ruby: Added optional support for FreeImage. If image loading with GDI+ fails, Ruby/Gosu will look for FreeImage.dll and retry.
* 2011-06-01: Mac/Ruby: One more attempt to clear the GL error (to keep ruby-opengl from complaining)
* 2011-06-01: All: Text handling code correctly fails when a function is unexpectedly passed a newline (for example, Font#draw does not handle it)
* 2011-05-13: Linux: Gosu does not require freeimage ≥3.13 anymore

## 0.7.31
* 2011-04-30: Mac/iOS: Proper exception when image loading fails

## 0.7.30
* 2011-04-29: Windows: Improved Audiere error handling with incompatible formats
* 2011-04-29: Ruby: Exceptions within Window#draw/update are now puts'ed too for redundancy (issue 78)
* 2011-04-29: Linux: Gosu now uses FreeImage to read/write images, supports more formats
* 2011-04-28: Windows: All-around fixed Gosu::SampleInstance/currentSong
* 2011-04-10: Windows: Gosu now uses GDI+ to read/write images, supports more formats (thanks to mathias for the fork/lots of code)
* 2011-04-10: Mac/iOS: Gosu now uses Apple APIs to read/write images, supports more formats
* 2011-04-06: Mac: The 'ruby' platform Gem should now work with MacRuby, Rubinius given all dependencies (experimental)

## 0.7.29
* 2011-03-25: Added GL_FLOAT support in all places where RGBA BLOB strings are passed in Ruby (determined by the length of the string)

## 0.7.28 (first GitHub backed release)
* 2011-03-12: Added Image::insert(Bitmap, x, y) / Image#insert(binary_string, x, y) (undocumented for now)
* 2011-03-05: Fixed Color#==
* 2011-03-05: Fixed Macro Z-Ordering (thanks mathias - towards a supported Macro...)
* 2011-03-05: OS X 64-bit: Gosu now supports all file types supported by NSImage (even PSD & PDF)
* 2011-02-26: Gosu's image loading is now unified under loadImageFile()
* 2011-02-09: Fixed PNG transparency bug
* 2011-02-07: Fixed kbBeginRange constant (C++), thanks shawn42! 

## 0.7.27
* 2011-01-29: Linux: Switched from SDL_mixer to Audiere (supports 'speed' arguments now)
* 2011-01-22: Windows: Switched from FMOD3 to Audiere
* 2011-01-19: All: Added Gosu::fps() that returns the approximate current framerate

## 0.7.26
* 2011-01-08: Ruby: Added Color#== and Color::argb/Color::rgba constructors
* 2011-01-08: All: Added Window#gl(z, &block) (Ruby) / Graphics::scheduleGL(functor, z) (C++)
* 2011-01-08: All. Optimized Gosu's rendering backend a bit
* 2011-01-02: Ruby: All Strings coming from Gosu are now correctly tagged as UTF-8 in Ruby 1.9
* 2010-11-20: Fixed SDL_TTF font height on Linux

## 0.7.25
* 2010-11-01: All: Fixed Gosu::Image#to_blob/ImageData::toBitmap
* 2010-10-27: Ruby: Now seeding Gosu::random with the system time on startup
* 2010-09-29: Ruby: Added missing scale(x, y, around_x, around_y) (thanks to Spooner)
* 2010-09-29: Ruby: Added Image#save(fn)
* 2010-09-08: All: Un-deprecated button_id_to_char/char_to_button_id
* 2010-09-08: Mac: Fixed button_id_to_char/char_to_button_id

## 0.7.24
* 2010-09-08: All: Made all beginClipping/clip_to arguments doubles instead of ints
* 2010-09-08: C++: Made Image, Sample, Font copy-constructable because they are immutable - should greatly reduce the need of shared_ptrs.
* 2010-09-03: OS X: Improved text rendering
* 2010-09-03: Ruby: line_height (argument to Image#from_text) is now a signed int, not unsigned int
* 2010-08-30: Windows: Fixed speed issues (re-introduced optimization switch)

## 0.7.23
* 2010-08-23: Windows: Removed inappropriate exception when mouseX/Y cannot be refreshed due to locked screen
* 2010-08-23: C++: Finally removed RotFlip completely. If you actually happened to use it: a replacement is available on the forum.
* 2010-08-22: Mac: Fixed setMousePos/mouse_x=/mouse_y= on OS X when the window has been shrunk down.
* 2010-08-19: C++: Added releaseMemory() callback to Gosu::Window that is mainly called on iOS when the OS is low on memory. Proposals for creative uses on other operating systems welcome.
* 2010-08-16: All: Fixed a channel swapping bug in Image::toBitmap/to_blob.
* 2010-08-13: All: Fixed a crash when formatting a paragraph of text with a word that is wider than the max paragraph width.
* 2010-08-12: All: Fixed an exception when partial formatting strings were rendered.
* 2010-08-05: C++: Added Window::loseFocus callback that is mainly called on iOS when the screen is locked.
* 2010-08-01: Mac: Fixed a crash where a USB device would not have a device name (product name)
* 2010-08-01: All: Added Window#flush/Graphics::flush() to flush the current Z queue to OpenGL and start a fresh one. All drawing operations afterwards will inevitably be *over* the previous ones.
* 2010-07-27: Added aroundX, aroundY parameters to Gosu::scale(sx, sy)
* 2010-07-07: Added accelerometerX/Y/Z() methods to Input (returning 0 on non-iPhone platforms), with thanks to PhilCK
* 2010-07-04: All: Made clipping operations nestable (also: faster, respects transforms etc.)
* 2010-07-04: C++: Deprecated zImmediate
* 2010-06-29: Fixed MAX_TEXTURE_SIZE, now always 512 (pessimistic value) on Linux
* 2010-06-28: All: Added support for negative line spacing, improved some text rendering corners
* 2010-06-26: All: Added Window#needs_cursor?/Window::needsCursor() to be able to show the cursor when in editor situations

## 0.7.22
* 2010-06-17: All: Fixed CJK support throughout Gosu
* 2010-06-17: All: Transforms are now applied in reverse order (the one that makes sense)

## 0.7.21
* 2010-05-13: Ruby: Updated CptnRuby to use translate() for scrolling
* 2010-05-13: All: In light of transformations, Font#drawRot is deprecated now
* 2010-05-13: C++: Fixed alpha support in Gosu::saveToPNG
* 2010-05-13: All: Added Image.getData().toBitmap() (C++)/Image#to_blob (Ruby)
* 2010-05-13: All: Added support for custom entities as registerEntity(name, bitmap) (C++)/register_entity(name, image) (Ruby) that can be placed in text as &name;
* 2010-05-13: All: Added HTML-like text markup for Font and Image#from_text (and C++ equivalents): `<b>`, `<u>`, `<i>` and `<c=aarrggbb>/<c=rrggbb>`
* 2010-05-10: All: Added four matrix transformations that affect all contained drawing: scale(), translate(), rotate() and a free-form transform()
* 2010-05-31: Linux: made gem Rubinius-compatible

## 0.7.20
* 2010-05-30: Windows: Removed Ruby package (use the rubygem)
* 2010-05-30: Linux: Removed Ruby support from autotools/source package (use the rubygem)
* 2010-05-30: All: Added setCaretPos/setSelectionStart (C++) and caret_pos=/selection_start= (Ruby) to TextInput
* 2010-05-30: Linux: Added fallback to SDL_TFF when loading local .ttf files, please install libSDL-ttf2.0-dev to continue using Gosu, thanks to the_om3ga
* 2010-05-29: Windows: When requesting a windowed resolution larger than the desktop, Gosu will transparently scale the window down
* 2010-05-23: C++: Added operator< for Gosu::Button so they can be put into a std::map
* 2010-05-21: Mac: Gosu wrapper .app now contains full, three-way universal Ruby 1.9 (only tcltk etc. missing)
* 2010-05-09: Linux: Converted Ruby gem to use mkmf instead of autotools (fixes rvm problems)
* 2010-05-07: Ruby: Added Window#fullscreen?

## 0.7.19
* 2010-04-24: Mac: Fixed custom TTF loading on 64-bit OS X 10.6 (thanks Tri&Alex for trying it out); see GettingStartedOnOsx for necessary Xcode project setup instructions
* 2010-04-23: All: Renamed the semi-documented gosuToRadianScale to degreesToRadian and vice versa (in Ruby, instance methods of Numeric). gosuToRadians and radiansToGosu remain unchanged.
* 2010-03-29: All: Added amMultiply/:multiply as alpha mode (thanks to mathias for the contribution)
* 2010-03-28: C++: Sockets should work on 64-bit systems now
* 2010-03-13: Ruby: Added Gosu::enable_undocumented_retrofication. It globally disables all texture bilinear filtering. Will be removed when proper interface is available, please put this in a "try" block when using.

## 0.7.17
* 2010-01-03: Mac/Ruby: Added stringio.bundle to the list of built-in extensions in RubyGosu App.app
* 2010-01-01: All: Reverted Gosu::Sample and Gosu::Song to retain their first argument for now
* 2010-01-01: Ruby: Fixed support for Ruby 1.9
* 2010-01-01: Ruby: Gosu::milliseconds always returns a Fixnum now

## 0.7.16
* 2009-12-29: All: Added Gosu::TextInput#filter for customizing what can/will be entered
* 2009-12-27: Windows: Added an error message when running a windowed game on a too small desktop
* 2009-12-27: All: Removed Gosu::Audio/Gosu::Window arguments from Gosu::Sample and Gosu::Song constructors
* 2009-12-19: All: Added Gosu::Color::RED etc., for C++ and Ruby, deprecated Colors::red in C++
* 2009-12-07: Ruby: Added Gosu::MAX_TEXTURE_SIZE for banisterfiend ;)
* 2009-12-07: Ruby: Added support for socket and yaml (=syck.bundle) in RubyGosu App.app
* 2009-10-09: Ruby: Added enough experimental MacRuby support to run Tutorial.rb (you will need to build Gosu from source)

## 0.7.15
* 2009-09-13: Ruby: Added compatibility with 64-bit x86 Ruby on OS X (= Snow Leopard)
* 2009-09-08: Ruby: Fixed Gosu::Color#dup

## 0.7.14
* 2009-06-28: Mac: OpenAL officially replaces FMOD in Gosu's OS X port.
* 2009-06-28: Ruby: Added Gosu::VERSION constants
* 2009-06-28: Linux: Removed FMOD support altogether
* 2009-06-28: C++: Added GOSU_VERSION macros in Gosu/Version.hpp
* 2009-06-07: All: Fixed max texture size calculation
* 2009-05-17: Linux: Improved compatibility with Ruby 1.9

## 0.7.13.3
* 2009-05-15: Ruby: Published the experimental Ruby 1.9 .app wrapper, feedback very welcome!
* 2009-05-14: C++: Added name() and flags() getters to Gosu::Font, and a flags argument to its constructor.

## 0.7.13.2 (experimental minor release; Ruby gems only)
* 2009-05-11: All: Added flags, height, name accessors to Font
* 2009-05-06: Linux: Fixed issue where thrown exceptions could result in a SIGSEGV on Linux
* 2009-05-06: Ruby: Worked around incompatibility between Ruby's GC and SWIG's object tracking
* 2009-05-04: Ruby: Added support for Ruby 1.9 for Windows and Linux
* 2009-05-04: Ruby: Rebuilt RubyGosu wrapper with SWIG 1.3.3.9
* 2009-04-29: Added support for newlines to simple version of createText/Image#from_text
* 2009-04-20: Fixed two bugs with texture borders

## 0.7.13
* 2009-04-17: All: Implemented global screen width/screen height getter functions
* 2009-04-16: Ruby: button_id_to_char and char_to_button_id are also available as class methods of Window now (old version is inofficially deprecated now).
* 2009-04-15: Win: Spinning the mouse wheel generates buttonUp events right after the buttonDown events for symmetry (fix)
* 2009-04-15: Win: Gosu automatically uses the first icon in the game's executable (if present) as the window icon, thanks for the suggestion Tuiq!
* 2009-04-16: Win: No button_down events for clicking on the task bar button anymore, thanks AmIMeYet!
* 2009-04-08: All: Introduced Window#needs_redraw? for game-specific optimizations
* 2009-04-08: All: Accept both OpenGL and previous vertex order for draw_quad/Image#draw_as_quad
* 2009-04-01: All: Reinstalled Image allocation optimization
* 2009-04-01: All: Fixed PNG writing (alpha channel)
* 2009-03-26: All: Fixed loading top-down BMP files (seem to be rare? :) )
* 2009-03-09: All: Made Gosu::createText/Image.from_text more compatible with Chinese and Japanese scripts (wrt line breaks)
* 2009-03-08: All: Reintroduced optimization that square, power-of-two, hard-bordered images are always allocated on a texture of their own
* 2009-02-10: Ruby: Upgraded to SWIG 1.3.37 (better error messages, probably some fixes in corner cases)
* 2009-02-10: All: Added Window::updateInterval() / Window#updateInterval

## 0.7.12
* 2009-02-07: All: Added Window::setMousePosition/set_mouse_position/mouse_x=/mouse_y=
* 2009-02-07: Win: Improved timing code
* 2009-01-31: All: Added Song and Sample looping
* 2009-01-31: All: Added Song#pause, #paused? and SampleInstance#pause, paused?, resume
* 2009-01-31: C++: Added Gosu::zImmediate (bypasses Z ordering)
* 2009-01-27: Win: Automatically link against Windows' socket libraries
* 2009-01-01, All: Gosu::angle_diff() fixed
* 2009-01-01, Mac: Window::close/Window#close now closes the Window immediately, not after the next event happens (thanks BackupBrian!)

## 0.7.11
* Ruby: `char_to_button_id` and `button_id_to_char` return nil for value that couldn't be converted (instead of 0).
* All: `Input::down(button)` silently returns false for a "no button" id, `Window#button_down?` silently returns false for `nil` values.
* All: Added simpler createText()/Image#from_text with support for just one line.
* All: Added kbA - kbZ constants that map to the physical A-Z keys (i.e. should not be affected by localized keyboards).
* Mac: Added some more spacing between Font characters.
* Linux: Disabled key repeat. (Really!)
* Linux: Fixed timing bug on very fast machines.
* Linux: Fixed crashes with regards to non-ASCII keys and Button<>char conversion.
* (All: Added experimental bi-directional text support in Gosu::Font, based on the LTR Override and RTL Override code points. You will need to manually insert them for now, implicit LTR/RTL text will not be recognized.)

## 0.7.10.1 / 0.7.10.2 / 0.7.10.3
* Linux: Fixed bug with -fPIC causing compilation trouble AGAIN (thanks 0x17!)
* Linux: Fixed bug with installing Gosu for Ruby 1.9 when 1.8 is also present
* All: Quite some fixes regarding the new release system…

## 0.7.10
* All: Added Song::volume()/Song#volume (thanks rabbitblue!)
* All: Fixed Gosu::angleDiff
* All: Fixed loading of PNG files with transparent palette entries.
* All: Added clipping via Window::beginClipping/endClipping or Window#clip_to, respectively
* All: Added Font::drawRot()/Font#draw_rot
* All: Increased the max OpenGL texture size used for a single image to 1024x1024 (only important if you rely on Image#tex_info)
* Ruby: Added `Numeric#gosu_to_radians` and `Numeric#radians_to_gosu` for easy angle conversion.
* C++: Renamed boundBy() to clamp()
* Linux: Fixed panning of SDL-based sound system, also added support for graceful degradation if no sound device available (thanks oli...! ;))
* Linux: Windowed mode fixed on Compiz, fullscreen mode fixed everywhere.
* Linux: Mouse wheel should work now.
* Linux: Now available as a Ruby gem! (Thanks to Leonardo Boiko for the contribution)
* Windows, Linux: Fixed an unlikely lockup.

## 0.7.9
* All: Added Gosu::TextInput functionality with example for Ruby and C++
* All: OpenGL allocates depth buffer, allows for better custom OpenGL effects.
* All: Gosu::Font looks a lot smoother
* All: Disabled undocumented Async functionality until further testing has happened
* FreeBSD: Linux port extended to cover FreeBSD as well (thanks Vagabond!)
* Mac: Fixed a bug where fullscreen mode could rearrange desktop icons (and otherwise confuse OS X).
* Mac: Added mouse wheel support.
* Mac: char_to_id bugfix (thanks 0x17!)
* Mac: Mouse will not be hidden as aggressively
* Mac: Don't keep firing buttonDown events when holding keys down
* Windows: Fullscreen mode allows alt+tab switching.
* Windows: Fixed mouse wheel support.

## 0.7.8.5
* All: Much better HSV interface. Hope this doesn't already break any code.
* All: Audio interface VASTLY extended! Yay.
* Linux: SDL_mixer port much closer to FMOD one.
* Mac: Fixed right-click detection

## 0.7.8
* Mac, Windows: Font substitution works, i.e. chars outside of the selected font can be used (こんにちは日本！)
* Mac, Windows: Custom font loading—just use a TTF filename as a font name (must contain '/')
* Mac: Fixed Window#button_id_to_char
* Mac: Window now pops up in the front when run from the Terminal
* Windows: Fixed fullscreen mode
* Linux: Removed optimization that prevented 64bit compilation
* Linux: Fixed compilation error (boost::none.hpp was missing, thanks to Ryan Baxter)
* Ruby: Another cool Chipmunk/RMagick demo by Robert Sheehan
* Ruby: HSV color support as in C++

## 0.7.7
* All: Gosu now uses doubles as Z positions
* All: Gosu allows for custom OpenGL integration, (Ruby) example game included
* Mac, Linux: Additive drawing fixed
* Mac: Leopard compatibility
* Mac: Vsync finally enabled—was *so* more necessary @ 60 Hz
* Windows: Gosu now uses OpenGL instead of Direct3D (less code to maintain, more game portability)
* Windows: Vsync also enabled (didn't work on Intel chipset though...)
* Ruby: Gosu::sleep was not supposed to exist, now killed (did overwrite Ruby's sleep when include'ing Gosu)
* Ruby: Gosu now cooperates with Ruby's multitasking
* Ruby: Chipmunk integration example

## 0.7.6
* All: Fixed a bug potentially cutting off text on all platforms
* All: Fixed a bug which would exclude lines from very long text
* All: updateInterval is now a float, not an integer. On systems other than OS X, it is effectively rounded upwards, though. The new default value is 16.666666 (= 60 FPS).
* Ruby: RMagick Images can be passed instead of filenames + example game
* Ruby: Image#draw_as_quad

## 0.7.5
* All: functions for button id<>character conversion are static now. Code shouldn't break.
* Ruby: Fixed name clash in CptnRuby.rb
* Ruby: Fixed memory leaks in load_tiles and from_text (thanks to Galin Yordanov!)
* Linux: Some changes for UTF-8 support (thanks to Galin Yordanov again)
* Linux: Hid mouse cursor over X11 window (thanks to acetoxy)
* Mac: Changed userSettingsPrefix to be ~/Library/Preferences
* Mac: Some changes for Ruby UTF-8 support
* Windows: Strings in Ruby programs now must be UTF-8 encoded
* Windows: FMOD.dll ships with Gosu now (RubyGosu adjusted to find it magically)

## 0.7.4
* Mac: Hats work more reliably than in 0.7.3 (and SDL :P)
* Ruby: Ooops - exceptions don't halt everything anymore.

## 0.7.3
* Mac: Gamepad support at last!
* Ruby: New example game/exercise collection ‘Cptn. Ruby’
* All: Added README.txt file to tell people to read the wiki.

## 0.7.2
* Mac/Ruby: The cumbersome .app wrapper is now only used for deployment; for development, running Gosu applications from the Terminal is now possible.
* Ruby: Re-added missing mouse_x/mouse_y/width/height accessor functions in Window. Thanks mutwin.kraus! ;)
* Ruby: Removed the annoying "type" argument for Song#initialize. *Breaks code*, even if this is not a milestone release ;(
* C++: Added (simplified!) constructors that take filenames to classes Image, Sample and Song; also loadImagesFromTiledBitmap accepts a filename. See reference.
* C++: Changed back Button:isDown to be Input::down(Button). There was kind of a mess going on, esp. because the tutorials were outdated.
* Win/Ruby: Tutorial media files were missing, sorry!

## 0.7.1
* Win: Moved to SWIG too.
* Mac: Fixed build script.
* Linux: Added SDL_mixer fallback. Yay, thanks nornagon!

## 0.7.0
* Moved to Google Code!
* Mac: implemented idToChar/charToId
* Mac: implemented fullscreen
* C++: Input uses Gosu::Button instead of unsigned for identification. *Breaks code.*
* Ruby: clearer Mac game distribution scheme
* Ruby: moved to SWIG
* Ruby: MUCH improved exception handling
* Ruby: Some arguments swapped to become consistent with C++'s order. *Breaks code.*

## 0.6.5
* Linux, Mac: Fixed File.

## 0.6.4
* Linux: Made texture binding lazier; this seriously speeds up Gosu on some 3D drivers.
* Linux: Made checking for fmod more tolerant.
* Mac: simplified keyboard code; if this breaks something please inform us!
* Mac: Universal at last!
* Mac: updated to .xcodeproj files
* Win: Updated to more recent library versions.

## 0.6.3
* Mac: added mouse clicking and hiding

## 0.6.2
* Mac: Now even fixed Gosu/Input for C++!
* Win: Another Input bug fixed.

## 0.6.1
* All: Fixed the stuff that the 0.6.0 update broke
* Linux, Mac: Improved installation routine

## 0.6.0
* All: Added Mac support
* Ruby: Added draw_line and draw_triangle

## 0.5.1
* All: Added Gosu::File and made it the prefererred option over loadFile/saveFile

## 0.5.0
* All: Fixed Song::playing
* All: Replaced Gosu::Streams by new Gosu::IO system
* Win: Fixed Gosu::argument() splitting
* Win: Fixed Gosu::argument() range checking

## 0.4.3
* All: globally replaced Bitmap::replace() by applyColorKey() for color keying
* All: added Win::appFilename and Win::appDirectory
* All: added Gosu/Compression.hpp

## 0.4.2
* All: fixed some bugs in Song
* All: multiple instances of Audio prohibited
* All: added distance()
* All: added numpad keyboard IDs
* Unix: Compile OpenAL if fmod isn't found

## 0.4.1
* Ruby: Some documentation improvements
* Ruby: Linux bug fixes
* Ruby: draw_quad fixed

## 0.4.0
* All: merged documentation and website into one
* All: tutorial greatly improved
* Ruby: tutorial now supports Ruby
* Ruby: reference improved

## 0.3.2
* MSVC: fixed linker errors (remains of MSVC6 compatibility)
* GCC: improved config script
* Ruby: added Linux support
* Ruby: improved exception stability

## 0.3.1
* MSVC: removed non-working MSVC6 compatibility (hopeless)

## 0.3.0
(initial public release based on internal libraries)