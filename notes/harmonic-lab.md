# Harmonic Lab — Part 1 (harmonics & spectra) + voice analysis + filter

Single-file HTML, canvas, no libraries. A standalone copy is needed for the microphone, since artifacts on this account can't use the mic. The artifact supports "Load recording" instead.

## Synth features
- Fundamental f0: log slider 20–2000 Hz + number input, note name and cents.
- Harmonic amplitude bar chart (1–32 harmonics): drag bars or use sliders; Linear/dB toggle. Bars above Nyquist faded.
- Presets: Sine, Square, Sawtooth, Triangle, Hollow (odd), Reset (also set phases 0/π).
- Waveform panel (3 periods, ms axis, formula with phases).
- Fourier transform: 16384-pt FFT, Hann, dB/linear, linear/log Hz, hover readout.
- Audio: Web Audio PeriodicWave oscillator (amplitudes + phases), play/stop + volume.

## Voice input (v2)
- Microphone: getUserMedia with echo cancellation, noise suppression and AGC off; AnalyserNode fftSize 32768. Live view updates the bars, the waveform overlay (recorded vs rebuilt), the spectrum, f0, clarity and formants at ~25 fps.
- Capture (button or Space) freezes the last ~0.7 s and analyzes it. Play tone while live auto-captures first to avoid feedback.
- Load recording: decodes an audio file, auto-picks the loudest 0.6 s, overview strip to click another region.
- Analysis: YIN pitch (60–1000 Hz, threshold 0.15) on 7 segments → median; f0 refined by maximizing harmonic energy (±1.2%); per-harmonic least-squares sinusoid fit at exact n·f0 over a Hann window of whole periods (≥80 ms); amplitudes averaged across segments, phases from the loudest segment, with the origin shifted so the fundamental's phase is 0. H = clamp(floor(5000/f0), 8, 32). Amps normalized so the max = 1.
- Formants: F1 = strongest harmonic in 200–1000 Hz, F2 = strongest in max(F1+250, 650)–3000 Hz, refined by a parabolic fit in dB. Closest vowel uses Peterson & Barney averages (men's values if f0 ≤ 165 Hz, else women's). Rough guess only.
- "Play recording" plays the analyzed region, peak-normalized to match the synth's loudness.

## Filter (v3): source–filter model
- Signal chain: source → filter → output. The output is what plays, and what the waveform, Fourier transform and solid bars show. Outlined bars = the bars (the target vowel).
- Source: "All harmonics at max" (flat, all phases 0) or "Bars as set".
- Filter types: Vowel formants (cascade of 3 two-pole resonators F1–F3, each with frequency and bandwidth, gain 1 at 0 Hz, plus spectral tilt in dB/octave referenced to 100 Hz), and analog 2nd-order low-pass / high-pass / band-pass (cutoff + Q).
- How it's applied: for a steady tone, filtering = multiplying each harmonic by |H(n·f0)| and adding arg H(n·f0) to its phase. Output normalized so the loudest harmonic = 1. The filter curve (scaled by the same gain) is drawn on the harmonics chart and dashed on the FFT.
- Vowel presets: Peterson & Barney F1/F2/F3 (men's if f0 ≤ 165 Hz, else women's), bandwidths 80/100/160 Hz, tilt −6 dB/oct.
- Fit filter to vowel: fits F1–F3, B1–B3 and tilt so a flat source matches the bars in dB (overall gain ignored). Weights: harmonics above −35 dB = 1, above −50 dB = 0.5, quieter = 0.05 (otherwise the noise floor pulls F3 up). Coordinate descent from 3 seeds (peak-picked formants, nearest P&B vowel, 500/1500/2500). About 0.5 s.
- Filter is ignored during live mic view. Dragging bars is blocked while the source is flat.
- Test on synthetic /ɑ/ (true formants 730/1090/2440): fit found 719/1083/2494 Hz with 1.9 dB average error.
- The filtered output's phases come from the filter, not the voice, so its waveform looks different from the recording even when the harmonic strengths match.

## Ideas for later parts
- Amplitude envelope (ADSR) and vibrato on playback, glottal-pulse source, spectrogram, side-by-side comparison of vowels, LPC formant estimation, real-time filtering of the live mic.
