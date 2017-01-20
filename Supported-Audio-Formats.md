# Supported Audio Formats

The short version is: If you are not interested in iOS, just use common WAV encodings or Ogg Vorbis files for everything. If you also want to deploy on iOS, you should use music in a format that is hardware accelerated such as MP3 and M4A. Gosu Touch also supports Ogg Vorbis music on iOS, but it will slow your game down a lot, and I may drop support altogether at one point.

The long version is that Gosu uses libsndfile for audio decoding on Windows and Linux. Its website lists all supported file formats: http://www.mega-nerd.com/libsndfile/

On macOS and iOS, Gosu uses the AudioToolkit and AVFoundation frameworks to load everything that is not an OGG file. These frameworks support a wide range of audio formats: CAF, MP3, M4A, WAV, AIFF...