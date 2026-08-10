Wraithgate Vocoder
Ethereal 32-Band Spectral & Ghost-Driven Vocoder
Developed by Spectral Garden
Wraithgate Vocoder is a high-performance, real-time spectral morphing processor designed for Windows VST3 hosts. It bridges the frequency characteristics of an incoming Modulator (traditionally a vocal or speech source) with a Carrier (internal synthesized waves or an external sidechained instrument) through a highly optimized 32-band filterbank, enhanced by a unique Spectral Ghost Engine.
🛠️ System Requirements & Specifications
Platform: Windows 10 / 11 (64-bit)
Plugin Format: VST3 only
Host Compatibility: Any standard Windows VST3 Digital Audio Workstation (Ableton Live, FL Studio, Reaper, Cubase, etc.)
Rendering Engine: GPU-accelerated via JUCE OpenGLContext for ultra-smooth 60 FPS visual feedback.
System Architecture & Signal Flow
code
Text
[ AUDIO INPUT (Stereo) ]
       |
       +-----------------------+
       | (Left Channel)        | (Right Channel)
       v                       v
[ Modulator Input ]     [ External Carrier ]
       |                       |
       v                       | (If sidechain active)
[ 32-Band Analysis ]           |
       |                       v
       v                [ Carrier Selector ] <--- [ Internal Generator ]
[ 32x Envelope Followers ]     |                  (Noise, Saw, Square)
       |                       |
       | (Modulator Energy)    v
       |                [ 32-Band Synthesis Filterbank ]
       +-----------------> [ * ] <-----------------+ (Envelope Multiplication)
                           |
                           v
                 [ Spectral Ghost Engine ]
                  - Phase Drift (LFO Wobble)
                  - Gaussian Smear (1D Blur)
                  - Spectral Density (Bin Gating)
                  - Stereo Width (L/R Phase Interleaving)
                           |
                           v
                [ Breath Control (HF Noise) ]
                           |
                           v
              [ Post-EQ Tone Tilt & Limiter ]
                           |
                           v
              [ Dry/Wet Mix Crossfade ]
                           |
                           v
                 [ OUTPUT BUFFER ]
 Control Parameter Reference
1. Modulator & Global Controls
Input Gain (-24.0 dB to +24.0 dB): Controls the incoming amplitude of the modulator signal before it hits the analysis filterbank.
Output Gain (-24.0 dB to +24.0 dB): Post-limiter gain stage adjusting the final output level.
Mix (0.0 to 1.0): Blends between the unprocessed dry signal (modulator input) and the processed vocoded signal.
Tone (0.0 to 1.0): A post-EQ tilt filter. Setting this to 0.5 is flat; below 0.5 boosts low frequencies while attenuating highs; above 0.5 tilts the spectrum toward bright, airy spectral highs.
Bypass (On/Off): Initiates a 50 ms click-free linear crossfade directly between the dry input buffer and wet output buffer.
Oversampling (Off, 2x, 4x, 8x): Processes the entire DSP path at an elevated sample rate using a polyphase IIR half-band filterbank, dramatically reducing filter-aliasing artifacts when modulating sharp waveforms.
Eco Mode (On/Off): Decimates the envelope follower and ghost engine calculations to every second sample, conserving CPU threads on older systems.
2. Carrier Controls
Carrier Source (Noise, Saw, Square, External): Selects the sound source fed into the synthesis filterbank. "External" routes the right stereo input channel as a sidechain.
Carrier Pitch (40.0 Hz to 440.0 Hz): Adjusts the fundamental frequency of the internal Saw and Square oscillators.
Formant Shift (-12.0 st to +12.0 st): Transposes the center frequencies of the synthesis filterbank relative to the analysis filterbank. Shifting upward yields brighter, childlike speech timbres; shifting downward creates deep, guttural tones.
Breath Control (0.0 to 1.0): Injects high-frequency white noise into the upper bands of the synthesis output when high-frequency energy is detected in the modulator, ensuring sibilant consonants ("s", "t", "ch") remain highly intelligible.
3. Ghost Engine Controls
Ghost Amount (0.0 to 1.0): Increases the LFO-driven phase wobble, causing bandpass frequencies to drift independently, generating detuned, chorus-like dispersion.
Smear (0.0 to 1.0): Adjusts the radius of the 1D frequency-domain Gaussian blur. Higher settings smooth out sharp formant transitions into an ethereal, pad-like wash.
Density (0.0 to 1.0): Controls the probability threshold of bin activation. Lower values force random bands to drop out, creating a flickering, disintegrating spectral effect.
Width (0.0 to 1.0): Introduces LFO phase offsets between the left and right synthesis filters, generating wide stereo widening.
Attack Time (1.0 ms to 1000.0 ms): Configures the rise time of the envelope followers. Faster times capture transient plosives; slower times lag, creating soft, swelling transitions.
Release Time (5.0 ms to 3000.0 ms): Configures the decay rate of the envelope followers. High values result in long, atmospheric tails.
 MIDI Learn Implementation
Wraithgate Vocoder features an integrated, right-click MIDI mapping system:
To Map: Right-click any dial on the interface. A popup menu will materialize. Select "Learn MIDI CC". The plugin will automatically monitor incoming MIDI messages and map the first detected Controller Number (CC) to that target parameter.
To Unmap: Right-click a mapped dial and select "Forget MIDI CC" to clear the assignment.
Storage: MIDI assignments are automatically serialized into the plugin's host state XML chunk when saving projects.
 Preset Management & File Structures
User presets are written as raw JSON files (.json) to prevent platform dependencies.
Windows Preset Directory:
C:\Users\<Username>\Documents\Coven Audio\Wraithgate Vocoder\Presets\
Format: Standard UTF-8 JSON.
Action: To share presets, copy .json files directly into this directory and refresh the instance or click any category inside the preset browser to update the listing.
