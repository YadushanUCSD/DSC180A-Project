# Vowel Blend Map

Single-file HTML, canvas, Web Audio, no libraries.

## Idea
Vowels sit at the corners of a regular shape. Place a point inside; the sound is rebuilt from harmonics as a weighted blend of the corner vowels. Halfway along an edge = exactly 50/50.

## Layout and weights
- 3 vowels (default ɑ / i / u): equilateral triangle, so every pair is equidistant. 4–6 vowels: regular polygon (only 3 points can be mutually equidistant in 2D); each vowel equidistant from its neighbours and the centre.
- Weights = Wachspress coordinates (barycentric for the triangle): 100% at a corner, linear along edges, smooth inside. Point is clamped to the shape and snaps to corners, edge midpoints and the centre.
- Corner vowels selectable from 10 Peterson & Barney vowels (men's / women's tables by Voice).

## Synthesis
- Source 1/n (−6 dB/oct) through a cascade of 5 two-pole resonators (F1–F3 from the table, F4/F5 fixed), gain 1 at 0 Hz. Harmonics up to 5 kHz (max 48), RMS-normalized.
- Blend "Formants": F1–F5 interpolated in log frequency, bandwidths linearly → a true in-between vowel.
- Blend "Harmonic levels": each harmonic's dB averaged across the corners (sounds more like layering); F1/F2 then estimated from peaks.
- Audio: one sine oscillator per harmonic, gains ramped with setTargetAtTime; optional vibrato (5.2 Hz, 18 cents) via a shared LFO scaled per harmonic; compressor as limiter.
- Hold mouse on the map to hear, or Play to latch. Space toggles; arrows nudge.

## Readouts
Mix chips, closest vowel (log F1/F2 distance), F1–F3, harmonic bar chart in dB with the blended envelope dashed, 3-period waveform.

## Ideas
Glide/path recording between vowels, glottal pulse source, add F1–F2 vowel-space plot, load the user's own recorded vowels (via Harmonic Lab analysis) as corners.
