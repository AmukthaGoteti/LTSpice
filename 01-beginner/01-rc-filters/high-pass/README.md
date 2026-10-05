# RC High-Pass Filter

## Overview
This project studies a first-order RC high-pass filter in LTspice. A high-pass filter allows signals above a certain cutoff frequency to pass while attenuating lower-frequency content. It is commonly used in coupling stages, AC coupling, and signal conditioning.

The circuit is built from a series capacitor and a resistor to ground, forming a simple frequency-selective network.

## Objective
- Understand how a capacitor and resistor create a frequency-dependent response
- Observe the gain and phase shift of a high-pass filter
- Verify the cutoff frequency using LTspice AC analysis
- Compare simulation results with the theoretical transfer function

## Circuit Description
The input signal is applied to the left side of the capacitor. The output is taken across the resistor to ground.

In a first-order RC high-pass filter:
- the capacitor is in series with the signal path
- the resistor provides the return path to ground
- low-frequency signals are blocked because the capacitor impedance is large
- high-frequency signals pass because the capacitor impedance becomes small

## Theory
The transfer function for a first-order RC high-pass filter is:

$$
H(s) = \frac{sRC}{1 + sRC}
$$

where:
- $R$ = resistance
- $C$ = capacitance
- $s = j\omega$

The magnitude response is:

$$
|H(j\omega)| = \frac{\omega RC}{\sqrt{1 + (\omega RC)^2}}
$$

The cutoff frequency, or -3 dB point, is:

$$
f_c = \frac{1}{2\pi RC}
$$

This is the frequency where the output power drops to half of the passband value, and the amplitude is reduced by about 3 dB.

## LTspice Implementation
The schematic for this project is stored in:
- `schematic.asc`

This LTspice simulation uses:
- AC source as the input stimulus
- RC network as the frequency-selective stage
- `.ac` analysis to sweep frequency over a wide range

## Simulation Setup
Open the schematic in LTspice and run:

```spice
.ac dec 100 1 1Meg
```

This performs an AC sweep from 1 Hz to 1 MHz with 100 points per decade.

Then plot:
- `V(out)`
- `V(in)`
- or the ratio `V(out)/V(in)` to visualize the filter response

## Expected Behavior
- At very low frequencies, the capacitor impedance is very large, so the output approaches zero
- At mid frequencies, the response rises with frequency
- At high frequencies, the output approaches the input amplitude
- At the cutoff frequency, the output magnitude is reduced to about 70.7% of the input

## Practical Interpretation
A high-pass filter is useful when you want to remove DC offsets or low-frequency drift from a signal while preserving the variations that occur at higher frequencies. In audio and signal-processing systems, this is often used to discard unwanted low-frequency noise, hum, or DC components.

## Files in This Project
- `schematic.asc` — LTspice schematic
- `plots/` — saved waveform and simulation plots
- `README.md` — project notes and theory

## Notes
This example is intended as a beginner-friendly introduction to RC filter behavior. It is a good starting point before exploring second-order filters, resonance, and active filter design.

---

### Summary
An RC high-pass filter is the simplest way to pass AC signals while suppressing low-frequency or DC components. The key design parameter is the cutoff frequency:

$$
f_c = \frac{1}{2\pi RC}
$$

By changing the resistor or capacitor values, the filter can be tuned to pass different frequency ranges.
