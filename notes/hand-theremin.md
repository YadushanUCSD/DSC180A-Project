# Hand Theremin (camera gesture synth)

Single-file HTML, opened locally in Chrome/Edge. MediaPipe HandLandmarker (tasks-vision 0.10.14 via jsDelivr, numHands 2) + Web Audio additive synth.

## Mapping
### Right hand — pitch and volume
- Pitch = pointing direction (wrist → average of extended fingertips). Left 180° = low, up 90° = middle, right 0° = high; log-frequency sweep between Low/High (default 110–1760 Hz, 4 octaves). Pointing down clamps to the nearer side.
- Amplitude = fingers up: 1 → -24 dB, 2 → -18, 3 → -12, 4 → -6, 5 → 0 dB. Fist or hand out of view = silent.
### Left hand — timbre / harmonics
- Fingers up = number of harmonics added on top of the fundamental. 0 (fist or hand out of view) = pure sine; 1 adds 2f, 2 adds 3f … 5 adds up to 6f.
- Setting "Odd only" adds 3f, 5f, 7f, 9f, 11f instead (hollow, clarinet-like).
- Levels follow a natural 1/n roll-off, normalised to equal RMS so adding harmonics changes colour, not loudness. Partials above Nyquist are muted.

## Implementation notes
- Additive synth: 6 sine oscillators, each with its own gain, ramped with setTargetAtTime (60 ms) so harmonics fade in/out without clicks.
- Hand assignment: MediaPipe handedness assumes a mirrored image; raw camera frames are un-mirrored, so its "Left" label = player's right hand. If both hands get the same label, the hand on the raw image's left is treated as the right hand. A "Swap hands" setting flips everything if the camera delivers mirrored frames.
- Finger counts debounced over 6 frames per hand; right-hand direction smoothed.

## Features
- Labeled camera view on the left with a Live indicator and right/left hand status chips; hands drawn in brass (right) and cyan (left) with on-video labels and the pointing arrow.
- Pitch dial, Hz + note/cents readout, 5-pip volume meter, harmonic bar chart (with per-partial Hz), auto-scaled output scope.
- Settings: harmonic series (all / odd), smooth/chromatic/pentatonic steps, low/high Hz, master volume, mirror, tracking overlay, swap hands.
- No-camera fallback: drag the dial for pitch, keys 1–5 for volume, ↑ ↓ for harmonics.

## Troubleshooting
- Camera blocked: open the file in Chrome/Edge; allow camera via the address-bar icon; enable the browser under OS camera privacy settings; close other apps using the camera; or serve with `python3 -m http.server 8000` and open localhost.
- Hands mixed up: tick "Swap hands".

## Changelog
- v3: two hands — right keeps pitch/volume, left adds harmonics (additive synth replaces the single-waveform oscillator and the Waveform setting).
- v2: fixed the "How to play" card covering the video; added camera label, live indicator, tracking-overlay toggle.

## Ideas
- Left-hand height for vibrato or filter cutoff, harmonic presets (organ, brass), recording.
