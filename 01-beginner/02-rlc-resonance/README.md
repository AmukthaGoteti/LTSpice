### OBJECTIVE
Analyze a series RLC bandpass network: extract resonant frequency, bandwidth, and Q from an AC sweep, and correlate with the transient ringing seen in a step response.
### THEORY NOTES
Resonant frequency: f0 = 1 / (2π√(LC)).
Q = f0 / BW = (1/R)√(L/C) for a series RLC driven as a bandpass (output taken across R).
Damping regimes: underdamped (ringing, Q > 0.5), critically damped, overdamped (no ringing) — set by R relative to 2√(L/C).
Damped natural frequency in the transient ringing is close to f0 for high-Q circuits.
### LTSPICE WORKFLOW
Build a series loop: AC/pulse source → L → C → R → back to source return.
For the bandpass characteristic, probe V(R) (or the loop current I(R)) rather than V(C) or V(L) alone.
Run '.ac dec 200 1 100k'; measure the peak frequency and the two -3 dB frequencies to compute BW and Q.
Switch to a pulse or step source and run .tran to observe ringing; measure the ringing period and decay envelope.
Use '.step param R list ...' to sweep R and see the peak sharpen (higher Q) as R decreases.
### EXPECTED RESULTS
A clear resonant peak at f0 in the bandpass magnitude, sharper for lower R (higher Q).
Transient step response shows decaying oscillation whose ring frequency approaches f0 and whose decay rate tracks R/L.
### COMMON PITFALLS
Probing V(C) or V(L) instead of V(R) gives a low-pass or high-pass-like shape, not the bandpass response expected from a series RLC.
Real inductors have series DCR that adds to R and lowers Q — if using a non-ideal inductor model, this shows up as a broader peak than hand calculations predict.
Too coarse an .ac point density near a high-Q peak under-samples the resonance.