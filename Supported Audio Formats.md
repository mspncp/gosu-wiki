# Supported Audio Formats

This list is populated using the semi-automated script from `feature_tests/audio_formats.rb`. It is important to note that many container formats, such as WAV or OGG, can contain several types of audio data. Recommended formats for compatibility are PCM WAV (not the weird floating-point kind) and Ogg Vorbis.

                    Format|Sample (OS X)|Song (OS X)  |Sample (Windows)|Song (Windows)|Sample (Linux)|Song (Linux)
--------------------------|--------------|------------|----------------|--------------|--------------|------------
          aiff 32bit float|      &#x2713;|    &#x2713;|                |              |              |            
              au 16bit pcm|      &#x2713;|    &#x2713;|                |              |              |            
        caf be 16bit 44khz|      &#x2713;|    &#x2713;|                |              |              |            
        caf le 16bit 44khz|      &#x2713;|    &#x2713;|                |              |              |            
         caf le 8bit 44khz|      &#x2713;|    &#x2713;|                |              |              |            
              general midi|              |            |                |              |              |            
           impulse tracker|              |            |                |      &#x2713;|              |    &#x2713;
           mp3 128k stereo|      &#x2713;|    &#x2713;|        &#x2713;|      &#x2713;|              |    &#x2713;
mp3 avg 96kbit jointstereo|      &#x2713;|    &#x2713;|        &#x2713;|      &#x2713;|              |    &#x2713;
                ogg vorbis|      &#x2713;|    &#x2713;|        &#x2713;|      &#x2713;|      &#x2713;|    &#x2713;
             wav 16bit pcm|      &#x2713;|    &#x2713;|        &#x2713;|      &#x2713;|      &#x2713;|    &#x2713;
             wav 32bit pcm|      &#x2713;|    &#x2713;|                |              |              |            
         wav 4bit ms adpcm|      &#x2713;|    &#x2713;|                |              |      &#x2713;|            

OS X refers to both OS X and iOS, given that Apple keeps its frameworks in sync. I've thrown in a selection of CAF formats since they are popular on iOS.