# Supported Audio Formats

The short version is: If you are not interested in iOS, just use common WAV encodings or Ogg Vorbis files for everything. If you also want to deploy on iOS, you should use music in a format that is hardware accelerated such as MP3 and M4A. Gosu Touch also supports Ogg Vorbis music on iOS, but it will slow your game down a lot, and I may drop support altogether at one point.

The long version is that Gosu on Windows and Linux uses libsndfile for audio decoding. Its website sports a comprehensive list of all supported formats: http://www.mega-nerd.com/libsndfile/

Gosu on OS X and iOS uses the AudioToolkit and AVFoundation frameworks in addition to the Ogg Vorbis libraries to support both Ogg Vorbis files (software decoded) as well as everything that Apple supports on the OS level: CAF, MP3, M4A, WAV, AIFF...