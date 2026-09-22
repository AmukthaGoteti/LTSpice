#### OBJECTIVE
Build single-pole RC low-pass and high-pass filters, extract the -3 dB cutoff frequency, and characterize the magnitude/phase response with an AC sweep.

#### THEORY NOTES
Cutoff frequency: fc = 1 / (2πRC).
Magnitude rolls off at -20 dB/decade beyond fc (single pole).
Phase transitions across 90° centered on fc: low-pass goes 0° → -90°, high-pass goes 90° → 0°.
At fc exactly, magnitude is -3 dB and phase is ±45°.

#### LTSPICE WORKFLOW
Place a resistor and capacitor in series between an AC input source and ground.
For low-pass, take the output across the capacitor; for high-pass, take it across the resistor.
Set the source's AC amplitude to 1 (SPICE directive AC 1) — the DC/transient value is irrelevant for an .ac sweep.
Run '.ac dec 100 1 1Meg' to sweep 1 Hz to 1 MHz with 100 points per decade.
Add trace V(out)/V(in); right-click the trace to display it in dB, and add a second plot pane for phase.
Use cursors (or a .meas statement) to locate the -3 dB point and confirm it matches the calculated fc.

#### EXPECTED RESULTS
Flat magnitude in the passband, -20 dB/decade slope beyond fc, -3 dB exactly at fc.
Phase is 45° (LPF: -45°, HPF: +45°) at fc, asymptoting to 0°/90° well away from it.

#### COMMON PITFALLS
Forgetting the AC 1 magnitude on the source — without it, the .ac sweep produces a flat zero trace.
Probing the wrong node (e.g., across R when you meant to build an LPF).
Cascading a second RC stage directly loads the first stage and shifts fc — a buffer is needed to keep the stages independent.

#### SAMPLE VALUES
R = 10 kΩ, C = 16 nF (fc ≈ 1 kHz)
Source: AC 1, sweep 1 Hz–1 MHz