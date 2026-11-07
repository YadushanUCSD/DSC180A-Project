# DSC180A Project — Agentic Sound Learning

The long-term goal of this project is an application that lets people who cannot speak produce speech with their bodies: specific motions are mapped to specific speech sounds, and performing them in succession produces speech entirely digitally.

This quarter focused on learning the acoustics of sound and speech — sine waves, fundamental frequency and harmonics, the Fourier transform, and the source–filter model of the voice — by building a browser-based tool for each idea. Each app is a single self-contained HTML file (canvas + Web Audio, no build step); open it in Chrome or Edge. Each one has a short video walkthrough below.

## Wave Mixer
Type in frequencies and amplitudes to see each sine wave and their sum, hear the combined sound, and find how often the combined wave repeats.

[![Wave Mixer walkthrough](https://img.youtube.com/vi/j-HT9900lNc/hqdefault.jpg)](https://youtu.be/j-HT9900lNc)

[Open the app](apps/wave-mixer/index.html) · [Notes](notes/wave-mixer.md) · [Watch on YouTube](https://youtu.be/j-HT9900lNc)

## Harmonic Lab
Build a tone from a fundamental and its harmonics and watch its waveform and Fourier transform update live. Sing a vowel into the microphone to measure its pitch, harmonics and formants, then recreate it from its harmonics or with a fitted formant filter.

[![Harmonic Lab walkthrough](https://img.youtube.com/vi/ysGRJu2imYo/hqdefault.jpg)](https://youtu.be/ysGRJu2imYo)

[Open the app](apps/harmonic-lab/index.html) · [Notes](notes/harmonic-lab.md) · [Watch on YouTube](https://youtu.be/ysGRJu2imYo)

## Vowel Blend Map
Vowels sit at the corners of a shape; place a point inside it to hear a vowel blended from the corners, rebuilt from harmonics.

[![Vowel Blend Map walkthrough](https://img.youtube.com/vi/1HsPPfcJtGA/hqdefault.jpg)](https://youtu.be/1HsPPfcJtGA)

[Open the app](apps/vowel-blend-map/index.html) · [Notes](notes/vowel-blend-map.md) · [Watch on YouTube](https://youtu.be/1HsPPfcJtGA)

## Hand Theremin
A webcam tracks both hands: the right hand's pointing direction sets the pitch and its raised fingers set the loudness, while each finger raised on the left hand adds a harmonic.

[![Hand Theremin walkthrough](https://img.youtube.com/vi/4UiIoKLFAgw/hqdefault.jpg)](https://youtu.be/4UiIoKLFAgw)

[Open the app](apps/hand-theremin/index.html) · [Notes](notes/hand-theremin.md) · [Watch on YouTube](https://youtu.be/4UiIoKLFAgw)

## Running locally
Download or clone the repo, then double-click an app's `index.html`, or serve the folder so the microphone and camera work reliably:

```bash
python3 -m http.server 8000
# then open http://localhost:8000/apps/harmonic-lab/ (or apps/hand-theremin/, etc.)
```

Microphone (Harmonic Lab) and camera (Hand Theremin) need a browser permission prompt; they work from `localhost` or `file://` in Chrome/Edge.

## Background
Vowel formant values are the Peterson & Barney (1952) adult averages.
