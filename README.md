# 👻 Wraithgate Vocoder (Spectral Garden)
*Ethereal 32-Band Spectral & Ghost-Driven Vocoder for Windows VST3*

**Wraithgate Vocoder** is a high-performance, real-time spectral morphing audio processor. It cross-analyzes the frequency characteristics of an incoming **Modulator** (traditionally a vocal or speech source) with a **Carrier** (internal synthesized waves or an external sidechained instrument) through an optimized 32-band filterbank, powered by an immersive **Spectral Ghost Engine**.

---

## System Architecture & Signal Flow

```text
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
