# Hacking Guide for Contributors

## Architecture

### C++ and Ruby

Gosu is implemented as a layer of C++/Objective-C on top of the SDL 2 library and operating system APIs.
The C++ source code lives in [`src/`](https://github.com/gosu/gosu/tree/master/src), the headers in [`Gosu/`](https://github.com/gosu/gosu/tree/master/Gosu).

Gosu is made available to Ruby using [SWIG (Simplified Wrapper and Interface Generator)](http://www.swig.org/). See the `swig` task in the [Rakefile](https://github.com/gosu/gosu/blob/master/Rakefile) for the full command line, and note that the generated file needs additional patching to work.

### The Rendering System

Gosu does not use the Z-ordering provided by OpenGL, but instead serialises all rendering operations into a [`DrawOp`](https://github.com/gosu/gosu/blob/master/src/DrawOp.hpp).
These `DrawOp`s are then added to a [`DrawOpQueue`](https://github.com/gosu/gosu/blob/master/src/DrawOpQueue.hpp) and sorted by their Z-coordinate right before being rendered (in `DrawOpQueue::performDrawOpsAndCode`).

## Recommended Workflows

Here are some workflows that allow for a relatively quick feedback cycle while working on Gosu.

### Using RubyGems on Linux or a Mac (Ruby)

The best way to test the full Gosu stack (C++ core, Ruby gem) is to rebuild and install the RubyGem:

```bash
# This gem is necessary for building Gosu
[sudo] gem install rake-compiler
# This is the version of the Gosu gem to build - I always use 9.9.9
export GOSU_RELEASE_VERSION=9.9.9
# If changes to the Ruby/Gosu interface have been made (needs SWIG from Homebrew/apt)
rake swig
# This builds the gem by bundling relevant source code files
rake gem

gem install pkg/gosu-9.9.9.gem
# ...now run a few tests to see whether your change was effective ...
rake test # for example Gosu's own test suite
# Then uninstall this development version of Gosu:
gem uninstall gosu -v 9.9.9
```

### Xcode & local CocoaPod (C++)

The podspec for the C++ Tutorial (in `examples/Tutorial`) includes Gosu as a local "development pod" using a relative path (`../Gosu`).
Because of this, all of the Gosu source files will be added *directly* to the target project during `pod install`.
Every change in these files will be picked up when you hit cmd+R to run your game.

When you add a source code file to Gosu, you will need to modify the `Gosu.podspec` file and run `pod install` again (to add the file to the Xcode project).

## Code Style

See [CONTRIBUTING.md](https://github.com/gosu/gosu/blob/master/CONTRIBUTING.md).