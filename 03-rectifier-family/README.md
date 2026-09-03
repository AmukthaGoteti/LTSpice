# Diode Rectifier Family

This project studies a four-diode full-wave bridge rectifier with a capacitive filter. The circuit converts a sinusoidal AC source into a unidirectional, smoothed output suitable for a simple DC supply. It demonstrates diode conduction, peak charging, capacitor discharge, and ripple frequency.

## Learning Goals

- Identify the current path through a bridge rectifier during each half-cycle.
- Compare a rectified waveform with a capacitor-filtered waveform.
- Estimate the DC output and ripple before running LTspice.
- Relate load resistance and capacitance to ripple voltage.
- Recognize the limitations of a small-signal diode model in a power-supply circuit.

## Circuit Under Test

The LTspice schematic is [schematic.asc](schematic.asc).

| Component | Value | Purpose |
|---|---:|---|
| V1 | `SINE(0 12 60)` | 12 V peak, 60 Hz source |
| D1-D4 | `1N4148` | Full-wave bridge |
| R1 | 1 kOhm | Load resistor |
| C1 | 100 uF | Reservoir/smoothing capacitor |

The transient analysis directive is:

```spice
.tran 0 100m 0 100m
```

The simulation covers 100 ms, or six cycles of the 60 Hz input.

## How the Bridge Works

The bridge routes current through two diodes on every half-cycle:

- On the positive half-cycle, one diagonal pair conducts.
- On the negative half-cycle, the other diagonal pair conducts.
- The load current keeps the same polarity in both cases.

Therefore, the ripple frequency at the bridge output is twice the input frequency:

$$f_{ripple} = 2 f_{in} = 2(60\ \text{Hz}) = 120\ \text{Hz}$$

Without C1, the output is approximately the absolute value of the input sine wave, minus the forward voltage of two conducting diodes. With C1 installed, the capacitor charges near each input peak and discharges through R1 between peaks.

## Expected Waveforms

Probe these nodes in the waveform viewer:

- `V(IN)`: 60 Hz sinusoidal input, with 12 V peak amplitude.
- `V(OUT)`: full-wave rectified and capacitor-filtered output.
- `I(R1)`: load current, approximately `V(OUT) / 1 kOhm`.

After startup, `V(OUT)` should show:

- A positive voltage near the source peak minus two diode drops.
- Two recharge events per input cycle.
- A sawtooth-like ripple as C1 discharges through R1.
- A ripple period of about 8.33 ms.

## Hand Calculations

### Source values

The source has 12 V peak amplitude, so its RMS value is:

$$V_{in,rms} = \frac{V_{peak}}{\sqrt{2}} = \frac{12}{\sqrt{2}} \approx 8.49\ \text{V}$$

Two bridge diodes conduct in series. Using an approximate forward drop of 0.7 V per diode:

$$V_{DC,peak} \approx 12 - 2(0.7) = 10.6\ \text{V}$$

The actual LTspice value comes from the `1N4148` model and varies with current and temperature.

### Load current

Using the estimated filtered voltage:

$$I_{load} \approx \frac{V_{DC}}{R} = \frac{10.6\ \text{V}}{1\ \text{kOhm}} \approx 10.6\ \text{mA}$$

### Ripple estimate

For a capacitor-input full-wave rectifier, a first-order ripple estimate is:

$$\Delta V \approx \frac{I_{load}}{f_{ripple} C}$$

Substituting the nominal values:

$$\Delta V \approx \frac{10.6\ \text{mA}}{(120\ \text{Hz})(100\ \text{uF})} \approx 0.88\ \text{V}_{pp}$$

This predicts an output that falls by roughly 0.9 V between recharge pulses. The simulated ripple will differ because the diode conduction interval is finite and the diode forward voltage is not constant.

### RC discharge time constant

The capacitor discharges primarily through R1, giving:

$$\tau = RC = (1\ \text{kOhm})(100\ \text{uF}) = 100\ \text{ms}$$

Since $\tau$ is much longer than the 8.33 ms ripple period, the capacitor retains most of its charge between peaks. That is the source of the smoothing effect.

## What to Compare in LTspice

1. Plot `V(IN)` and `V(OUT)` together to verify full-wave polarity reversal and filtering.
2. Measure the steady-state maximum and minimum of `V(OUT)` over one ripple period.
3. Calculate simulated ripple as $V_{max} - V_{min}$ and compare it with the 0.88 V estimate.
4. Measure the average output voltage and load current after startup transients have settled.
5. Plot diode currents to see that each diode conducts only during part of each half-cycle.

## Design Tradeoffs

- Increasing C1 reduces ripple, but increases the short charging pulses and diode peak current.
- Increasing R1 reduces load current and ripple, but makes the output more lightly loaded.
- A bridge loses approximately two diode forward voltages, reducing the available DC output.
- The `1N4148` is a small-signal switching diode. It is useful for learning and simulation, but a practical higher-current rectifier would normally use a suitably rated rectifier diode.
- The 100 ms transient includes startup charging. Measurements should use a later cycle rather than the first peak.

## Key Takeaways

The bridge rectifier makes both halves of the AC waveform useful, changing the ripple frequency from 60 Hz to 120 Hz. The reservoir capacitor charges to approximately the rectified peak and supplies the load between peaks. Ripple is primarily controlled by load current, ripple frequency, and capacitance according to $\Delta V \approx I/(fC)$.
