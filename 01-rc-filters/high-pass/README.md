# RC High-Pass Filter — Complete Study Notes

---

## 1. Introduction & Working Principle

An **RC High-Pass Filter (HPF)** is a first-order linear circuit built from a resistor (R) and a capacitor (C) that **allows high-frequency signals to pass through while attenuating low-frequency signals**. It is the electrical dual of the RC Low-Pass Filter, achieved simply by swapping the positions of R and C.

**Core idea:** A capacitor's impedance is inversely proportional to frequency:

$$Z_C = \frac{1}{j\omega C}$$

- At **low frequencies** (ω → 0), $Z_C \to \infty$ — the capacitor behaves like an open circuit, blocking the signal from reaching the output.
- At **high frequencies** (ω → ∞), $Z_C \to 0$ — the capacitor behaves like a short circuit, allowing the signal to pass to the output almost unattenuated.

Since the capacitor is placed in **series** with the signal path and the resistor forms the output leg (to ground), this frequency-dependent blocking action gives rise to high-pass behavior.

---

## 2. Circuit Diagram

```
        C
 Vin o──||──┬────o Vout
            │
            R
            │
 GND o──────┴────o GND
```

**Description:**
- Input signal $V_{in}$ is applied across the series combination of C and R.
- Capacitor **C** is in series with the signal path (input side).
- Resistor **R** is connected from the output node to ground.
- Output $V_{out}$ is taken **across R**.

This is a **voltage divider** between $Z_C$ (capacitor impedance) and $R$.

---

## 3. Roles of R and C

| Component | Role |
|---|---|
| **Capacitor (C)** | Series element. Blocks DC and low frequencies (high impedance at low ω), passes high frequencies (low impedance at high ω). It is the frequency-selective gatekeeper. |
| **Resistor (R)** | Shunt/output element. Converts the current passed by C into an output voltage. Along with C, it sets the time constant $\tau = RC$ and hence the cutoff frequency. |

Together, R and C form a **voltage divider** whose division ratio depends on frequency — this frequency dependence is the entire mechanism of filtering.

---

## 4. Step-by-Step Derivation

### 4.1 Capacitor Impedance

In the phasor (frequency) domain, the impedance of a capacitor is:

$$Z_C = \frac{1}{j\omega C}, \qquad \omega = 2\pi f$$

This is purely imaginary (reactive) — no real power is dissipated in an ideal capacitor.

### 4.2 Voltage Divider Setup

Treating the circuit as a phasor voltage divider (C in series, R to ground):

$$V_{out} = V_{in} \cdot \frac{R}{R + Z_C} = V_{in} \cdot \frac{R}{R + \dfrac{1}{j\omega C}}$$

### 4.3 Transfer Function H(jω)

$$H(j\omega) = \frac{V_{out}}{V_{in}} = \frac{R}{R + \dfrac{1}{j\omega C}}$$

Multiply numerator and denominator by $j\omega C$:

$$H(j\omega) = \frac{j\omega RC}{1 + j\omega RC}$$

**Define the time constant:**

$$\tau = RC$$

So:

$$\boxed{H(j\omega) = \frac{j\omega \tau}{1 + j\omega \tau}}$$

### 4.4 Cutoff (Corner) Frequency

The cutoff frequency $\omega_c$ is defined as the point where $|H(j\omega)| = \frac{1}{\sqrt{2}}$ (the −3 dB point), which occurs when the real and imaginary parts of the denominator are equal, i.e., when $\omega R C = 1$:

$$\omega_c = \frac{1}{RC} \quad\Rightarrow\quad \boxed{f_c = \frac{1}{2\pi RC}}$$

Substituting $\omega = \omega/\omega_c$ lets us rewrite the transfer function in normalized form:

$$H(j\omega) = \frac{j(\omega/\omega_c)}{1 + j(\omega/\omega_c)}$$

### 4.5 Magnitude Response

$$|H(j\omega)| = \frac{\omega RC}{\sqrt{1 + (\omega RC)^2}} = \frac{\omega/\omega_c}{\sqrt{1+(\omega/\omega_c)^2}}$$

**Limiting behavior:**

| Frequency Region | Approximation | Behavior |
|---|---|---|
| $\omega \ll \omega_c$ | $|H| \approx \omega RC$ | Magnitude rises linearly with ω → **+20 dB/decade slope** |
| $\omega = \omega_c$ | $|H| = 1/\sqrt{2} = 0.707$ | **−3 dB point** |
| $\omega \gg \omega_c$ | $|H| \approx 1$ | Passband, unity gain (0 dB) |

In decibels:

$$|H(j\omega)|_{dB} = 20\log_{10}\left(\frac{\omega/\omega_c}{\sqrt{1+(\omega/\omega_c)^2}}\right)$$

### 4.6 Phase Response

$$\phi(\omega) = 90^\circ - \tan^{-1}(\omega RC) = \tan^{-1}\left(\frac{1}{\omega RC}\right)$$

| Frequency | Phase |
|---|---|
| $\omega \to 0$ | $\phi \to +90^\circ$ (output leads input) |
| $\omega = \omega_c$ | $\phi = +45^\circ$ |
| $\omega \to \infty$ | $\phi \to 0^\circ$ |

The HPF introduces a **phase lead**, decreasing from 90° to 0° as frequency increases.

### 4.7 Time Constant and Transient (Step) Response

For a step input of amplitude $V_0$ applied at $t=0$ to an initially uncharged capacitor, solving the KVL differential equation:

$$V_0 = i(t) R + \frac{1}{C}\int i(t)\,dt$$

gives the output (across R):

$$v_{out}(t) = V_0 \, e^{-t/\tau}, \qquad \tau = RC$$

- At $t = 0^+$: output instantly jumps to $V_0$ (capacitor acts as short for a sudden change).
- As $t \to \infty$: output decays to 0 (capacitor charges fully, blocking DC).
- At $t = \tau$: output falls to $36.8\%$ of $V_0$ (i.e., $V_0/e$).
- At $t = 5\tau$: output is essentially 0 (< 1%) — this is the settling time used in practice.

This decaying-exponential response is why the RC HPF is also called a **differentiator circuit** for slow-varying inputs relative to τ, and is used for **AC coupling**.

---

## 5. Frequency Response Summary Table

| f/fc | ω/ωc | \|H\| | \|H\| (dB) | Phase |
|---|---|---|---|---|
| 0.01 | 0.01 | 0.01 | −40.0 | 89.4° |
| 0.1 | 0.1 | 0.0995 | −20.0 | 84.3° |
| 0.5 | 0.5 | 0.447 | −7.0 | 63.4° |
| 1 | 1 | 0.707 | −3.0 | 45.0° |
| 2 | 2 | 0.894 | −1.0 | 26.6° |
| 10 | 10 | 0.995 | −0.04 | 5.7° |
| 100 | 100 | 0.99995 | ≈0 | 0.57° |

---

## 6. Bode Plot

**Magnitude Plot (asymptotic approximation):**

```
 dB
  0 dB ─────────────────────────────●━━━━━━━━━━━━━  (flat, passband)
                                  ╱
                                ╱   +20 dB/decade
                              ╱
-20 dB ────────────────────╱
                          ╱
-40 dB ─────────────╱
        │           │      │
     0.01fc       0.1fc    fc          10fc     100fc
                          (breakpoint, actual curve is
                           3 dB below asymptote here)
```

- Below $f_c$: straight line rising at **+20 dB/decade**.
- Above $f_c$: flat line at **0 dB**.
- The two asymptotes meet at $f = f_c$; the actual curve passes **3 dB below** this intersection.

**Phase Plot (asymptotic approximation):**

```
 Phase
  90° ━━━━━━━━━╲
                 ╲
                   ╲  (slope: −45°/decade from 0.1fc to 10fc)
  45° ─ ─ ─ ─ ─ ─ ─ ●─ ─ ─ ─ ─
                       ╲
                         ╲
   0° ─────────────────────╲━━━━━━━━━━━━━━━━━
        │           │      │           │
     0.01fc       0.1fc    fc        10fc
```

- Phase starts near +90° (leading), transitions through +45° at $f_c$, and settles to 0° well above $f_c$.
- Common straight-line approximation: phase is flat at 90° below $0.1f_c$, decreases linearly to 0° between $0.1f_c$ and $10f_c$, flat at 0° above $10f_c$.

---

## 7. Solved Numerical Example

**Given:** $R = 1.6\ \text{k}\Omega$, $C = 0.01\ \mu F = 10^{-8}\ F$

**Find:** (a) cutoff frequency $f_c$, (b) $|H|$ and phase at $f = 5\ \text{kHz}$, (c) time constant τ, (d) output for a 5 V step input at $t = \tau$.

**(a) Cutoff frequency:**

$$f_c = \frac{1}{2\pi RC} = \frac{1}{2\pi (1600)(10^{-8})} = \frac{1}{2\pi \times 1.6\times10^{-5}}$$

$$f_c = \frac{1}{1.005\times10^{-4}} \approx 9950\ \text{Hz} \approx 9.95\ \text{kHz}$$

**(b) At f = 5 kHz:**

Compute ratio: $\dfrac{f}{f_c} = \dfrac{5000}{9950} = 0.5025$

Magnitude:
$$|H| = \frac{f/f_c}{\sqrt{1+(f/f_c)^2}} = \frac{0.5025}{\sqrt{1+0.2525}} = \frac{0.5025}{1.1191} = 0.449$$

In dB: $20\log_{10}(0.449) = -6.96\ \text{dB} \approx -7\ \text{dB}$

Phase:
$$\phi = \tan^{-1}\left(\frac{1}{2\pi f RC}\right) = \tan^{-1}\left(\frac{1}{0.5025}\right) = \tan^{-1}(1.990) \approx 63.3^\circ$$

**(c) Time constant:**

$$\tau = RC = 1600 \times 10^{-8} = 1.6\times10^{-5}\ \text{s} = 16\ \mu s$$

**(d) Step response at t = τ (input step = 5 V):**

$$v_{out}(\tau) = 5\, e^{-1} = 5 \times 0.3679 = 1.839\ \text{V}$$

So the output has decayed to about **1.84 V** (36.8% of 5 V) after one time constant.

---

## 8. Practical Applications

1. **AC coupling / DC blocking** — passes AC signal components while blocking DC bias between amplifier stages (e.g., between audio preamp stages).
2. **Differentiator circuits** — approximates $d/dt$ operation for input signals varying slowly compared to τ (τ ≪ signal period).
3. **Treble boost / bass-cut filters** in audio tone-control circuits and speaker crossover networks (tweeter side).
4. **Noise and hum rejection** — removing low-frequency drift, 50/60 Hz hum, or baseline wander in instrumentation and biomedical signal chains (e.g., ECG preprocessing).
5. **Edge detection** — sharp transitions in pulse/digital circuits pass through readily, useful in trigger and spike-detection circuits.
6. **Radio & communication front-ends** — rejecting unwanted low-frequency interference before further RF processing.

---

## 9. Design Considerations

- **Component selection:** Choose R in the kΩ range (to keep loading effects and current manageable) and pick C to realize the desired $f_c = 1/(2\pi RC)$.
- **Source and load impedance:** The driving source should have low output impedance (≪ R) and the load should have high input impedance (≫ R) to avoid altering the intended divider ratio and $f_c$.
- **Capacitor non-idealities:** Real capacitors have ESR (equivalent series resistance), leakage, and tolerance (±5–20%) — these shift the actual $f_c$ from the calculated value. Use low-tolerance film or ceramic capacitors for precision work.
- **Cascading stages:** Cascading multiple RC HPF stages increases roll-off steepness (−20 dB/decade per stage) but each stage loads the previous one — use buffer (op-amp) stages between them for a clean multi-pole "active" high-pass filter (Sallen-Key, etc.) if steep roll-off is needed without impedance interaction.
- **Bandwidth vs. settling time trade-off:** A higher $f_c$ (smaller τ) settles faster but blocks more of the low-frequency content — choose $f_c$ well below the lowest frequency of interest in the passband (commonly a decade below).

---

## 10. Limitations

- **Gentle roll-off:** Only −20 dB/decade (first order) — inadequate for applications needing sharp frequency-domain separation.
- **Non-zero phase shift in passband:** Signals near $f_c$ experience significant phase distortion, which can degrade signals with multiple frequency components (e.g., distort pulse edges/square waves).
- **Loading effects:** Passive RC filters interact with source/load impedance, shifting the effective cutoff frequency unless buffered.
- **No gain:** Being passive, it can only attenuate, never amplify — insertion loss must be compensated elsewhere if needed.
- **Component drift:** Cutoff frequency depends directly on RC product, which drifts with temperature and component aging/tolerance.

---

## 11. LTspice Simulation Guide

### 11.1 Component Values (from the solved example)

- $R = 1.6\ \text{k}\Omega$
- $C = 0.01\ \mu F$
- Expected $f_c \approx 9.95\ \text{kHz}$

### 11.2 Building the Circuit

1. Open LTspice → **New Schematic**.
2. Place a **voltage source** (V1) from GND to node `in`.
3. Place **capacitor C1** from node `in` to node `out` (series element).
4. Place **resistor R1** from node `out` to **GND**.
5. Ground both the source's negative terminal and R1's bottom terminal (common ground reference).
6. Label the output node `out` (right-click wire → Label Net) for easy probing.

**Schematic node layout:**
```
V1 (in) ──C1── (out) ──R1── GND
  │                          │
 GND ───────────────────────┘
```

### 11.3 LTspice Netlist

```spice
* RC High-Pass Filter
V1 in 0 AC 1 SINE(0 5 5k)
C1 in out 0.01u
R1 out 0 1.6k
.ac dec 100 1 1Meg
.tran 0 200u 0 0.01u
.op
.backanno
.end
```

**Explanation of directives:**
- `V1 in 0 AC 1 SINE(0 5 5k)` — source has AC magnitude 1 (for .ac sweep) and, for transient analysis, is a 5 kHz sine wave with 5 V amplitude and 0 V offset.
- `C1 in out 0.01u` — capacitor between input and output node.
- `R1 out 0 1.6k` — resistor from output node to ground.

### 11.4 AC Analysis (Frequency Response / Bode Plot)

Directive:
```spice
.ac dec 100 1 1Meg
```
- Sweeps frequency **logarithmically** ("dec"), 100 points per decade, from 1 Hz to 1 MHz.

**Steps:**
1. Add the `.ac` directive (Simulate → Edit Simulation Cmd → AC Analysis tab; Type = Decade, 100 pts/decade, Start = 1, Stop = 1Meg).
2. Run simulation (F2 for parts if needed, then Run).
3. Click on the `out` node in the schematic — LTspice plots the **Bode plot** automatically: magnitude (dB, left axis) and phase (degrees, right axis) vs. frequency (log scale).
4. **Verify cutoff frequency:** Use the cursor (click and drag on the trace) to find the frequency where the magnitude trace crosses **−3 dB**. It should read close to **9.95 kHz**, matching the hand calculation.

### 11.5 Transient Analysis (Time-Domain / Step-Response Verification)

Directive:
```spice
.tran 0 200u 0 0.01u
```
- Simulates from 0 to 200 µs with a maximum internal timestep of 0.01 µs — enough to capture several time constants (τ = 16 µs) and multiple cycles of a 5 kHz sine.

**Steps:**
1. To see the **exponential decay / differentiator response**, temporarily change V1 to a **PULSE** source instead of SINE:
   ```spice
   V1 in 0 PULSE(0 5 0 1n 1n 1m 2m)
   ```
   This applies a 5 V step at t = 0.
2. Run `.tran 0 200u 0 0.01u` and probe `V(out)`.
3. You should see $V_{out}$ jump to 5 V at t = 0, then decay exponentially toward 0 with **τ = 16 µs** — confirming the earlier hand-calculated step response ($V_{out}(\tau) \approx 1.84$ V; check the cursor at t = 16 µs after the step).
4. For the **sine-wave case** (original netlist), run `.tran` and observe that at 5 kHz (below $f_c$), the output amplitude is attenuated and phase-shifted relative to input — consistent with the $|H| = 0.449$, $\phi = 63.3°$ computed in Section 7(b). Overlay `V(in)` and `V(out)` traces to visually confirm both the amplitude drop and phase lead.

### 11.6 Operating Point Check

`.op` reports the DC operating point — since the capacitor blocks DC in steady state, $V(out) = 0$ V at DC, confirming the high-pass (DC-blocking) behavior.

### 11.7 Quick Verification Checklist

| Check | Expected Result |
|---|---|
| −3 dB frequency on AC Bode plot | ≈ 9.95 kHz |
| Phase at $f_c$ | ≈ 45° |
| DC operating point, V(out) | 0 V |
| Step response time constant | ≈ 16 µs (63.2% rise from 5V baseline is decay to 36.8%) |
| High-frequency gain (e.g., at 1 MHz) | ≈ 0 dB (≈1, unity) |
| Low-frequency gain (e.g., at 10 Hz) | Large negative dB (strongly attenuated) |

---

## 12. Exam / Viva Q&A

**Q1. What is the basic difference between an RC low-pass and RC high-pass filter?**
A: In an LPF, the output is taken across the capacitor (R in series, C to ground); in an HPF, the output is taken across the resistor (C in series, R to ground). This swap inverts which frequencies are passed.

**Q2. Derive the cutoff frequency condition.**
A: Cutoff occurs when $|H(j\omega)| = 1/\sqrt{2}$, which happens when $\omega RC = 1$ (real part of denominator equals imaginary part), giving $f_c = \dfrac{1}{2\pi RC}$.

**Q3. Why is the RC HPF called a differentiator?**
A: When the time constant τ is much smaller than the period of variation of the input signal, the capacitor voltage stays small and the output across R approximates $RC\,\dfrac{dv_{in}}{dt}$, i.e., a scaled derivative of the input.

**Q4. What happens to a DC signal applied to an RC HPF?**
A: In steady state, the capacitor fully charges and blocks all current, so $V_{out} = 0$ for DC — hence "DC blocking" behavior.

**Q5. What is the phase shift at the cutoff frequency, and is it leading or lagging?**
A: +45°, and it is a **leading** phase shift (output leads input), since $\phi = \tan^{-1}(1/\omega RC)$ is always positive.

**Q6. What is the roll-off rate of a first-order RC HPF, and how would you increase it?**
A: −20 dB/decade (equivalently −6 dB/octave) below $f_c$. To increase roll-off steepness, cascade multiple RC stages (with buffering between stages to avoid loading) — each additional stage adds another −20 dB/decade.

**Q7. How do you determine τ from a step response experimentally?**
A: Apply a voltage step and measure the time for the output to decay to 36.8% ($1/e$) of its initial value; that elapsed time is τ = RC. Alternatively, measure the time to decay to $1/e$ from any point, since the decay is a pure exponential.

**Q8. Why must source resistance be low and load resistance be high for the filter to behave as designed?**
A: The transfer function derivation assumes an ideal (zero-impedance) source and an unloaded (infinite-impedance) output. Non-negligible source resistance adds in series with C (shifting $f_c$), while a low load resistance appears in parallel with R (also altering the effective time constant and gain).

**Q9. Sketch the Bode magnitude plot's asymptotic behavior.**
A: Below $f_c$: line rising at +20 dB/decade through the point (fc, 0 dB) when extrapolated. Above $f_c$: flat at 0 dB. Actual curve is 3 dB below the asymptote intersection at $f = f_c$.

**Q10. In LTspice, how do you experimentally verify $f_c$?**
A: Run an `.ac dec` sweep, plot $V(out)/V(in)$ in dB, and use the cursor to find the frequency at which the magnitude is −3 dB relative to the passband (high-frequency) level; this should match $1/(2\pi RC)$.

**Q11. What is the significance of $5\tau$ in transient analysis?**
A: After $5\tau$, the exponential transient has decayed to less than 1% of its initial value — considered the practical "settling time" for the circuit to reach steady state.

**Q12. Give two real-world applications of the RC HPF.**
A: (i) AC coupling between amplifier stages to block DC bias while passing audio signals; (ii) removing baseline wander/low-frequency drift in biomedical signal acquisition (e.g., ECG front-end).

---

*End of notes.*