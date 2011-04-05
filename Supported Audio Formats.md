# Supported Audio Formats

## (Outdated, this needs to be re-tested on Windows)

This list is populated using the semi-automated script from `feature_tests/audio_formats.rb`. It is important to note that many container formats, such as WAV or OGG, can contain several types of audio data. Recommended formats are Ogg Vorbis and PCM WAV, which are the most usual combinations.

## TODO reformat as HTML for GitHub wiki

|| Platform || aiff 32bit float || au 16bit pcm || caf be 16bit 44khz || caf le 16bit 44khz || caf le 8bit 44khz || general midi || impulse tracker || mp3 128k stereo || mp3 avg 96kbit jointstereo || ogg vorbis || wav 16bit pcm || wav 32bit pcm || wav 4bit ms adpcm ||
|| OS X (Gosu::Sample) || Yes || Yes || Yes || Yes || Yes ||  ||  || Yes || Yes || Yes || Yes || Yes || Yes ||
|| OS X (Gosu::Song)  || Yes || Yes || Yes || Yes || Yes ||  ||  || Yes || Yes || Yes || Yes || Yes || Yes ||
|| Windows (Gosu::Sample) ||  ||  ||  ||  ||  ||  ||  || Yes || Yes || Yes || Yes || || Yes ||
|| Windows (Gosu::Song)  ||  ||  ||  ||  ||  || Yes || Yes || Yes || Yes || Yes || Yes || || Yes ||
|| Linux (Gosu::Sample) ||  ||  ||  ||  ||  ||  ||  ||  ||  || Yes || Yes || ? (TODO) || Yes ||
|| Linux (Gosu::Song)  ||  ||  ||  ||  ||  || Yes || Yes || Yes || Yes || Yes || Yes || ? (TODO) || ||

OS X refers to both Macs and iPhones/iPods. I only tested the CAF formats because they are popular on the iPhone.
