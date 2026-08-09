# Series RLC Resonance — Complete Reference Guide
### Theory → Derivations → LTspice Simulation → Viva Prep

---

## 1. Basic Concept

### 1.1 What is a Series RLC Circuit?

A **series RLC circuit** consists of a **Resistor (R)**, **Inductor (L)**, and **Capacitor (C)** connected in series with each other, driven by an AC voltage source. Because they are in series, the **same current $I$** flows through all three elements at every instant — only the voltage across each element differs in magnitude and phase.

```
        R           L           C
  o---/\/\/\----000000000----| |----o
  |                                  |
  +----------- V(t) source ---------+
                (AC, 1V)
```

### 1.2 Role of R, L, and C

| Element | Opposition Type | Symbol | Phase of Voltage vs Current | Energy Behavior |
|---|---|---|---|---|
| **R** (Resistor) | Resistance | $R$ | In phase (0°) | Dissipates energy as heat |
| **L** (Inductor) | Inductive Reactance | $X_L$ | Voltage **leads** current by 90° | Stores energy in magnetic field |
| **C** (Capacitor) | Capacitive Reactance | $X_C$ | Voltage **lags** current by 90° | Stores energy in electric field |

- $R$ is frequency-independent — it always opposes current the same way regardless of frequency.
- $X_L = 2\pi f L$ **increases** with frequency — the inductor "chokes" high frequencies more.
- $X_C = \dfrac{1}{2\pi f C}$ **decreases** with frequency — the capacitor blocks DC/low frequencies more.

### 1.3 How and Why Resonance Occurs

Since $X_L$ rises with frequency and $X_C$ falls with frequency, there exists exactly **one frequency** where they become equal in magnitude:

$$X_L = X_C$$

At this frequency, called the **resonant frequency $f_0$**, the inductive and capacitive reactances are equal but **opposite in phase** (one is +90°, the other is −90°), so they **cancel each other out completely** in the total impedance. What remains is purely resistive impedance:

$$Z = R + j(X_L - X_C) = R + j(0) = R$$

**Physical explanation:** At resonance, energy oscillates back and forth between the inductor's magnetic field and the capacitor's electric field at exactly the rate needed to sustain a "tank" oscillation, and the source only needs to supply the energy dissipated by R. This is why:
- Impedance is at its **minimum** (= R)
- Current is at its **maximum**
- The circuit behaves as if L and C aren't there at all (electrically), even though large voltages appear across them individually.

### 1.4 Circuit Behavior Below, At, and Above Resonance

| Region | Condition | Dominant Reactance | Impedance Behavior | Phase Angle $\phi$ | Circuit Nature |
|---|---|---|---|---|---|
| **Below resonance** ($f < f_0$) | $X_C > X_L$ | Capacitive | $\|Z\| > R$, rises as $f \to 0$ | Negative (current **leads** voltage) | Capacitive |
| **At resonance** ($f = f_0$) | $X_C = X_L$ | Neither (cancel) | $\|Z\| = R$ (minimum) | $0°$ (current **in phase** with voltage) | Purely resistive |
| **Above resonance** ($f > f_0$) | $X_L > X_C$ | Inductive | $\|Z\| > R$, rises as $f \to \infty$ | Positive (current **lags** voltage) | Inductive |

This gives the circuit its classic **band-pass** current response: current is small far from $f_0$ in either direction, and peaks sharply at $f_0$.

---

## 2. Key Formulas and Derivations

### 2.1 Inductive Reactance

$$X_L = 2\pi f L = \omega L$$

- $X_L$ = inductive reactance (Ω)
- $f$ = frequency (Hz)
- $\omega = 2\pi f$ = angular frequency (rad/s)
- $L$ = inductance (Henry, H)

**Derivation:** For an inductor, $v_L(t) = L\dfrac{di}{dt}$. If $i(t) = I_m \sin(\omega t)$, then:
$$v_L(t) = L \cdot \omega I_m \cos(\omega t) = \omega L \cdot I_m \sin(\omega t + 90°)$$
The voltage amplitude is $\omega L \cdot I_m$, so the opposition (ratio of voltage to current amplitude) is $X_L = \omega L$, and voltage leads current by 90°.

### 2.2 Capacitive Reactance

$$X_C = \frac{1}{2\pi f C} = \frac{1}{\omega C}$$

- $X_C$ = capacitive reactance (Ω)
- $C$ = capacitance (Farad, F)

**Derivation:** For a capacitor, $i_C(t) = C\dfrac{dv}{dt}$. If $v(t) = V_m \sin(\omega t)$, then:
$$i_C(t) = \omega C V_m \cos(\omega t)$$
Rearranging in terms of voltage amplitude per current amplitude gives $X_C = \dfrac{1}{\omega C}$, with voltage **lagging** current by 90° (equivalently, current leads voltage by 90°).

### 2.3 Total Complex Impedance

$$Z = R + j(X_L - X_C)$$

This follows directly from summing the three series impedances in phasor (complex) form:
$$Z_R = R \angle 0°, \quad Z_L = jX_L = X_L\angle 90°, \quad Z_C = -jX_C = X_C \angle{-90°}$$
$$Z = Z_R + Z_L + Z_C = R + jX_L - jX_C = R + j(X_L - X_C)$$

### 2.4 Magnitude of Impedance

$$|Z| = \sqrt{R^2 + (X_L - X_C)^2}$$

Directly from the Pythagorean magnitude of the complex number $R + j(X_L-X_C)$, since $R$ is the real (in-phase) part and $(X_L - X_C)$ is the imaginary (quadrature) part.

### 2.5 Current

$$I = \frac{V}{|Z|}$$

From Ohm's Law in phasor form, where $V$ is the RMS or peak amplitude of the source (consistent with how $I$ is expressed).

### 2.6 Resonant Frequency

**Derivation:** Resonance occurs when $X_L = X_C$:
$$2\pi f_0 L = \frac{1}{2\pi f_0 C}$$
$$ (2\pi f_0)^2 = \frac{1}{LC} $$
$$2\pi f_0 = \frac{1}{\sqrt{LC}}$$

$$\boxed{f_0 = \frac{1}{2\pi\sqrt{LC}}} \qquad \text{and equivalently} \qquad \omega_0 = \frac{1}{\sqrt{LC}}$$

- $f_0$ = resonant frequency (Hz)
- $L$ = inductance (H)
- $C$ = capacitance (F)

### 2.7 Phase Angle

$$\phi = \tan^{-1}\left(\frac{X_L - X_C}{R}\right)$$

This is the angle of the complex impedance $Z = R + j(X_L-X_C)$, and it equals the phase by which the source voltage leads the current (positive = inductive/lagging current, negative = capacitive/leading current, zero at resonance).

### 2.8 Quality Factor

$$Q = \frac{\omega_0 L}{R} = \frac{X_{L0}}{R} = \frac{1}{R}\sqrt{\frac{L}{C}} = \frac{1}{\omega_0 R C}$$

- $Q$ = quality factor (dimensionless)
- Physically, $Q$ represents the **voltage magnification** at resonance: $V_L = V_C = Q \times V_{source}$
- $Q$ also equals $2\pi \times \dfrac{\text{energy stored}}{\text{energy dissipated per cycle}}$ — a measure of how "underdamped"/sharp the resonance is.
- **Higher Q → sharper, narrower resonance peak; Lower Q → broader, flatter peak.**

### 2.9 Bandwidth

$$BW = \frac{R}{2\pi L} = \frac{f_0}{Q} \quad \text{(Hz)}$$

**Derivation:** Since $Q = \omega_0 L/R$, we have $f_0/Q = f_0 R/(\omega_0 L) = f_0 R /(2\pi f_0 L) = R/(2\pi L)$. Bandwidth is the frequency span between the two half-power (−3 dB) points, $f_2 - f_1$.

### 2.10 Half-Power Frequencies ($f_1, f_2$)

These occur where the **power delivered is half the maximum power** (equivalently, current drops to $I_{max}/\sqrt{2} = 0.707\, I_{max}$, i.e. $|Z| = \sqrt{2}\,R$).

Setting $|Z|^2 = 2R^2 \Rightarrow (X_L - X_C)^2 = R^2 \Rightarrow X_L - X_C = \pm R$.

Solving $2\pi f L - \dfrac{1}{2\pi f C} = \pm R$ (a quadratic in $f$) gives the **exact** expressions:

$$f_1 = -\frac{R}{4\pi L} + \sqrt{\left(\frac{R}{4\pi L}\right)^2 + \frac{1}{4\pi^2 LC}}$$

$$f_2 = +\frac{R}{4\pi L} + \sqrt{\left(\frac{R}{4\pi L}\right)^2 + \frac{1}{4\pi^2 LC}}$$

**Useful identities** (exact, not approximations):
$$f_2 - f_1 = BW = \frac{R}{2\pi L} \qquad \qquad f_0 = \sqrt{f_1 f_2}$$

For high-Q circuits ($Q \gtrsim 10$), the resonance curve is nearly symmetric on a linear frequency scale and $f_1 \approx f_0 - BW/2$, $f_2 \approx f_0 + BW/2$ is a good approximation. For lower Q (like our example, $Q \approx 3.16$), use the exact formulas above — the curve is noticeably asymmetric on a linear scale (but symmetric on a **log** scale, and symmetric in terms of $f_1 f_2 = f_0^2$).

---

## 3. Resonance Characteristics (At $f = f_0$)

| Quantity | Behavior at Resonance | Explanation |
|---|---|---|
| **Impedance $\|Z\|$** | Minimum, $\|Z\| = R$ | Reactances cancel; only resistance remains |
| **Current $I$** | Maximum, $I_{max} = V/R$ | Minimum impedance → maximum current (Ohm's law) |
| **Phase angle $\phi$** | $0°$ | Circuit is purely resistive; $X_L = X_C$ |
| **Power factor** | $\cos\phi = 1$ (unity) | Voltage and current are perfectly in phase |
| **Voltage across R ($V_R$)** | $V_R = I_{max}R = V_{source}$ | All source voltage appears across R (since Z=R) |
| **Voltage across L ($V_L$)** | $V_L = I_{max}X_L = Q \cdot V_{source}$ | Can be **much larger** than source voltage if Q > 1 |
| **Voltage across C ($V_C$)** | $V_C = I_{max}X_C = Q \cdot V_{source}$ | Equal in magnitude to $V_L$, but 180° out of phase with it |
| **$V_L$ vs $V_C$ relationship** | $V_L = V_C$, but phase-opposed | They cancel in the loop, satisfying KVL: $V_R + V_L + V_C = V_{source}$ (phasor sum) |

**Key insight:** Even though $V_L$ and $V_C$ can individually be several times larger than the source voltage (a phenomenon called **voltage resonance** or **series resonance voltage magnification**), they cancel each other in the loop because they are exactly out of phase — this is *not* a violation of KVL, just a demonstration of phasor (vector) addition rather than simple arithmetic addition.

---

## 4. LTspice Simulation

### Component Values for This Guide
- $R = 100\,\Omega$
- $L = 10\,\text{mH} = 10\text{m}$
- $C = 100\,\text{nF} = 100\text{n}$
- AC source amplitude = $1\,V$

### 4.1 Building the Circuit

1. Open LTspice → **File → New Schematic**.
2. Place components using the toolbar icons or keyboard shortcuts:
   - Press **R** → place a **resistor**. Click to drop it, press **Escape** to stop placing.
   - Press **L** → place an **inductor**.
   - Press **C** → place a **capacitor**.
   - Press **G** → place **ground** (essential — LTspice will not simulate without a ground/node 0 reference).
3. Wire them in series with an independent voltage source:
   - Press **F2** → search "voltage" → place a **voltage source (V1)**.
   - Draw wires (press **F3** or the wire icon) connecting: `V1(+) → R1 → L1 → C1 → V1(−)`, and place ground at the V1(−)/C1 junction (the "bottom rail").
4. Suggested topology (series loop):

```
   N001        N002        N003
V1 +---[R1]---+---[L1]---+---[C1]---+
   |          100Ω        10mH      100nF
   |                                  |
   +----------------------------------+
                    |
                   GND
```

   - Node **N001**: between V1(+) and R1
   - Node **N002**: between R1 and L1
   - Node **N003**: between L1 and C1
   - The bottom node (V1 negative terminal, tied to C1's other end) is **ground (0)**.

5. Label nodes if you like (press **F4**, "Label Net") — e.g., label N001 as `Vin`, N003 as `Vc` — this makes it easier to reference them in plots later. This isn't mandatory; LTspice auto-numbers nodes.

### 4.2 Configuring the AC Source

1. Right-click on **V1** to open its properties.
2. Click **Advanced**.
3. Under **Small signal AC analysis (.AC)**:
   - **AC Amplitude** = `1` (this is the 1V AC magnitude used in the `.ac` sweep — it does NOT need a DC offset for AC analysis)
   - **AC Phase** = `0` (default)
4. You can leave the **DC value** as `0` since we're only doing frequency-domain (AC) analysis, not transient analysis.
5. Click OK. In the schematic, V1 should now show: `V1 AC 1`

> **Why "AC 1"?** The `.ac` analysis in SPICE is a *linear small-signal* analysis — it doesn't care about the source's transient waveform shape at all. It just needs the AC amplitude (and optionally phase) to compute the frequency response via complex (phasor) math, exactly like the derivations in Section 2.

### 4.3 Performing an `.AC` Sweep

1. Go to **Simulate → Edit Simulation Cmd** (or click the small settings icon).
2. Select the **AC Analysis** tab.
3. Configure:
   - **Type of Sweep**: `Decade` (logarithmic — best for resonance curves spanning a wide frequency range)
   - **Number of points per decade**: `200` (gives smooth, high-resolution curves; use 100 for faster/coarser runs)
   - **Start Frequency**: `100` (Hz)
   - **Stop Frequency**: `100k` (Hz)
4. Click OK — LTspice inserts the directive automatically into the schematic.

### 4.4 Appropriate Frequency Range and Points/Decade

For this circuit, $f_0 \approx 5033\,\text{Hz}$. A good rule of thumb is to sweep **roughly 1–2 decades below and above $f_0$**:

- **Start**: 100 Hz (≈ 50× below $f_0$)
- **Stop**: 100 kHz (≈ 20× above $f_0$)
- **Points/decade**: 100–200 (200 gives very smooth curves; fewer points = faster but coarser, less accurate peak reading)

This range comfortably shows the flat low-frequency region, the resonance peak, and the flat high-frequency roll-off, on both sides of $f_0$.

### 4.5 The Exact LTspice Directive

Typed directly (via **Spice Directive**, press **S**), or auto-generated by the dialog above, the directive is:

```
.ac dec 200 100 100k
```

Full netlist-equivalent for this circuit:

```
V1 N001 0 AC 1
R1 N001 N002 100
L1 N002 N003 10m
C1 N003 0 100n
.ac dec 200 100 100k
.backanno
.end
```

### 4.6 Plotting Current and Voltages

1. Click **Run** (▶ or F9 or Simulate → Run). A blank plot pane will appear.
2. **To plot current through the circuit:**
   - Hover over the wire/component `R1` (or any series element, since current is the same everywhere) until the cursor becomes a **current probe** (red clamp icon).
   - Click on **R1** → this plots `I(R1)`, the current magnitude and phase vs frequency (LTspice auto-plots dB magnitude on the left axis and phase on the right by default for AC analysis).
3. **To plot voltages:**
   - Hover near a node until the cursor becomes a **voltage probe** (red pointer).
   - Click on node **N001** → plots $V_{in}$ (should be flat 0 dB / 1V across all frequencies, confirming source amplitude)
   - Click on node **N002** → plots the voltage between R and L
   - Click on node **N003** → plots $V_C$ (voltage across the capacitor alone, since N003 to ground *is* C1)
   - To get $V_L$ specifically (voltage across just the inductor), you need the **difference**: right-click on the plot pane → **Add Trace** → type: `V(N002)-V(N003)`
   - To get $V_R$: `V(N001)-V(N002)`, or simply `I(R1)*100` (same result), or add trace `V(N001,N002)`.
4. **Switch between dB and linear magnitude:**
   - Right-click the left (magnitude) axis → **Manual Limits** → uncheck/change from dB, or right-click plot → in some LTspice versions go to **Plot Settings**.
   - Alternatively, plot linear current directly with trace expression: `mag(I(R1))` for linear magnitude, or just `I(R1)` (LTspice shows dB by default in AC plots, but the underlying data is linear; hover over a trace to see the actual linear value in the status bar, or add `.step` free — simplest is to add trace `abs(I(R1))` for a linear-magnitude view).

### 4.7 Identifying Resonant Frequency, Bandwidth, and Half-Power Frequencies

1. **Resonant frequency ($f_0$):** With `I(R1)` plotted, use the cursor:
   - Click on the trace name at the top to attach **Cursor 1**, then drag it to the **peak** of the current curve.
   - The cursor readout box shows the exact frequency and magnitude — this is your simulated $f_0$ (should read ≈ 5033 Hz) and $I_{max}$ (≈ 10 mA).
   - Alternatively: **right-click the plot → click on trace → Cursor → use "Peak" search** if available, or simply zoom in (drag a box) around the peak for higher precision reading.

2. **Half-power frequencies ($f_1, f_2$):**
   - Compute the half-power current level: $I_{max}/\sqrt{2} \approx 0.707 \times 10\,\text{mA} = 7.07\,\text{mA}$.
   - Attach **Cursor 1** on the rising (left) side of the peak and **Cursor 2** on the falling (right) side, and drag each until the magnitude readout shows ≈ 7.07 mA.
   - These two frequencies are your simulated $f_1$ and $f_2$.
   - The cursor panel typically shows $\Delta$ (delta) between Cursor 1 and Cursor 2 directly — this delta **is your simulated bandwidth**.

3. **Bandwidth verification:** Compare Cursor2_freq − Cursor1_freq (the Δ reading) to your theoretical $BW = R/(2\pi L)$.

4. **Tip — using dB scale:** If viewing current in dB, the half-power points are exactly **−3 dB below the peak** (since power ∝ current², and $20\log_{10}(0.707) \approx -3\,\text{dB}$). You can visually locate the −3dB points directly on a dB-scaled magnitude plot without computing 0.707 manually.

---

## 5. Worked Calculation (R = 100 Ω, L = 10 mH, C = 100 nF, V = 1 V)

### Step 1 — Resonant Frequency

$$f_0 = \frac{1}{2\pi\sqrt{LC}} = \frac{1}{2\pi\sqrt{(10\times10^{-3})(100\times10^{-9})}} = \frac{1}{2\pi\sqrt{1\times10^{-9}}}$$

$$\sqrt{1\times10^{-9}} = 3.1623\times10^{-5}\,\text{s}$$
$$f_0 = \frac{1}{2\pi(3.1623\times10^{-5})} = \frac{1}{1.9869\times10^{-4}}$$

$$\boxed{f_0 \approx 5032.9\ \text{Hz} \approx 5.033\ \text{kHz}}$$

Angular resonant frequency: $\omega_0 = 2\pi f_0 = 1/\sqrt{LC} \approx 31{,}623\ \text{rad/s}$

### Step 2 — Reactances at Resonance (sanity check, should be equal)

$$X_{L0} = \omega_0 L = 31{,}623 \times 0.01 = 316.23\ \Omega$$
$$X_{C0} = \frac{1}{\omega_0 C} = \frac{1}{31{,}623 \times 100\times10^{-9}} = 316.23\ \Omega$$

✅ $X_{L0} = X_{C0}$, confirming resonance.

### Step 3 — Impedance and Maximum Current

At resonance: $|Z| = R = 100\,\Omega$

$$I_{max} = \frac{V}{|Z|} = \frac{1\,\text{V}}{100\,\Omega} = 0.01\,\text{A} = \boxed{10\ \text{mA}}$$

### Step 4 — Quality Factor

$$Q = \frac{\omega_0 L}{R} = \frac{31{,}623 \times 0.01}{100} = \frac{316.23}{100} = \boxed{3.162}$$

(cross-check: $Q = \dfrac{1}{R}\sqrt{L/C} = \dfrac{1}{100}\sqrt{0.01/(100\times10^{-9})} = \dfrac{1}{100}\sqrt{10^5} = \dfrac{316.23}{100} = 3.162$ ✓)

This is a **moderate Q** circuit (not sharply resonant) — expect a visibly broad peak, not a razor-thin spike.

### Step 5 — Bandwidth

$$BW = \frac{R}{2\pi L} = \frac{100}{2\pi(0.01)} = \frac{100}{0.06283} = \boxed{1591.5\ \text{Hz}}$$

(cross-check: $BW = f_0/Q = 5032.9/3.162 = 1591.6$ Hz ✓)

### Step 6 — Half-Power Frequencies (exact formulas)

$$\frac{R}{4\pi L} = \frac{100}{4\pi(0.01)} = 795.8\ \text{Hz}$$
$$\frac{1}{4\pi^2 LC} = \frac{1}{4\pi^2(10^{-9})} = 2.5330\times10^7$$

$$\sqrt{(795.8)^2 + 2.5330\times10^7} = \sqrt{6.333\times10^5 + 2.5330\times10^7} = \sqrt{2.5963\times10^7} = 5095.4$$

$$f_1 = -795.8 + 5095.4 = \boxed{4299.6\ \text{Hz}}$$
$$f_2 = +795.8 + 5095.4 = \boxed{5891.2\ \text{Hz}}$$

**Verification checks:**
- $f_2 - f_1 = 5891.2 - 4299.6 = 1591.6\,\text{Hz}$ ✅ matches BW
- $\sqrt{f_1 f_2} = \sqrt{4299.6 \times 5891.2} = \sqrt{2.5333\times10^7} = 5033.2\,\text{Hz}$ ✅ matches $f_0$ (geometric mean property)

### Step 7 — Voltages at Resonance

$$V_R = I_{max} \times R = 0.01 \times 100 = 1\ \text{V} \quad (= V_{source}, \text{as expected})$$
$$V_L = I_{max} \times X_{L0} = 0.01 \times 316.23 = 3.162\ \text{V} \quad (= Q \times V_{source})$$
$$V_C = I_{max} \times X_{C0} = 0.01 \times 316.23 = 3.162\ \text{V} \quad (= Q \times V_{source})$$

### Summary Table of Theoretical Results

| Quantity | Value |
|---|---|
| $f_0$ | 5032.9 Hz |
| $\omega_0$ | 31,623 rad/s |
| $I_{max}$ | 10 mA |
| $Q$ | 3.162 |
| $BW$ | 1591.5 Hz |
| $f_1$ | 4299.6 Hz |
| $f_2$ | 5891.2 Hz |
| $V_R$ (at $f_0$) | 1 V |
| $V_L$ (at $f_0$) | 3.162 V |
| $V_C$ (at $f_0$) | 3.162 V |

### How to Verify These in LTspice
1. Run the `.ac dec 200 100 100k` sweep described in Section 4.
2. Use cursors on `I(R1)` to find the peak → compare against $f_0 = 5032.9$ Hz and $I_{max} = 10$ mA.
3. Find the 0.707×$I_{max}$ = 7.07 mA points on either side → compare against $f_1 = 4299.6$ Hz and $f_2 = 5891.2$ Hz, and check the Δ cursor reading against $BW = 1591.5$ Hz.
4. Add traces for `V(N002)-V(N003)` (=$V_L$) and `V(N003)` (=$V_C$) → at the resonance frequency, both should read ≈3.16 V (well above the 1V source — visible proof of voltage magnification by Q).
5. Add trace for phase of `I(R1)` — right-click plot, the phase trace (right axis, degrees) should cross **0°** exactly at $f_0$.

---

## 6. Results and Troubleshooting

### 6.1 Theoretical vs. LTspice Comparison Table

*(Fill in your simulated values from cursor readings after running the sweep — expected agreement is typically within 0.1–1%, since SPICE uses ideal components matching the math exactly.)*

| Parameter | Theoretical Value | LTspice Simulated Value | % Difference |
|---|---|---|---|
| $f_0$ | 5032.9 Hz | _______ | _______ |
| $I_{max}$ | 10 mA | _______ | _______ |
| $f_1$ | 4299.6 Hz | _______ | _______ |
| $f_2$ | 5891.2 Hz | _______ | _______ |
| $BW$ | 1591.5 Hz | _______ | _______ |
| $V_L$ at $f_0$ | 3.162 V | _______ | _______ |
| $V_C$ at $f_0$ | 3.162 V | _______ | _______ |
| Phase at $f_0$ | 0° | _______ | _______ |

With ideal SPICE components (no parasitics), the match should be essentially exact — any meaningful deviation usually points to a modeling mistake (see below), not a "real-world" effect.

### 6.2 Common LTspice Mistakes

| Mistake | Symptom | Fix |
|---|---|---|
| **Incorrect unit suffixes** | Values off by factors of 1000 or more (e.g., typing `10` for 10mH instead of `10m`, giving 10H instead) | Always use SPICE suffixes: `f`=10⁻¹⁵, `p`=10⁻¹², `n`=10⁻⁹, `u`=10⁻⁶, `m`=10⁻³, `k`=10³, `Meg`=10⁶ (note: **`M`means milli in some contexts is wrong — SPICE uses `Meg` for mega, and `m` for milli**; a bare `M` is parsed as milli!) |
| **Missing ground (node 0)** | Simulation fails with "less than 2 connections" or "no DC path" errors | Every circuit needs a ground symbol (net label `0`) — SPICE requires a reference node for all voltages |
| **Wrong AC source settings** | Flat/zero output, or `.ac` sweep runs but shows nothing | Ensure the voltage source has `AC 1` (or your desired amplitude) set — a source with only a DC value and no AC amplitude produces zero response in `.ac` analysis |
| **Incorrect sweep range** | Resonance peak cut off at the edge of the plot, or curve looks incomplete/flat | Always sweep at least 1 decade below and above your expected $f_0$; if unsure of $f_0$, start with a very wide range (e.g., 1 Hz to 1 MHz) then narrow down |
| **Too few points/decade** | Jagged curve, imprecise cursor readings for $f_0$/$f_1$/$f_2$ | Use ≥100 points/decade for smooth curves; increase further if you need high precision on cursor-based bandwidth reading |
| **Using `.tran` instead of `.ac`** | Get a time-domain waveform instead of a frequency sweep | For frequency response / resonance curves, you need `.ac`, not `.tran` (transient is for step response, not swept-frequency response) |
| **Forgetting `AC` magnitude on source while also setting a large DC value** | Confusing DC operating point with AC response; DC offset unnecessarily loads/biases circuit | For pure AC analysis, DC value can be `0`; only set DC offset if you specifically need a combined DC+AC test |
| **Probing the wrong node for $V_L$ or $V_C$** | Getting nonsensical or flipped voltage curves | Remember: clicking a **node** gives voltage to ground, not across a component. For voltage *across* L or R (not referenced to ground), use trace expressions like `V(node_a)-V(node_b)` |
| **Reading current from wrong element** | Believing current differs across elements | In a **series** circuit, current is identical through R, L, and C at every frequency — if your `I(R1)`, `I(L1)`, `I(C1)` don't match, double check your topology (a parallel branch may have crept in) |
| **Not zooming in enough on peak** | Misreading exact $f_0$ or missing the true peak value | Use box-zoom (click-drag) around the peak before placing cursors for higher-resolution reading |

---

## 7. Quick Revision

### 7.1 One-Page RLC Resonance Formula Sheet

```
═══════════════════════════════════════════════════════════
           SERIES RLC RESONANCE — FORMULA SHEET
═══════════════════════════════════════════════════════════

REACTANCES
  X_L = 2πfL = ωL                    (Ω, rises with f)
  X_C = 1/(2πfC) = 1/(ωC)            (Ω, falls with f)

IMPEDANCE
  Z = R + j(X_L − X_C)
  |Z| = √[R² + (X_L − X_C)²]
  φ = tan⁻¹[(X_L − X_C)/R]

CURRENT
  I = V / |Z|
  I_max (at resonance) = V / R

RESONANT FREQUENCY
  f₀ = 1 / (2π√(LC))         ω₀ = 1/√(LC)
  (condition: X_L = X_C)

QUALITY FACTOR
  Q = ω₀L/R = (1/R)√(L/C) = 1/(ω₀RC)
  Voltage magnification: V_L = V_C = Q·V_source (at f₀)

BANDWIDTH
  BW = R/(2πL) = f₀/Q     (Hz, between half-power points)

HALF-POWER FREQUENCIES (exact)
  f₁ = −R/(4πL) + √[(R/4πL)² + 1/(4π²LC)]
  f₂ = +R/(4πL) + √[(R/4πL)² + 1/(4π²LC)]
  Identities: f₂ − f₁ = BW        f₀ = √(f₁f₂)

AT RESONANCE
  |Z| = R (minimum)     I = V/R (maximum)
  φ = 0°                Power factor = 1 (unity)
  V_R = V_source         V_L = V_C = Q·V_source

BELOW f₀: Capacitive (φ<0, current leads)
AT f₀:    Resistive  (φ=0)
ABOVE f₀: Inductive  (φ>0, current lags)
═══════════════════════════════════════════════════════════
```

### 7.2 Ten Viva Questions with Short Answers

**Q1. What is series resonance, and what is the necessary condition for it to occur?**
A: Series resonance occurs when the inductive reactance equals the capacitive reactance ($X_L = X_C$), causing the net reactive impedance to cancel and the circuit to behave as a pure resistance.

**Q2. Why is the current maximum at resonance in a series RLC circuit?**
A: Because at resonance, $X_L$ and $X_C$ cancel, making total impedance $|Z|$ equal to just $R$, its minimum possible value — and since $I = V/|Z|$, minimum impedance gives maximum current.

**Q3. What is the power factor at resonance, and why?**
A: Unity (1), because the phase angle $\phi = 0°$ at resonance — voltage and current are perfectly in phase, so the circuit behaves purely resistively.

**Q4. Why can the voltage across L or C exceed the source voltage at resonance?**
A: Because $V_L = V_C = Q \times V_{source}$, and if $Q > 1$, this voltage magnification exceeds the source voltage. This does not violate KVL because $V_L$ and $V_C$ are 180° out of phase and cancel each other in the phasor sum, while $V_R$ alone equals $V_{source}$.

**Q5. Define Quality Factor (Q) and state its physical significance.**
A: $Q = \omega_0 L/R$ is the ratio of energy stored to energy dissipated per cycle (times $2\pi$); physically it indicates how "sharp" the resonance peak is and how much the reactive voltages are magnified relative to the source.

**Q6. How does bandwidth relate to Q-factor?**
A: $BW = f_0/Q$ — a higher Q gives a narrower bandwidth (sharper resonance), while a lower Q gives a wider bandwidth (broader resonance).

**Q7. What are half-power frequencies, and why are they called that?**
A: They are the two frequencies ($f_1$, $f_2$) at which the power delivered to the circuit drops to half its maximum (resonant) value; this corresponds to current dropping to $1/\sqrt{2}$ (≈0.707) of its maximum value.

**Q8. How does the circuit behave below and above resonance?**
A: Below resonance, $X_C > X_L$, so the circuit is net capacitive and current leads voltage. Above resonance, $X_L > X_C$, so the circuit is net inductive and current lags voltage.

**Q9. In LTspice, why do we use `.ac` analysis instead of `.tran` for studying resonance?**
A: `.ac` performs a linear frequency-domain sweep that directly computes magnitude and phase of impedance/current/voltage at each frequency — exactly matching the phasor mathematics of resonance — whereas `.tran` only shows time-domain waveforms at a single fixed frequency, which is not suited for observing a swept frequency response.

**Q10. Why is bandwidth exactly $f_2 - f_1$, and how is it related to $R$ and $L$ but not directly to $C$?**
A: Bandwidth is defined as the frequency span between the two half-power points, and algebraically simplifies to $BW = R/(2\pi L)$ — while $C$ still influences the *location* of $f_0$ (and thus the absolute position of $f_1, f_2$), it cancels out of the *width* $(f_2-f_1)$ expression itself, leaving bandwidth dependent only on $R$ and $L$.

---

---

## 8. Second-Order Response — Step (Transient) Response

A series RLC circuit is a classic **second-order system**. Writing KVL around the loop with the capacitor voltage $v_C(t)$ as the state variable:

$$L\frac{d^2v_C}{dt^2} + R\frac{dv_C}{dt} + \frac{1}{C}v_C = \frac{1}{C}V_{step}$$

Dividing through by $L$ and comparing to the standard second-order form $\ddot{x} + 2\zeta\omega_n\dot{x} + \omega_n^2 x = \omega_n^2 x_{final}$:

$$\omega_n = \frac{1}{\sqrt{LC}} \qquad \zeta = \frac{R}{2}\sqrt{\frac{C}{L}} = \frac{1}{2Q}$$

- $\omega_n$ = **undamped natural frequency** (rad/s) — numerically equal to $\omega_0$, the resonant angular frequency from Section 2.6
- $\zeta$ = **damping ratio** (dimensionless) — determines whether the response is overdamped ($\zeta>1$), critically damped ($\zeta=1$), or underdamped ($\zeta<1$, oscillatory)
- **Note the inverse relationship**: $\zeta = 1/(2Q)$ — a **high-Q** circuit is **lightly damped** (sharp resonance, long-lived oscillation), while a **low-Q** circuit is **heavily damped** (broad resonance, oscillation dies out fast). This is the same physics viewed from two different domains (frequency vs. time).

### 8.1 For This Circuit (R=100Ω, L=10mH, C=100nF)

$$\zeta = \frac{100}{2}\sqrt{\frac{100\times10^{-9}}{0.01}} = 50\sqrt{10^{-5}} = 50 \times 3.1623\times10^{-3} = 0.1581$$

Since $\zeta = 0.1581 < 1$, the circuit is **underdamped** — expect decaying oscillation, matching the earlier finding that $Q = 3.162$ (moderate Q, visibly ringing step response).

$$\omega_n = \omega_0 = 31{,}622.8\ \text{rad/s} \qquad \omega_d = \omega_n\sqrt{1-\zeta^2} = 31{,}622.8\sqrt{1-0.025} = 31{,}223\ \text{rad/s}$$

$$f_d = \frac{\omega_d}{2\pi} = 4969.6\ \text{Hz} \quad \text{(the actual oscillation frequency you'll see in the ringing, slightly below } f_0\text{)}$$

**Underdamped step response** (capacitor voltage, step input $V$ applied at $t=0$):

$$v_C(t) = V\left[1 - \frac{1}{\sqrt{1-\zeta^2}}e^{-\zeta\omega_n t}\sin(\omega_d t + \phi)\right], \qquad \phi = \cos^{-1}(\zeta)$$

Current follows from $i(t) = C\dfrac{dv_C}{dt}$.

**Key transient metrics:**

| Metric | Formula | Value (this circuit) |
|---|---|---|
| Damping ratio $\zeta$ | $\frac{R}{2}\sqrt{C/L} = 1/(2Q)$ | 0.1581 |
| Damped frequency $f_d$ | $\frac{\omega_n\sqrt{1-\zeta^2}}{2\pi}$ | 4969.6 Hz |
| % Overshoot | $e^{-\zeta\pi/\sqrt{1-\zeta^2}} \times 100$ | 60.4% |
| Peak time $t_p$ | $\pi/\omega_d$ | 100.6 μs |
| Settling time (2%) $t_s$ | $4/(\zeta\omega_n)$ | 0.8 ms |

**Interpretation:** With $Q\approx3.16$ this circuit is moderately underdamped — you'll see roughly 60% overshoot and a handful of visibly decaying oscillation cycles in $v_C(t)$ before it settles near $V$, with $i(t)$ showing a decaying oscillation that starts and ends at zero (since steady-state series current through a capacitor under a DC step is zero).

### 8.2 Verifying in LTspice

1. Change **V1** to a **PULSE** or **step-like** source for transient analysis: right-click V1 → set `PULSE(0 1 0 1n 1n 10m 20m)` (0V to 1V step, ~instant rise, held for 10ms).
2. Replace the `.ac` directive with a transient directive: `.tran 0 2m 0 1u` (simulate 0 to 2ms, max timestep 1μs for smooth resolution of the ringing).
3. Run, then plot `V(N003)` (capacitor voltage) and `I(R1)` (current) vs. time.
4. Use cursors to confirm: overshoot peak near $t_p\approx100.6\,\mu s$, oscillation period $\approx 1/f_d \approx 201\,\mu s$, and settling within $\approx0.8\,ms$.

### 8.3 Python Code — Step Response Plot

```python
import numpy as np
import matplotlib.pyplot as plt

R, L, C, V = 100, 10e-3, 100e-9, 1.0
wn = 1/np.sqrt(L*C)
zeta = (R/2)*np.sqrt(C/L)
wd = wn*np.sqrt(1-zeta**2)
phi = np.arccos(zeta)

t = np.linspace(0, 2e-3, 2000)
env = np.exp(-zeta*wn*t)
vc = V*(1 - (1/np.sqrt(1-zeta**2))*env*np.sin(wd*t+phi))
dvc = (1/np.sqrt(1-zeta**2))*env*(zeta*wn*np.sin(wd*t+phi) - wd*np.cos(wd*t+phi))
i_ma = C*dvc*1000  # mA

fig, axs = plt.subplots(2, 1, figsize=(8, 6), sharex=True)
axs[0].plot(t*1000, vc)
axs[0].set_ylabel("V_C (V)")
axs[0].set_title("Series RLC step response (underdamped)")
axs[0].grid(True, alpha=0.3)

axs[1].plot(t*1000, i_ma, color='tab:orange')
axs[1].set_ylabel("i (mA)")
axs[1].set_xlabel("time (ms)")
axs[1].grid(True, alpha=0.3)

plt.tight_layout()
plt.savefig("step_response.png", dpi=150)
plt.show()

print(f"zeta={zeta:.4f}, wn={wn:.1f} rad/s, wd={wd:.1f} rad/s, fd={wd/2/np.pi:.1f} Hz")
print(f"overshoot={np.exp(-zeta*np.pi/np.sqrt(1-zeta**2))*100:.1f}%")
print(f"settling time (2%) = {4/(zeta*wn)*1000:.3f} ms")
```

---

## 9. Q-Factor Plots

### 9.1 Frequency Response for Different Q Values (Same $f_0$)

Holding $L$ and $C$ fixed (so $f_0$ stays constant) and varying only $R$ shows directly how $Q = \omega_0 L/R$ controls the **sharpness** of the resonance peak:

| $R$ (Ω) | $Q = 316.23/R$ | Peak character |
|---|---|---|
| 20 | 15.81 | Very sharp, tall, narrow peak |
| 50 | 6.32 | Sharp peak |
| 100 | 3.16 | Moderate peak (this guide's example) |
| 200 | 1.58 | Broad peak |
| 500 | 0.63 | Very broad, low peak (heavily damped) |

**Why this happens:** $I_{max} = V/R$ — smaller $R$ directly gives a taller peak. Simultaneously, $BW = R/(2\pi L)$ — smaller $R$ also gives a narrower bandwidth. Both effects compound: low-R circuits are tall *and* narrow (high Q), high-R circuits are short *and* wide (low Q). The resonant frequency $f_0$ itself is untouched by $R$, since $f_0$ depends only on $L$ and $C$.

### 9.2 Q vs. R Relationship

Since $Q = \dfrac{\omega_0 L}{R}$ with $\omega_0$ and $L$ fixed, $Q$ is **inversely proportional to R** — a hyperbola. Doubling $R$ exactly halves $Q$; this is a direct, simple design lever: to sharpen a resonant filter, reduce series resistance (parasitic or intentional); to broaden it, add series resistance.

Equivalently, in terms of damping ratio: $\zeta = 1/(2Q)$, so **increasing R increases damping** — consistent with Section 8's finding that higher Q (lower R) circuits ring longer in the time domain.

### 9.3 Python Code — Q-Factor Plots

```python
import numpy as np
import matplotlib.pyplot as plt

L, C, V = 10e-3, 100e-9, 1.0
Rs = [20, 50, 100, 200, 500]
f = np.logspace(2, 5, 500)  # 100 Hz to 100 kHz
w = 2*np.pi*f
w0 = 1/np.sqrt(L*C)

# --- Frequency response overlay for varying Q ---
plt.figure(figsize=(8, 5))
for R in Rs:
    XL = w*L
    XC = 1/(w*C)
    Z = np.sqrt(R**2 + (XL-XC)**2)
    I = (V/Z)*1000
    Q = w0*L/R
    plt.semilogx(f, I, label=f"R={R}Ω, Q={Q:.2f}")

plt.xlabel("Frequency (Hz)")
plt.ylabel("Current (mA)")
plt.title("Effect of Q-factor on resonance sharpness (fixed L, C)")
plt.legend()
plt.grid(True, which="both", alpha=0.3)
plt.tight_layout()
plt.savefig("q_factor_response.png", dpi=150)
plt.show()

# --- Q vs R relationship ---
plt.figure(figsize=(6, 4))
R_range = np.linspace(10, 1000, 200)
Q_range = w0*L/R_range
plt.plot(R_range, Q_range)
plt.xlabel("R (Ω)")
plt.ylabel("Q factor")
plt.title("Q vs R (L, C fixed) — hyperbolic relationship")
plt.grid(True, alpha=0.3)
plt.tight_layout()
plt.savefig("q_vs_r.png", dpi=150)
plt.show()
```

### 9.4 Verifying in LTspice

1. Add a **`.step param`** sweep: place a SPICE directive `.step param Rval list 20 50 100 200 500`, and set R1's value to `{Rval}` instead of a fixed number.
2. Re-run the `.ac dec 200 100 100k` sweep — LTspice will overlay all five curves automatically on one plot.
3. Use cursors on each trace to confirm peak current $\approx V/R$ and that all peaks align at the same $f_0\approx5033$ Hz.
4. To see the Q vs R relationship numerically, read the peak current and half-power bandwidth (Section 4.7 method) for each stepped R, and compute $Q=f_0/BW$ — compare against $Q=316.23/R$.

---

*End of reference document. All formulas double-checked against standard derivations; worked values computed for R=100Ω, L=10mH, C=100nF, V=1V.*