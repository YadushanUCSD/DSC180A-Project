# Wave Mixer (sine additive mixer)

Video walkthrough: https://youtu.be/j-HT9900lNc

Single-file HTML, canvas, Web Audio, no libraries.

## Features
- Type a frequency (1–20,000 Hz) and amplitude, press Add (or Enter); quick-add buttons for common pitches.
- Frequency list with note name, cents and period; click a swatch to mute/unmute, ✕ to remove, "Clear all".
- Graph shows each wave (faint, colored) plus their sum; "Clear graph" blanks the plot, "Redraw graph" brings it back.
- Scale: log time-window slider (0.5–500 ms), "Fit 3 cycles of lowest", "Fit beat cycle" (uses GCD of frequencies), amplitude scale slider or auto-fit.
- Readout of the combined repeat period when the mix is periodic.
- Play/stop the summed sound (one oscillator per wave, gains normalized), volume slider, updates live as you edit.
