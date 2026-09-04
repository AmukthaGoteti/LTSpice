# BJT Common-Emitter Amplifier

This project studies a voltage-divider-biased **2N2222 common-emitter amplifier**. The stage uses an emitter resistor for DC feedback and bias stability, an emitter-bypass capacitor for increased AC gain, and coupling capacitors to isolate the transistor bias point from the source and load.

## Learning Goals

- Establish a stable operating point for an NPN transistor.
- Understand voltage-divider bias and emitter degeneration.
- Derive the small-signal voltage gain of a common-emitter stage.
- Observe the 180-degree phase inversion between input and output.
- Explore how coupling and bypass capacitors set the low-frequency response.
- Use LTspice AC analysis to evaluate gain and bandwidth.

## Circuit Under Test

The LTspice schematic is [schematic.asc](schematic.asc).

| Component | Value | Function |
|---|---:|---|
| V1 | `AC 1` | Small-signal AC input source |
| V2 | 12 V | DC supply |
| Q1 | `2N2222` | NPN amplifying transistor |
| R1 | 47 kOhm | Upper base-bias resistor |
| R4 | 10 kOhm | Lower base-bias resistor |
| R2 | 2.2 kOhm | Collector resistor |
| R3 | 1 kOhm | Emitter resistor for DC stabilization |
| C1 | 1 uF | Input coupling capacitor |
| C2 | 10 uF | Emitter bypass capacitor |
| C3 | 1 uF | Output coupling capacitor |
| R5 | 10 kOhm | Output load |

The schematic uses the following AC analysis directive:

```spice
.ac dec 100 1 10000Meg
```

This sweeps frequency logarithmically from 1 Hz to 10 GHz. The `.op` directive is present but commented out; enabling it is useful for checking the DC operating point before interpreting the AC response.

## Circuit Topology

```text
                         VCC = 12 V
                             |
                            R2
                         2.2 kOhm
                             |
                             +---- C3 ---- OUT
                             |              |
                            C Q1            R5
                       2N2222              10 kOhm
                            E              |
                             +---- R3 -----+---- GND
                             |   1 kOhm
                            C2
                          10 uF
                             |
                            GND

         IN ---- C1 ---- B
                       |
                 R1    +---- R4 ---- GND
              47 kOhm
                |
               VCC
```

C1 and C3 provide DC isolation. R1 and R4 set the base voltage, while R3 sets the emitter current and provides negative feedback. C2 bypasses R3 for AC signals over its effective corner frequency, increasing gain while preserving DC bias stabilization.

## DC Bias Analysis

The bias network can first be approximated by its Thevenin equivalent:

$$V_{TH} = V_{CC}\frac{R4}{R1+R4}$$

$$R_{TH} = R1 \parallel R4$$

For the nominal values:

$$V_{TH} = 12\frac{10\ \text{kOhm}}{47\ \text{kOhm}+10\ \text{kOhm}} \approx 2.11\ \text{V}$$

$$R_{TH} = 47\ \text{kOhm} \parallel 10\ \text{kOhm} \approx 8.25\ \text{kOhm}$$

Using $V_{BE} \approx 0.7\ \text{V}$ and an assumed transistor current gain $\beta$:

$$I_B \approx \frac{V_{TH}-V_{BE}}{R_{TH}+(\beta+1)R3}$$

$$I_E \approx (\beta+1)I_B$$

$$V_E \approx I_E R3$$

$$V_C \approx V_{CC}-I_C R2$$

$$V_{CE} = V_C - V_E$$

The transistor should remain in the forward-active region, with $V_C > V_B$ and a positive $V_{CE}$ comfortably above saturation. The exact LTspice operating point depends on the model's $\beta$, $V_{BE}$, and Early-effect parameters.

## Small-Signal Gain

At midband, C1, C2, and C3 can be treated as approximately short circuits. If C2 fully bypasses R3, the approximate unloaded voltage gain is:

$$A_v \approx -g_m R_C$$

where

$$g_m = \frac{I_C}{V_T}$$

and $V_T$ is approximately 25.9 mV at room temperature. Including the 10 kOhm load, the collector resistance becomes:

$$R_{C,eff} = R2 \parallel R5$$

so a more useful estimate is:

$$A_v \approx -g_m(R2 \parallel R5)$$

At frequencies where C2 does not fully bypass R3, emitter degeneration reduces the gain approximately to:

$$A_v \approx -\frac{g_m(R2 \parallel R5)}{1+g_m R3}$$

The negative sign indicates that the output is inverted by 180 degrees relative to the input.

## Frequency Response

The amplifier has three main low-frequency poles:

### Input coupling capacitor

C1 forms a high-pass network with the resistance seen looking into the amplifier input. A first estimate is:

$$f_{L,in} \approx \frac{1}{2\pi R_{in}C1}$$

where $R_{in}$ includes the bias-network resistance and the transistor's small-signal base input resistance.

### Emitter bypass capacitor

C2 must have a low impedance compared with R3 over the intended signal band. Its approximate corner is:

$$f_{L,e} \approx \frac{1}{2\pi R_{seen,e}C2}$$

Below this frequency, R3 is less bypassed and gain is lower but feedback is stronger.

### Output coupling capacitor

C3 and R5 form another high-pass network. If R5 dominates the output-side resistance:

$$f_{L,out} \approx \frac{1}{2\pi R5 C3}$$

For the nominal output coupling components alone:

$$f_{L,out} \approx \frac{1}{2\pi(10\ \text{kOhm})(1\ \text{uF})} \approx 15.9\ \text{Hz}$$

The overall lower cutoff is set by the highest of the input, emitter, and output corner frequencies. At high frequency, transistor parasitics and the coupling-capacitor impedances determine the gain roll-off.

## LTspice Procedure

1. Enable the `.op` directive and run the operating-point analysis.
2. Confirm that Q1 is forward-active and record `V(B)`, `V(E)`, `V(C)`, `I(R2)`, and `V(CE)`.
3. Re-enable the `.ac` directive and run the logarithmic frequency sweep.
4. Plot `V(OUT)` and `V(IN)` in the dB waveform view.
5. Plot gain using `dB(V(OUT)/V(IN))` and phase using `phase(V(OUT)/V(IN))`.
6. Identify the midband gain and the frequencies where gain is 3 dB below that value.
7. Compare the simulated gain with the small-signal estimate and explain differences caused by loading, incomplete bypassing, and the transistor model.

Because V1 has `AC 1`, the plotted output magnitude directly represents the transfer gain in volts per volt. The input source's DC value is zero, so C1 does not disturb the transistor's DC bias point.

## What to Observe

- `V(OUT)` is inverted relative to the input signal.
- The output is blocked at DC by C3, while the collector has a DC bias voltage before the coupling capacitor.
- Gain rises through the low-frequency region as C1, C2, and C3 become effective.
- The midband gain is approximately flat before transistor parasitics cause high-frequency roll-off.
- The emitter resistor improves bias stability and reduces distortion, at the cost of gain when it is not bypassed.
- The 10 kOhm load reduces gain by loading the collector through the output coupling capacitor.

## Design Tradeoffs

- Increasing R2 can increase voltage gain, but reduces collector-voltage headroom and may push Q1 toward saturation.
- Increasing R3 improves DC and temperature stability, but lowers unbypassed AC gain.
- Increasing C2 lowers emitter degeneration at lower frequencies, but increases component size and startup time.
- Larger C1 or C3 extends the low-frequency response downward.
- The voltage-divider bias network consumes supply current and its Thevenin resistance affects sensitivity to transistor beta.
- A single-transistor stage provides voltage gain but has limited output swing and linearity compared with a feedback amplifier.

## Key Takeaways

A common-emitter amplifier converts a small base-voltage variation into a larger collector-voltage variation through transistor transconductance. R1, R4, and R3 establish a usable DC operating point; R2 and the transistor set the gain; and C1, C2, and C3 shape the frequency response. The output is amplified and phase-inverted, with the best approximation to the midband gain occurring after all three capacitors act as low-impedance AC paths.
