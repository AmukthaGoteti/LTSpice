# The RC Low-Pass Filter — A Complete ECE Guide

---

## 1. Introduction

### What is an RC Low-Pass Filter?

An **RC low-pass filter** is the simplest possible frequency-selective circuit. It is built from just two passive components — one **resistor (R)** and one **capacitor (C)** — arranged so that low-frequency signals pass through to the output almost unchanged, while high-frequency signals are progressively weakened (attenuated).

Think of it as a "frequency gatekeeper": it lets slow-changing signals through the gate, but blocks fast-changing ones.

### Purpose and Practical Applications

The RC low-pass filter is one of the most widely used building blocks in electronics. Typical applications include:

- **Noise/ripple filtering** — smoothing the output of a rectifier in a DC power supply.
- **Anti-aliasing filters** — placed before an ADC to remove high-frequency components that would otherwise cause aliasing.
- **Audio tone control** — rolling off treble frequencies in audio circuits (bass boost/treble cut).
- **Signal conditioning** — removing high-frequency noise picked up by sensors before further processing.
- **Integrator approximation** — at frequencies well above cutoff, the RC low-pass approximates an integrator.
- **Decoupling/bypass networks** — stabilizing supply rails by shunting high-frequency noise to ground.

### Why "Low-Pass"?

The name describes exactly what the circuit does to the *frequency spectrum* of a signal:

- **Low frequencies → passed** (output ≈ input)
- **High frequencies → blocked/attenuated** (output → 0)

Because only the *low* end of the frequency spectrum is allowed to "pass" through with full strength, the circuit is called a **low-pass filter**.

---

## 2. Circuit Diagram

The classic RC low-pass filter is a **series R** followed by a **shunt C** to ground, with the output taken across the capacitor.

```
                    R
        Vin  o----/\/\/\----+----o  Vout
                             |
                            ---
                            --- C
                             |
                             |
                            ---
                             -    Ground (0V)
```

**Node identification:**

| Symbol | Meaning |
|--------|---------|
| **Vin** | Input voltage source (AC or time-varying signal), applied at the left node |
| **R** | Series resistor — carries current from input to output node |
| **C** | Shunt capacitor — connected from the output node to ground |
| **Vout** | Output voltage, measured across the capacitor (node between R and C) |
| **Ground (0V)** | Reference/return node, bottom plate of C connects here |

**Key structural insight:** R and C form a **voltage divider**. Because a capacitor's impedance depends on frequency, this "divider ratio" is *frequency-dependent* — that's the entire mechanism behind the filtering action.

---

## 3. Working Principle

### Behavior at Low Frequencies

At low frequencies (including DC, f → 0), the capacitor's opposition to current flow (its **reactance**, $X_C = \frac{1}{2\pi f C}$) becomes very **large** — approaching infinity as f → 0.

- A very large $X_C$ compared to R means almost no current is "lost" through the capacitor's path in a way that drops voltage across R.
- Since negligible voltage is dropped across R, nearly all of $V_{in}$ appears across C.
- Result: **$V_{out} \approx V_{in}$** — the signal passes through almost unattenuated.

### Behavior at High Frequencies

At high frequencies (f → ∞), $X_C = \frac{1}{2\pi f C}$ becomes very **small** — approaching zero.

- The capacitor behaves almost like a short circuit to ground.
- Almost all of the input voltage is now dropped across R instead.
- Result: **$V_{out} \to 0$** — the signal is heavily attenuated.

### Charging and Discharging of the Capacitor

In the time domain, this frequency behavior corresponds to how fast the capacitor can charge and discharge through R:

- **Charging:** When Vin steps up, current flows through R into C, gradually raising Vout following an exponential curve. The capacitor cannot charge instantly — it takes time proportional to $\tau = RC$.
- **Discharging:** When Vin drops (or is removed), C discharges back through R, and Vout exponentially decays toward zero.

If the input changes **slowly** (low frequency), the capacitor has enough time to fully charge/discharge and track the input — hence passes through. If the input changes **rapidly** (high frequency), the capacitor cannot keep up — it barely charges before the input reverses, so the output stays small — hence attenuated.

This time-domain view and the frequency-domain view ($X_C$ vs frequency) are two sides of the same physical phenomenon.

### How Capacitive Reactance Changes with Frequency

$$X_C = \frac{1}{2\pi f C}$$

This is an **inverse relationship**: as frequency f increases, $X_C$ decreases proportionally. This inverse relationship is the mathematical root of all low-pass behavior — it's why increasing frequency always pushes more of the divided voltage onto R and less onto C.

### Why is the Output Taken Across the Capacitor?

Because the capacitor is the element whose impedance **shrinks** with increasing frequency:

- At low f → $X_C$ large → most voltage appears across C → **large output**
- At high f → $X_C$ small → most voltage appears across R → **small output across C**

If instead we took the output across R, we would get the opposite behavior — a **high-pass filter**. So the choice of *which component you measure across* determines the filter type, not just the R-C arrangement itself.

---

## 4. Mathematical Analysis

### 4.1 Capacitive Reactance

$$X_C = \frac{1}{2\pi f C}$$

**Variables explained:**

| Symbol | Meaning | Unit |
|--------|---------|------|
| $X_C$ | Capacitive reactance — the capacitor's frequency-dependent opposition to AC current | Ohms (Ω) |
| $f$ | Frequency of the input signal | Hertz (Hz) |
| $C$ | Capacitance value | Farads (F) |
| $2\pi$ | Converts frequency (cycles/sec) to angular frequency (radians/sec) | — |

Note: Reactance is not resistance — it does not dissipate energy as heat. It represents the capacitor's opposition to current flow due to charge storage, and it introduces a 90° phase shift between voltage and current in an ideal capacitor.

### 4.2 Voltage Divider Equation (Complex Impedance Form)

**Step 1 — Represent the capacitor as a complex impedance.**

In phasor/AC analysis, a capacitor's impedance is:

$$Z_C = \frac{1}{j\omega C}$$

where $\omega = 2\pi f$ is the angular frequency (rad/s), and $j = \sqrt{-1}$ is the imaginary unit (used in electrical engineering instead of $i$ to avoid confusion with current).

**Step 2 — Apply the voltage divider rule.**

R and $Z_C$ are in series across $V_{in}$, and $V_{out}$ is measured across $Z_C$ (the capacitor). For any two series impedances, the voltage divider rule gives:

$$V_{out} = V_{in} \times \frac{Z_C}{R + Z_C}$$

**Step 3 — Substitute $Z_C = \dfrac{1}{j\omega C}$:**

$$V_{out} = V_{in} \times \frac{\dfrac{1}{j\omega C}}{R + \dfrac{1}{j\omega C}}$$

**Step 4 — Multiply numerator and denominator by $j\omega C$ to clear the fraction:**

$$V_{out} = V_{in} \times \frac{\dfrac{1}{j\omega C} \times j\omega C}{\left(R + \dfrac{1}{j\omega C}\right)\times j\omega C}$$

$$V_{out} = V_{in} \times \frac{1}{R \cdot j\omega C + 1}$$

**Step 5 — Rearranging:**

$$V_{out} = V_{in} \times \frac{1}{1 + j\omega R C}$$

This is the **frequency-domain transfer function** of the RC low-pass filter (with $s = j\omega$, matching the Laplace form derived next).

### 4.3 Transfer Function (Laplace Domain)

**Step 1 — Replace $j\omega$ with the general Laplace variable $s$.**

In circuit analysis, impedances are often written using the Laplace variable $s$ instead of $j\omega$, which allows analysis of transient (not just sinusoidal steady-state) behavior. The capacitor impedance becomes:

$$Z_C(s) = \frac{1}{sC}$$

**Step 2 — Apply the same voltage-divider derivation as before, using $s$ in place of $j\omega$:**

$$H(s) = \frac{V_{out}(s)}{V_{in}(s)} = \frac{Z_C(s)}{R + Z_C(s)} = \frac{\dfrac{1}{sC}}{R + \dfrac{1}{sC}}$$

**Step 3 — Multiply numerator and denominator by $sC$:**

$$H(s) = \frac{1}{sRC + 1}$$

**Final transfer function:**

$$\boxed{H(s) = \frac{1}{1 + sRC}}$$

**Meaning of each term:**

- **Laplace variable $s$**: A complex frequency variable, $s = \sigma + j\omega$, used to generalize sinusoidal (frequency-domain) analysis to include transient/exponential behavior. Setting $s = j\omega$ recovers the pure sinusoidal steady-state response.
- **Pole**: The transfer function has a **pole** where the denominator equals zero:
$$1 + sRC = 0 \implies s = -\frac{1}{RC}$$
  This pole lies on the negative real axis of the s-plane, confirming the circuit is **stable** (poles in the left-half plane → bounded response → no oscillation or runaway growth). The pole location directly sets the cutoff frequency (see Section 5).
- **First-order system**: The transfer function has only **one pole and no zeros**, and the denominator is a first-degree polynomial in $s$. This means the circuit's differential equation is first-order, its step response is a single exponential, and its frequency response rolls off at a constant rate of **20 dB/decade** beyond cutoff (see Section 6).

---

## 5. Cutoff Frequency

### Derivation of $f_c$

The **cutoff frequency** (also called the **corner frequency** or **-3 dB frequency**) is defined as the frequency at which the output power drops to half its low-frequency value, equivalently where output voltage magnitude drops to $\frac{1}{\sqrt{2}} \approx 0.707$ of the input.

**Step 1 — Start from the magnitude of $H(j\omega)$:**

$$|H(j\omega)| = \left|\frac{1}{1+j\omega RC}\right| = \frac{1}{\sqrt{1+(\omega RC)^2}}$$

**Step 2 — Set this equal to $\dfrac{1}{\sqrt{2}}$** (the -3 dB condition):

$$\frac{1}{\sqrt{1+(\omega RC)^2}} = \frac{1}{\sqrt{2}}$$

**Step 3 — Cross-multiply / equate denominators:**

$$\sqrt{1+(\omega RC)^2} = \sqrt{2}$$

**Step 4 — Square both sides:**

$$1 + (\omega RC)^2 = 2$$

**Step 5 — Solve for $(\omega RC)^2$:**

$$(\omega RC)^2 = 1 \implies \omega RC = 1 \implies \omega_c = \frac{1}{RC}$$

**Step 6 — Convert angular frequency $\omega_c$ to ordinary frequency $f_c$** using $\omega = 2\pi f$:

$$2\pi f_c = \frac{1}{RC}$$

$$\boxed{f_c = \frac{1}{2\pi RC}}$$

### Why -3 dB?

$$\text{Gain}_{dB} = 20\log_{10}\left(\frac{1}{\sqrt{2}}\right) = 20 \times (-0.1505) \approx -3.01\ \text{dB}$$

The "-3 dB point" is a widely-adopted engineering convention because it corresponds to the **half-power point**: since power is proportional to $V^2$, a voltage ratio of $\frac{1}{\sqrt2}$ corresponds to a power ratio of $\left(\frac{1}{\sqrt2}\right)^2 = \frac{1}{2}$ — exactly half the input power. This makes -3 dB a natural, physically meaningful threshold for defining "where the filter starts cutting off," rather than an arbitrary number.

### Verifying $|H(j\omega)| = \frac{1}{\sqrt2}$ at Cutoff

At $\omega = \omega_c = \frac{1}{RC}$:

$$|H(j\omega_c)| = \frac{1}{\sqrt{1+(\omega_c RC)^2}} = \frac{1}{\sqrt{1 + (1)^2}} = \frac{1}{\sqrt2} \approx 0.707$$

This confirms algebraically that at $f = f_c$, the output magnitude is exactly $70.7\%$ of the input — the defining condition of the cutoff frequency.

---

## 6. Gain

### Linear Gain

The magnitude of the transfer function gives the **linear voltage gain** at any frequency f:

$$|H(j\omega)| = \frac{1}{\sqrt{1+(2\pi f RC)^2}}$$

This directly follows from Section 5, Step 1, using $\omega = 2\pi f$. It tells you what fraction of $V_{in}$'s amplitude appears at $V_{out}$ for a sinusoid of frequency f.

- At $f \ll f_c$: the term $(2\pi f RC)^2 \ll 1$, so $|H| \approx 1$ (unity gain, full pass).
- At $f \gg f_c$: the term $(2\pi f RC)^2 \gg 1$, so $|H| \approx \frac{1}{2\pi f RC}$ (gain falls off inversely with frequency).

### Gain in Decibels

$$Gain_{dB} = 20\log_{10}|H(j\omega)|$$

Decibels are used because:
1. They compress a very wide dynamic range into manageable numbers.
2. Cascaded stages' gains simply **add** in dB instead of multiplying.
3. They align naturally with how the human ear perceives loudness (logarithmic).

### Why -20 dB/decade?

**Step 1 —** For $f \gg f_c$, approximate:

$$|H(j\omega)| \approx \frac{1}{2\pi f RC} = \frac{f_c}{f}$$

**Step 2 —** Convert to dB:

$$Gain_{dB} \approx 20\log_{10}\left(\frac{f_c}{f}\right) = 20\log_{10}(f_c) - 20\log_{10}(f)$$

**Step 3 —** Consider what happens when frequency increases by a **decade** (×10). Replace $f$ with $10f$:

$$Gain_{dB}(10f) = 20\log_{10}(f_c) - 20\log_{10}(10f) = 20\log_{10}(f_c) - 20\log_{10}(f) - 20\log_{10}(10)$$

Since $\log_{10}(10) = 1$:

$$Gain_{dB}(10f) = Gain_{dB}(f) - 20\ \text{dB}$$

**Conclusion:** every time frequency increases 10×, the gain drops by exactly **20 dB**. This constant slope — **-20 dB/decade** (equivalently **-6 dB/octave**) — is a direct signature of a **first-order** system (one pole, no zeros). Each additional real pole in a filter adds another -20 dB/decade to the ultimate roll-off slope.

---

## 7. Phase Shift

### Derivation

Starting from the transfer function in phasor form:

$$H(j\omega) = \frac{1}{1+j\omega RC}$$

The phase of $H(j\omega)$ is the negative of the phase of the denominator (since the numerator is a real, phase-less constant, 1):

$$\phi = -\angle(1 + j\omega RC) = -\tan^{-1}\left(\frac{\omega RC}{1}\right)$$

Substituting $\omega = 2\pi f$:

$$\boxed{\phi = -\tan^{-1}(2\pi f RC)}$$

The negative sign indicates that $V_{out}$ **lags** $V_{in}$ — the output waveform reaches its peak *after* the input, because the capacitor takes time to charge.

### Physical Meaning of Key Phase Values

| Frequency | Phase $\phi$ | Physical Meaning |
|-----------|-------------|-------------------|
| $f \to 0$ (DC/very low f) | **0°** | Capacitor charges essentially instantly relative to signal changes; output tracks input with no delay. |
| $f = f_c$ | **-45°** | At the corner frequency, the output lags input by exactly one-eighth of a cycle. This is the "midpoint" of the phase transition. |
| $f \to \infty$ | **-90°** | Output significantly lags input; in the extreme, the capacitor voltage lags current by 90° (fundamental capacitor I-V relationship), and almost no output amplitude remains anyway. |

This behavior — phase transitioning smoothly from 0° to -90°, passing through -45° exactly at $f_c$ — is a hallmark feature used to identify a first-order low-pass response on a Bode phase plot.

---

## 8. Frequency Response

### Passband, Cutoff Region, Stopband

| Region | Frequency Range | Behavior |
|--------|-----------------|----------|
| **Passband** | $f \ll f_c$ | Gain ≈ 0 dB (unity); signal passes with negligible attenuation; phase ≈ 0°. |
| **Cutoff region** | $f \approx f_c$ | Gain transitioning through -3 dB; phase transitioning through -45°; the "knee" of the response. |
| **Stopband** | $f \gg f_c$ | Gain falls at -20 dB/decade; phase approaches -90°; signal strongly attenuated. |

### Bode Magnitude Plot (Description)

- **Flat line at 0 dB** for $f < f_c$ (approximation: exactly flat only asymptotically; true curve gently rolls off approaching $f_c$).
- **Corner/knee at $f = f_c$**, where actual gain is -3 dB (the asymptotic approximation would show 0 dB up to $f_c$ then a sharp bend — a 3 dB deviation is the standard "error" at the corner in the straight-line Bode approximation).
- **Straight line sloping downward at -20 dB/decade** for $f > f_c$, continuing indefinitely for an ideal RC filter.

```
 Gain (dB)
   0 dB ─────────────╮
                       ╲
                        ╲   slope = -20 dB/decade
                         ╲
                          ╲
                           ╲
 -3dB ····················· •  (at f = fc)
                              ╲
                               ╲
                                ╲___________
                    fc                     f (log scale)
```

### Bode Phase Plot (Description)

- **Flat at 0°** for $f \ll 0.1 f_c$
- **Smooth downward curve** transitioning through **-45° exactly at $f_c$**
- **Flattens toward -90°** for $f \gg 10 f_c$

```
 Phase
   0° ──────╮
             ╲
              ╲
   -45° ·······•  (at f = fc)
                ╲
                 ╲
                  ╲______
  -90°                   ╲__________
              0.1fc   fc    10fc     f (log scale)
```

---

## 9. Time Constant

### Definition

$$\tau = RC$$

The **time constant** τ (in seconds) characterizes how quickly the capacitor charges or discharges through the resistor. It is directly linked to cutoff frequency: $f_c = \frac{1}{2\pi\tau}$ — a smaller τ means faster response and a higher cutoff frequency, and vice versa.

### Charging

When a step input is applied, the capacitor voltage rises according to:

$$V_C(t) = V_{in}\left(1 - e^{-t/\tau}\right)$$

- At $t = \tau$: $V_C = V_{in}(1 - e^{-1}) = V_{in}(1 - 0.368) = 0.632\,V_{in}$

This is the origin of the famous **63.2% rule**: after one time constant, the capacitor has charged to 63.2% of its final value — regardless of the actual R, C, or voltage values.

| Time elapsed | % of final value reached |
|---|---|
| 1τ | 63.2% |
| 2τ | 86.5% |
| 3τ | 95.0% |
| 4τ | 98.2% |
| 5τ | 99.3% (considered "fully charged" in practice) |

### Discharging

When the input is removed (or shorted to 0V) and the capacitor discharges through R:

$$V_C(t) = V_0\, e^{-t/\tau}$$

- At $t = \tau$: $V_C = V_0 e^{-1} = 0.368\,V_0$

This gives the **36.8% remaining rule**: after one time constant of discharging, 36.8% of the original voltage still remains (equivalently, 63.2% has been lost).

### Practical Note

The time-domain (τ = RC) and frequency-domain ($f_c = \frac{1}{2\pi RC}$) descriptions are mathematically linked — they describe the *same* physical circuit from two different, complementary viewpoints: how fast it responds to a step (time domain) vs. how it treats sinusoids of different frequencies (frequency domain).


---

## 10. LTspice Implementation

### Step-by-Step: Building the Circuit

**Step 1 — Create a new schematic**
- Open LTspice → `File` → `New Schematic`. A blank grid canvas appears.

**Step 2 — Place the AC voltage source**
- Click the component button or press `F2`.
- Search for **"voltage"** in the component browser and select it.
- Click on the canvas to place it. The top terminal is positive by convention.

**Step 3 — Place the resistor**
- Press `R` (hotkey).
- Rotate horizontal if needed (`Ctrl+R` while placing) so current flows left → right from Vin to the output node.
- Click to place it in series after the voltage source's positive terminal.

**Step 4 — Place the capacitor**
- Press `C` (hotkey).
- Place it **vertically**, top terminal at the R–C junction (the output node), bottom terminal going to ground.

**Step 5 — Wire the circuit**
- Press `F3` to enter wiring mode.
- Connect (+) of V1 → left terminal of R.
- Connect right terminal of R → top terminal of C (this junction is Vout).
- Connect (−) of V1 → bottom terminal of C (shared bottom rail = ground).

**Step 6 — Add ground**
- Press `G` and place the ground symbol on the shared bottom rail. Every LTspice circuit must have a ground/node 0 or the simulation will fail.

**Step 7 — Set component values**
- Right-click R → enter e.g. `10k`.
- Right-click C → enter e.g. `100n`.
- ⚠️ Suffixes: `p`=pico, `n`=nano, `u`=micro, `m`=milli, `k`=kilo, `Meg`=mega (bare `M` means milli in SPICE, not mega).

**Step 8 — Configure the AC voltage source**
- Right-click V1 → `Advanced`.
- Under "Small signal AC analysis (.AC)", set **AC Amplitude = 1** (so output directly reads as linear gain).
- For transient analysis, under "Function", select `SINE` and set DC offset, amplitude, frequency.

**Step 9 — Label the output node (recommended)**
- Press `F4` (Label Net) and label the R–C junction as `Vout` for easy referencing in plots and `.meas` statements.

**Step 10 — Add the simulation directive**
- Click the SPICE directive icon (`S`, or `Edit → SPICE Directive`) and type the desired command (Section 11), e.g. `.ac dec 100 10 1Meg`.

**Step 11 — Run the simulation**
- Click Run (the running-man icon). Click on the Vout wire to plot the response.

---

## 11. LTspice Commands

### AC Sweep
```
.ac dec 100 10 1Meg
```
Performs a small-signal AC frequency sweep, producing the Bode magnitude/phase plots.

| Parameter | Meaning |
|-----------|---------|
| `.ac` | Directive for frequency-domain (AC) analysis |
| `dec` | Logarithmic, decade-spaced sweep — ideal for Bode plots spanning many decades |
| `100` | Points per decade — higher gives a smoother curve |
| `10` | Start frequency = 10 Hz |
| `1Meg` | Stop frequency = 1 MHz (must write `Meg`, not `M`) |

### Transient Analysis
```
.tran 0 50m
```
Runs a time-domain simulation showing Vout's actual charge/discharge response.

| Parameter | Meaning |
|-----------|---------|
| `.tran` | Directive for transient analysis |
| `0` | Start time for saving data |
| `50m` | Stop time = 50 ms (total simulated duration) |

### Operating Point
```
.op
```
Computes DC steady-state node voltages/currents (capacitor = open circuit at DC). For this filter, `.op` confirms $V_{out}=V_{in}$ at DC.

### Parameter Sweep (optional)
```
.step param R list 1k 10k 100k
```
Sweeps a component value across multiple runs in one simulation — e.g., replace R's value with `{R}`, add `.param R 10k`, then `.step param R list 1k 10k 100k`, combined with an `.ac` sweep to overlay Bode plots for each R and visually see $f_c$ shift.

---

## 12. Example Design

**Specs:** R = 10 kΩ, C = 100 nF

**Time Constant:**
$$\tau = RC = (10{,}000)(100\times10^{-9}) = 1\times10^{-3}\ \text{s} = 1\ \text{ms}$$

**Cutoff Frequency:**
$$f_c = \frac{1}{2\pi RC} = \frac{1}{2\pi(1\times10^{-3})} \approx 159.15\ \text{Hz}$$

**Gain at each frequency**, using $|H| = \dfrac{1}{\sqrt{1+(2\pi fRC)^2}}$, $RC=10^{-3}$s:

**10 Hz:** $2\pi fRC = 0.0628$; $|H| = 1/\sqrt{1.00395} \approx 0.998$; Gain ≈ **−0.02 dB**

**100 Hz:** $2\pi fRC = 0.6283$; $|H| = 1/\sqrt{1.3948} \approx 0.847$; Gain ≈ **−1.44 dB**

**159 Hz (≈ $f_c$):** $2\pi fRC \approx 1$; $|H| = 1/\sqrt2 \approx 0.707$; Gain ≈ **−3.01 dB**

**1 kHz:** $2\pi fRC = 6.283$; $|H| = 1/\sqrt{40.48} \approx 0.157$; Gain ≈ **−16.07 dB**

**10 kHz:** $2\pi fRC = 62.83$; $|H| = 1/\sqrt{3948.6} \approx 0.0159$; Gain ≈ **−35.97 dB**

| Frequency | $2\pi fRC$ | \|H(jω)\| | Gain (dB) | Region |
|---|---|---|---|---|
| 10 Hz | 0.063 | 0.998 | −0.02 dB | Passband |
| 100 Hz | 0.628 | 0.847 | −1.44 dB | Near passband |
| 159 Hz | ≈1.000 | 0.707 | **−3.01 dB** | **Cutoff** |
| 1 kHz | 6.283 | 0.157 | −16.07 dB | Stopband |
| 10 kHz | 62.83 | 0.0159 | −35.97 dB | Deep stopband |

Check: from 1 kHz→10 kHz, gain drops ≈19.9 dB, matching the −20 dB/decade rule.

---

## 13. LTspice Verification

**Cutoff frequency:** Run `.ac dec 100 10 1Meg` with V1 AC amplitude = 1V. Use the cursor on the Vout trace to find where the dB value crosses −3.01 dB; the frequency should match ≈159 Hz. Or add `.meas AC fc WHEN Vdb(Vout)=-3`.

**Gain:** Compare cursor readouts at 10 Hz, 100 Hz, 159 Hz, 1 kHz, 10 kHz against the hand-calculated table above.

**Phase:** LTspice's AC plot shows both magnitude and phase traces. Confirm phase ≈ −45° at 159 Hz, approaching 0° at low f and −90° at high f.

**Time-domain:** Switch to `.tran`, drive V1 with a `PULSE` source, plot Vout vs. time, and confirm it reaches 63.2% of its final value at t = τ = 1 ms.

---

## 14. Common Mistakes

| Mistake | Why It's a Problem | Fix |
|---|---|---|
| Incorrect output node | Probing across R instead of C gives a high-pass response, not low-pass | Vout must be measured across C, at the R–C junction |
| Missing ground | LTspice needs node 0; without it, simulation fails | Always place the ground symbol on the return rail |
| Wrong capacitor units (nF vs µF) | `100n` vs `100u` differs by 1000×, shifting $f_c$ drastically | Double-check SI suffix; recompute $f_c$ as a sanity check |
| Incorrect AC source amplitude | Non-unity AC amplitude makes reading gain directly off the plot error-prone | Set AC Amplitude = 1V for `.ac` sweeps |
| Wrong frequency sweep settings | Too-narrow a range misses passband or stopband regions | Sweep from ≤ $f_c$/100 to ≥ $f_c$×100 |
| Typing `1M` instead of `1Meg` | SPICE reads `M` as milli, not mega | Always write `Meg` explicitly |
| No AC amplitude set for `.ac` | Zero AC amplitude gives a flat zero output everywhere | Explicitly set the AC Amplitude field, separate from transient/DC settings |

---

## 15. Viva / Interview Questions

**1. What is an RC low-pass filter?** A first-order passive circuit (one R, one C) where low frequencies pass through nearly unattenuated and high frequencies are attenuated, with output taken across the capacitor.

**2. Why "first-order"?** Because it has one energy-storage element (C), giving a transfer function with one pole and a constant −20 dB/decade roll-off.

**3. Derive $f_c$.** Set $|H(j\omega)|=1/\sqrt2$ in $1/\sqrt{1+(\omega RC)^2}$, solve to get $\omega_c RC=1$, so $f_c=1/(2\pi RC)$.

**4. Why −3 dB for cutoff?** It's the half-power point: power ∝ V², and $(1/\sqrt2)^2=1/2$ — a universal, physically meaningful threshold.

**5. What is capacitive reactance vs resistance?** $X_C=1/(2\pi fC)$ is frequency-dependent opposition that stores/releases energy (no heat dissipation) and shifts voltage-current phase by 90°, unlike resistance.

**6. Why does the filter attenuate high frequencies?** $X_C$ shrinks with frequency, so C increasingly shorts to ground, dropping more voltage across R and less across C (Vout).

**7. What is the time constant physically?** $\tau=RC$ (seconds) — the time for the capacitor to reach 63.2% of a step change.

**8. Relation between τ and $f_c$?** Inverse: $f_c = 1/(2\pi\tau)$.

**9. Significance of 63.2%/36.8%?** From evaluating $1-e^{-1}$ and $e^{-1}$ — universal fractions after one time constant, independent of actual R, C, V values.

**10. What is a Bode plot?** Log-frequency-axis magnitude (dB) and phase (degrees) plots showing frequency response.

**11. Why −20 dB/decade roll-off?** In the stopband $|H|\approx f_c/f$; taking $20\log_{10}$ shows a 20 dB drop every 10× frequency increase.

**12. Phase at $f_c$?** −45°, since $\omega RC=1$ gives $\phi=-\tan^{-1}(1)=-45°$.

**13. What does a pole represent?** The value of $s$ where $H(s)$'s denominator is zero ($s=-1/RC$); it's the natural response rate, and a left-half-plane pole means stability.

**14. Double R, fixed C — effect on $f_c$?** $f_c$ halves, since $f_c\propto 1/(RC)$.

**15. Double C, fixed R — effect?** Same: $f_c$ halves.

**16. Why output across C, not R?** C's impedance falls with frequency, giving the low-pass characteristic; output across R instead gives a high-pass filter.

**17. `.ac` vs `.tran`?** `.ac` gives frequency-domain gain/phase (Bode); `.tran` gives the actual time-domain waveform.

**18. Why AC amplitude = 1V in LTspice?** So Vout directly equals $|H(j\omega)|$, the linear gain, without extra scaling.

**19. Response at DC (f=0)?** C is an open circuit, no drop across R, so $V_{out}=V_{in}$ (unity gain, 0° phase).

**20. Ideal vs real RC filter?** Real capacitors have ESR/leakage/tolerance; real resistors have parasitics at high f; and load impedance can alter the effective cutoff if not much larger than $X_C$.

**21. Why used for anti-aliasing?** It removes content above the Nyquist frequency before sampling, preventing aliasing.

**22. Pole location vs time response?** Pole at $s=-1/RC$ corresponds to decay $e^{-t/RC}$; more negative pole = faster decay.

**23. How to verify $f_c$ in LTspice without hand calculation?** Run `.ac dec` sweep, use cursor or `.meas AC fc WHEN Vdb(Vout)=-3` to read where gain crosses −3 dB.

**24. Effect of source/load impedance on actual $f_c$?** Non-ideal source impedance adds to R; load in parallel with C changes effective RC — both shift $f_c$ unless source impedance is negligible and load impedance is very high.

---

## 16. Summary — Key Formulas

| Quantity | Formula | Units | Description |
|----------|---------|-------|-------------|
| Capacitive Reactance | $X_C = \dfrac{1}{2\pi f C}$ | Ω | Frequency-dependent opposition of C to AC current |
| Impedance of C (Laplace) | $Z_C(s) = \dfrac{1}{sC}$ | Ω | General complex-frequency impedance |
| Time Constant | $\tau = RC$ | s | Time to reach 63.2% charge / 36.8% remaining on discharge |
| Cutoff Frequency | $f_c = \dfrac{1}{2\pi RC}$ | Hz | Frequency where output = $1/\sqrt2$ (−3 dB) of input |
| Transfer Function | $H(s) = \dfrac{1}{1+sRC}$ | — | Laplace-domain input–output relation |
| Output Voltage (phasor) | $V_{out} = V_{in}\times\dfrac{1}{1+j\omega RC}$ | V | Frequency-domain output for sinusoidal input |
| Linear Gain | $|H(j\omega)| = \dfrac{1}{\sqrt{1+(2\pi fRC)^2}}$ | ratio | Fraction of input amplitude at output |
| Decibel Gain | $Gain_{dB} = 20\log_{10}|H(j\omega)|$ | dB | Logarithmic gain |
| Phase Shift | $\phi = -\tan^{-1}(2\pi fRC)$ | ° | Output lag relative to input |
| Pole Location | $s = -\dfrac{1}{RC}$ | rad/s | Root of denominator; sets natural response rate |
| Roll-off Slope | −20 dB/decade (beyond $f_c$) | dB/decade | Attenuation rate, characteristic of a first-order filter |

### Final Takeaway

The RC low-pass filter is deceptively simple — just two components — yet it embodies nearly every core idea in linear systems theory: complex impedance, voltage dividers, Laplace transforms, poles, Bode plots, and time constants. Mastering it thoroughly, both by hand and in LTspice, builds the foundation for every more advanced filter (RC high-pass, RLC, active/Butterworth/Chebyshev filters) in the ECE curriculum.