# RC Low-Pass Filter

This project contains an LTspice simulation of a first-order RC low-pass filter. It shows how a resistor-capacitor network can smooth a pulsed input signal and reduce fast transitions at the output.

## Circuit Overview

The schematic in [RC_Low_Pass_Filter.asc](RC_Low_Pass_Filter.asc) uses:

- Input source: a pulsed voltage source switching between 0 V and 5 V
- Resistor: 10 kΩ
- Capacitor: 0.1 µF
- Output taken across the capacitor

This is a standard passive low-pass filter with the cutoff frequency:

$$f_c = \frac{1}{2\pi RC}$$

Using $R = 10\,k\Omega$ and $C = 0.1\,\mu F$:

$$f_c \approx 159\,Hz$$

The time constant is:

$$\tau = RC = 1\,ms$$

## What the Simulation Demonstrates

- The output responds more slowly than the input.
- Sharp edges are rounded off as the capacitor charges and discharges.
- The circuit acts as a smoothing filter for high-frequency components.

## Files

- [RC_Low_Pass_Filter.asc](RC_Low_Pass_Filter.asc) — LTspice schematic
- [RC_Low_Pass_Filter.plt](RC_Low_Pass_Filter.plt) — saved waveform plot configuration

## How to Use

1. Open [RC_Low_Pass_Filter.asc](RC_Low_Pass_Filter.asc) in LTspice.
2. Run the transient analysis defined in the schematic.
3. Observe the input and output waveforms to see the filtering behavior.

## Notes

The simulation uses a transient analysis over 60 ms, which is sufficient to observe the charging and discharging behavior of the capacitor clearly.