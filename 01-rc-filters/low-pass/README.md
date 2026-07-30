# RC Low-Pass Filter — Notes

## 1. Circuit

```
        R
  Vin o--/\/\/\--+------o Vout
                  |
                 ===  C
                  |
  GND o-----------+------o GND
```

Series resistor **R**, shunt capacitor **C** to ground. Output is taken across the capacitor.

## 2. Intuition

- A capacitor's impedance is $Z_C = \dfrac{1}{j\omega C}$ — it's large at low frequencies (acts like an open circuit) and small at high frequencies (acts like a short).
- At **low frequency**: $Z_C \gg R$, so almost all of $V_{in}$ appears across C → $V_{out} \approx V_{in}$.
- At **high frequency**: $Z_C \ll R$, so the capacitor shorts the output to ground → $V_{out} \to 0$.
- Net effect: low frequencies pass through, high frequencies are attenuated — hence **low-pass**.

Physically, the capacitor can't charge/discharge instantly. Fast (high-frequency) wiggles in $V_{in}$ get smoothed out before $V_{out}$ can follow them; slow changes have time to fully charge the cap, so they pass through unchanged.

## 3. Design procedure

To design for a desired cutoff $f_c$:
1. Pick a practical capacitor value $C$ (µF to pF range depending on application).
2. Pick a practical resistance value $R$ (Ω to kΩ range depending on application).
3. Solve for $f_c$: $\ f_c = \dfrac{1}{2\pi R C}$
4. Check loading: the source driving this filter should have low output impedance compared to R, and whatever load follows should have high input impedance compared to $Z_C$ at the frequencies of interest — otherwise the divider ratio shifts.

**Example:** Choose $C = 0.1\ \mu\text{F}$ and $R = 159\ \Omega$:

$$
f_c = \frac{1}{2\pi (159)(0.1\times10^{-6})} \approx 1.0 \times 10^4\ \text{Hz} = 10\ \text{kHz}
$$

## 4. Applications

- **Anti-aliasing filter** before an ADC — removes high-frequency content that would fold back (alias) into the sampled signal.
- **Signal smoothing / noise reduction** — removing high-frequency noise from sensor signals.
- **Audio tone controls** — bass-pass / treble-cut networks.
- **Power supply decoupling / ripple filtering** — smoothing rectified DC.
- **PWM-to-analog conversion** — averaging a PWM signal into a DC-like voltage (common in microcontroller DAC-less analog output).
- **Envelope detection** stage (paired with a rectifier).

## 5. Key limitations to know

- **Not a brick-wall filter** — only −20 dB/decade roll-off; for sharper cutoff you need higher-order filters (cascaded RC stages, active filters, etc.).
- **Loading effects** — an RC low-pass is not a true op-amp buffer stage; connecting a low-impedance load distorts the response. Buffer with an op-amp (active RC filter) if needed.
- **No gain** — passive RC filters can only attenuate, never amplify (max gain = 1, i.e., 0 dB).

## 6. Quick-reference formulas

| Quantity | Formula |
|---|---|
| Time constant | $\tau = RC$ |
| Cutoff frequency | $f_c = \dfrac{1}{2\pi RC}$ |
| Transfer function | $H(j\omega) = \dfrac{1}{1+j\omega RC}$ |
| Magnitude | $\|H\| = \dfrac{1}{\sqrt{1+(\omega RC)^2}}$ |
| Phase | $-\tan^{-1}(\omega RC)$ |
| Roll-off | −20 dB/decade above $f_c$ |