# DSC180A Project — Agentic Sound Learning

Browser-based tools for exploring sound: harmonics, Fourier spectra, the source–filter model of the voice, and vowel formants. Each app is a single self-contained HTML file (canvas + Web Audio, no build step) — open it in Chrome or Edge.

| App | What it does | Notes |
|---|---|---|
| [Harmonic Lab](apps/harmonic-lab/index.html) | Build a tone from a fundamental and its harmonics; analyze a sung vowel from the mic or a recording; recreate it with a formant filter. | [notes](notes/harmonic-lab.md) |
| [Wave Mixer](apps/wave-mixer/index.html) | Add sine waves, see each one and their sum, hear the mix, find the combined repeat period. | [notes](notes/wave-mixer.md) |
| [Vowel Blend Map](apps/vowel-blend-map/index.html) | Place a point between corner vowels and hear the blended vowel rebuilt from harmonics. | [notes](notes/vowel-blend-map.md) |
| [Hand Theremin](apps/hand-theremin/index.html) | Camera gesture synth (MediaPipe hand tracking): right hand sets pitch and volume, left hand adds harmonics. | [notes](notes/hand-theremin.md) |

## Running locally
Double-click a file to open it, or serve the folder so the microphone and camera work reliably:

```bash
python3 -m http.server 8000
# then open http://localhost:8000/apps/harmonic-lab/ (or apps/hand-theremin/, etc.)
```

Microphone (Harmonic Lab) and camera (Hand Theremin) need a browser permission prompt; they work from `localhost` or `file://` in Chrome/Edge.

## Background
Vowel formant values are the Peterson & Barney (1952) adult averages.
