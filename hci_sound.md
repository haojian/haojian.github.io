Sound
===========


- [Motor And Sensory Homunculus](http://www.autismindex.com/Therapies/Therapy_Key_Word_Site_Map/sensory/motor_sensory_homunculus.html)

## Audio transform
- speed up audio without changing pitch
	- [Audacity change speed](http://wiki.audacityteam.org/wiki/Change_Speed)
		- Open Effect > Change Tempo (which changes tempo without affecting pitch)
- [soundtouch](http://www.surina.net/soundtouch/soundstretch.html#examples)


## Data set
- [VocalSketch: Vocally Imitating Audio Concepts](https://static1.squarespace.com/static/552210bae4b0c19f89444531/t/55261514e4b080e2d1bc28ec/1428559124627/CartwrightPardo_2015.pdf)


## Audio Processing Tools
- [Python Audio Analysis Library: Feature Extraction, Classification, Segmentation and Applications](https://github.com/tyiannak/pyAudioAnalysis)
- [Change the bpm of a song while playing it in python](http://stackoverflow.com/questions/4024389/change-the-bpm-of-a-song-while-playing-it-in-python)
- [multichannel audio source separation](http://www.loria.fr/~aliutkus/kaml/)
- [audio segmentation](https://gforge.inria.fr/projects/audioseg): AudioSeg is a toolkit dedicated to audio segmentation and
classification of audio streams
- [aubio](http://aubio.org/): aubio is a tool designed for the extraction of annotations from audio signals.
- [The SoX of Silence](http://digitalcardboard.com/blog/2009/08/25/the-sox-of-silence/)

## Demo
- [python implementation](https://github.com/Katee/quietnet)
- [Low Pass filter web demo](http://www.cnblogs.com/hustskyking/p/webAudio-filter.html)


- [DB effects](http://www.sengpielaudio.com/calculator-levelchange.htm)
- [Hearing test](http://www.audiocheck.net/testtones_hearingtestaudiogram.php)
- [Online sound editing](https://twistedwave.com/online/)
- [Audacity](http://audacity.sourceforge.net/)
- [PortAudio - cross-platform Audio I/O](http://www.portaudio.com/)


## Android 
- Get the audio from two different speakers:
	- [Android Stereo recording](http://stackoverflow.com/questions/17982714/android-stereo-recording-exact-same-data-from-two-different-channels)
	- [How to access the second mic android such as Galaxy 3](http://stackoverflow.com/questions/15418267/how-to-access-the-second-mic-android-such-as-galaxy-3)
	- [How to do stereo recording using the AudioRecord](http://stackoverflow.com/questions/14627246/how-can-i-record-2-microphone-in-android-simultaneously)
	- [code in OpenSL recording](http://cabbage.googlecode.com/svn/trunk/JuceLibraryCode/modules/juce_audio_devices/native/juce_android_OpenSL.cpp)
	- [Playing back sound coming from microphone in real-time](http://stackoverflow.com/questions/5728454/playing-back-sound-coming-from-microphone-in-real-time)
	- [OpenSL Documentation](https://www.khronos.org/registry/sles/specs/OpenSL_ES_Specification_1.0.1.pdf)

## Signal Processing
- [Fast FFT in JNI](https://code.google.com/p/scalalab/wiki/JavaFFTvsNative)
- [Bandpass filter](http://stackoverflow.com/questions/16389205/simple-bandpass-filter-in-java)
- [Matlab's code in Bandpass filter](http://www.ligo-wa.caltech.edu/~cheryl.vorvick/etmx2007/OldStuffFromPCLaptop/MATLAB6p1/toolbox/signal/signal/firls.m)
- [Sound Classification](http://stackoverflow.com/questions/441438/which-algorithm-should-i-use-for-signal-sound-one-class-classification)
- [Sound processing in matlab](http://homepages.udayton.edu/~hardierc/ece203/sound.htm)
- [Fast FFT in JNI](https://code.google.com/p/scalalab/wiki/JavaFFTvsNative)
- [Matched filter in matlab](http://stackoverflow.com/questions/19468733/how-to-implement-a-matched-filter)
- [State of art chirp finding](https://github.com/skymoo/lalsuite/blob/ce490c58024389142d03e9c9530f6574bb86efd5/lalinspiral/src/FindChirpBCV.h)
- [Matched filtering for fm waveform - matlab](http://www.mathworks.com/help/phased/ug/matched-filtering.html)
- [chirp filter](http://www.qsl.net/dl4yhf/speclab/chirp_filter.htm#implementation)
- [Matlab sound](http://www.icn.ucl.ac.uk/courses/MATLAB-Tutorials/Sessions2008_09/Marieke_Scholvinck/html/Matlab_sounds_complicated.html)


## Typical Audio Signal design requirement
- Dealing with multi-user communication system that share the same time-slots and the same bandwidth.

- Requirement (rank through priority)
	- can detect the exact beginning of the signal
	- each signal in the set is easy to distinguish from (apossibly time-shifted version of) every other signal in the set.
	- each signal in the set is easy to distinguish from a time-shifted version ofitself; (signal from the same phone)
	- fast and easy to process
	- immune to doppler effects


## Audio Ranging Papers

- Robust Range Estimation Using Acoustic and Multimodal Sensing:
	- PN sequence based. 
	- Mobile speakers and microphones' rated power is 0.1 w
	- pseudo-noise sequences as the acoustic signal in most work
	- binary phase shift keying wave form
	- BPSK at 12 kHz chip rate. 
	- Using direct sequence based on a codes from 511 bit code.
	- using the correleation with a different sequence to simulate the noise level. 


- Exploiting Quasi-Orthogonal Chirp signals in Multi-user access communication systems
	- Chirp signal are known to immune to Doppler shift.
	- Chirp rates are selected to keep the used set of chirp signals quasi-orthogonal. (didn't understand the selection criteria yet)
	
- Quasi-orthogonal chirp signals Design for Multi-user CSS system
	- priciples for choosing signal
		- time bandwidth product TmBw >=20 their cross-correlation is less than 0.2
		- cross correlation p <= 0.4. small bit error rate change.
		
- SwordFight: Enabling a new class of Phone-to-Phone Action Games on Commodity Phones
	- 12 Hz with 2cm median error while withstanding up to 0dB noise, multipath and Doppler effect
	- Realtime correlation algorithm based on a special chirp.
	- Addressed dopler effects.
	- Compute auto-correlation before cross-correlation.
	- Deal with occasional tone loss. two alternating codes.

## Open source code

- [基于Android的声波通信原理和源代码](http://www.oschina.net/question/730666_129117)
- [JUC is a wide-ranging C++ class library for building rich cross-platform applications and plugins for all the major operating systems.](http://www.juce.com/)


## Devices

- iPhone 5: 3 microphones (One on the front, one on the bottom, and one on the back). 2 speakers (back and front) [Reference](http://ipod.about.com/od/iPhone5SandiPhone5C/ss/Anatomy-Of-Iphone-5S.htm)
- [Determining the native buffer size and sample rate for OpenSL ES](https://play.google.com/store/apps/details?id=com.levien.audiobuffersize)

- - -



