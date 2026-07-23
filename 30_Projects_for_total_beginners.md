# 30 LTspice Portfolio Projects for an ECE Grad

Built for a near-total beginner. Projects escalate in complexity so each one teaches you the next simulation skill you'll need.

---

## How to use this document
- Do the projects **in order** — later ones assume tools/concepts from earlier ones.
- Every project lists which LTspice analyses to run. Don't skip "boring" ones like DC operating point — interviewers ask about these first.
- Save every project as its own folder: schematic (`.asc`), plots (`.png`/`.pdf`), and a `README.md` (template given in the roadmap doc).

---

# BEGINNER (Projects 1–10)
Goal: learn the LTspice interface, core passive/active devices, and the four analyses you'll use constantly (DC operating point, DC sweep, AC sweep, transient).

### 1. RC Low-Pass & High-Pass Filter Pair
- **Difficulty:** Beginner
- **Objective:** Learn schematic capture, AC analysis, and Bode plots.
- **Circuit overview:** Single resistor + capacitor, built two ways (low-pass, high-pass).
- **Key components:** R, C, AC voltage source.
- **Simulations:** `.AC` sweep (decade, 10 Hz–10 MHz); `.TRAN` with a square wave input to see edge rounding.
- **Performance metrics:** −3 dB cutoff frequency, roll-off (dB/decade), phase shift at cutoff.
- **Real-world application:** Anti-aliasing filters, audio tone controls, sensor signal conditioning.
- **Skills demonstrated:** Schematic capture, Bode plot reading, first-order system intuition.
- **Resume value:** "Characterized frequency response of first-order RC filters using LTspice AC analysis."

### 2. RLC Series Resonant Circuit
- **Difficulty:** Beginner
- **Objective:** Understand resonance, Q factor, and damping.
- **Circuit overview:** R, L, C in series driven by an AC source; observe peak/notch response.
- **Key components:** R, L, C.
- **Simulations:** `.AC` sweep around resonant frequency; `.TRAN` step response for underdamped/critically damped/overdamped cases.
- **Performance metrics:** Resonant frequency f₀, quality factor Q, bandwidth, damping ratio.
- **Real-world application:** RF tank circuits, EMI filters, crystal oscillator modeling.
- **Skills demonstrated:** Second-order system analysis, parameter sweeps (`.step param`).
- **Resume value:** "Simulated second-order RLC response and validated Q-factor against analytical calculations."

### 3. Diode Rectifier Family (Half-Wave, Full-Wave, Bridge)
- **Difficulty:** Beginner
- **Objective:** Learn diode models and ripple analysis.
- **Circuit overview:** Three rectifier topologies feeding an RC smoothing filter.
- **Key components:** 1N4148/1N4007 diodes, smoothing capacitor, load resistor.
- **Simulations:** `.TRAN` over several AC cycles; FFT of output to quantify ripple harmonics.
- **Performance metrics:** DC output voltage, ripple voltage (Vpp), ripple frequency, efficiency.
- **Real-world application:** Every AC-DC power supply front end.
- **Skills demonstrated:** Diode modeling, FFT-based ripple analysis.
- **Resume value:** "Designed and compared rectifier topologies, quantifying ripple via FFT analysis in LTspice."

### 4. Zener Diode Voltage Regulator
- **Difficulty:** Beginner
- **Objective:** Learn basic voltage regulation and line/load regulation metrics.
- **Circuit overview:** Series resistor + Zener diode shunt regulator.
- **Key components:** Zener diode, series resistor, variable load.
- **Simulations:** `.DC` sweep of input voltage (line regulation) and load resistance (load regulation).
- **Performance metrics:** Line regulation (%), load regulation (%), Zener power dissipation.
- **Real-world application:** Simple reference voltages, low-current regulation.
- **Skills demonstrated:** DC sweep analysis, regulator metric calculation.
- **Resume value:** "Quantified line and load regulation of a Zener shunt regulator via DC sweep analysis."

### 5. BJT Common-Emitter Amplifier
- **Difficulty:** Beginner
- **Objective:** Learn transistor biasing and small-signal gain.
- **Circuit overview:** Single-stage CE amp with voltage-divider bias, emitter degeneration, coupling/bypass caps.
- **Key components:** NPN BJT (2N2222 model), bias resistors, coupling capacitors.
- **Simulations:** `.OP` for bias point verification; `.AC` for gain/bandwidth; `.TRAN` to check clipping/distortion at large signal swing.
- **Performance metrics:** Voltage gain (dB), input/output impedance, bandwidth, THD at rated output.
- **Real-world application:** Audio pre-amp stages, sensor front-ends.
- **Skills demonstrated:** BJT biasing, small-signal vs. large-signal analysis, distortion measurement.
- **Resume value:** "Designed and biased a BJT CE amplifier, verifying gain and linearity through AC/transient co-simulation."

### 6. MOSFET Common-Source Amplifier
- **Difficulty:** Beginner
- **Objective:** Compare MOSFET biasing/gain behavior to BJT.
- **Circuit overview:** NMOS CS amp with resistive bias network.
- **Key components:** NMOS (e.g., irf-series or generic level-1 model), bias resistors.
- **Simulations:** `.OP`, `.DC` sweep of Vgs to extract transconductance, `.AC` for gain.
- **Performance metrics:** gm, gain, output swing, bias point stability across temperature (`.TEMP` sweep).
- **Real-world application:** Low-power analog front ends, RF LNA precursor topology.
- **Skills demonstrated:** MOSFET square-law behavior, gm extraction, temperature sweeps.
- **Resume value:** "Extracted MOSFET transconductance and gain via DC/AC sweeps; validated temperature stability."

### 7. Op-Amp Inverting & Non-Inverting Amplifiers
- **Difficulty:** Beginner
- **Objective:** Learn ideal op-amp usage and closed-loop gain setting.
- **Circuit overview:** Two configurations built side-by-side with a generic op-amp model (e.g., LT1001/UniversalOpAmp2).
- **Key components:** Op-amp, feedback/input resistors.
- **Simulations:** `.AC` for gain and bandwidth; `.TRAN` for slew-rate-limited step response.
- **Performance metrics:** Closed-loop gain accuracy vs. theoretical, −3 dB bandwidth, slew rate.
- **Real-world application:** Instrumentation front-ends, sensor signal scaling.
- **Skills demonstrated:** Feedback theory, gain-bandwidth tradeoff.
- **Resume value:** "Validated closed-loop gain and bandwidth of op-amp amplifier configurations against theoretical predictions."

### 8. Active Filters (Sallen-Key Low-Pass & High-Pass)
- **Difficulty:** Beginner→Intermediate bridge
- **Objective:** Learn 2nd-order active filter design and component sensitivity.
- **Circuit overview:** Sallen-Key topology using op-amp + RC network.
- **Key components:** Op-amp, resistors, capacitors.
- **Simulations:** `.AC` sweep for magnitude/phase; `.step param` sweeping R or C to see cutoff-frequency sensitivity; basic Monte Carlo (component tolerance) on cutoff frequency.
- **Performance metrics:** Cutoff frequency accuracy, filter Q, passband ripple, roll-off.
- **Real-world application:** Anti-aliasing filters ahead of ADCs — directly relevant to embedded/mixed-signal roles.
- **Skills demonstrated:** Active filter design, Monte Carlo basics, component tolerance impact.
- **Resume value:** "Designed a Sallen-Key active filter and used Monte Carlo analysis to quantify cutoff-frequency sensitivity to component tolerance."

### 9. Astable & Monostable 555 Timer Circuits
- **Difficulty:** Beginner
- **Objective:** Learn behavioral/subcircuit models and timing-circuit design.
- **Circuit overview:** 555 timer in astable (square-wave generator) and monostable (one-shot) configurations.
- **Key components:** NE555 subcircuit, timing R/C network.
- **Simulations:** `.TRAN` for waveform generation; parameter sweep of R/C to hit a target frequency/duty cycle.
- **Performance metrics:** Output frequency, duty cycle, pulse width accuracy vs. calculated.
- **Real-world application:** Clock generation, watchdog timers, PWM basics for embedded systems.
- **Skills demonstrated:** Subcircuit/IC-model usage, timing-circuit design.
- **Resume value:** "Designed 555-based astable/monostable timing circuits and validated frequency/duty-cycle accuracy in simulation."

### 10. Basic Linear Voltage Regulator (Discrete, Pre-LDO)
- **Difficulty:** Beginner (capstone for this tier)
- **Objective:** Combine BJT + Zener + feedback concepts into your first "real" power circuit.
- **Circuit overview:** Series-pass BJT regulator with Zener reference and error amplifier.
- **Key components:** Pass transistor, Zener reference, op-amp error amp, output cap.
- **Simulations:** `.DC` line/load regulation sweep; `.TRAN` for load-transient response (step the load current); `.AC` for loop response (open the loop to check phase margin — your first taste of stability analysis).
- **Performance metrics:** Line/load regulation, transient recovery time, output voltage accuracy, loop phase margin.
- **Real-world application:** Precursor to LDOs used in every embedded board.
- **Skills demonstrated:** Feedback regulator design, load-transient testing, intro to loop stability.
- **Resume value:** "Built a discrete linear regulator with closed-loop feedback and characterized load-transient and stability performance."

---

# INTERMEDIATE (Projects 11–20)
Goal: multi-stage design, stability analysis, switching converters, noise, and Monte Carlo/worst-case analysis — the skills that separate "coursework" from "portfolio."

### 11. Two-Stage Op-Amp Design (Miller-Compensated)
- **Difficulty:** Intermediate
- **Objective:** Learn op-amp internals: differential pair + gain stage + compensation.
- **Circuit overview:** NMOS differential input pair, current mirror load, common-source second stage, Miller compensation cap.
- **Key components:** Discrete MOSFETs, current sources, compensation capacitor/resistor.
- **Simulations:** `.OP` for bias verification; `.AC` loop-gain analysis (open-loop Bode plot) for phase margin; `.TRAN` step response for overshoot/settling time.
- **Performance metrics:** DC gain (dB), unity-gain bandwidth, phase margin, slew rate, settling time.
- **Real-world application:** Building block of every ADC/DAC, sensor interface, and power-management IC.
- **Skills demonstrated:** Transistor-level analog design, frequency compensation, stability analysis.
- **Resume value:** "Designed a two-stage Miller-compensated op-amp achieving [X] dB gain and [Y]° phase margin, verified via loop-gain simulation."

### 12. Instrumentation Amplifier (3 Op-Amp Topology)
- **Difficulty:** Intermediate
- **Objective:** Learn differential signal amplification and common-mode rejection.
- **Circuit overview:** Classic 3-op-amp in-amp with a single gain-set resistor.
- **Key components:** 3 op-amps, precision resistor network.
- **Simulations:** `.AC` differential gain vs. common-mode gain (two separate runs) to compute CMRR; Monte Carlo on resistor tolerance to see CMRR degradation.
- **Performance metrics:** CMRR (dB), gain accuracy, input-referred noise (from `.noise` analysis).
- **Real-world application:** Bio-signal acquisition (ECG/EMG), strain-gauge/load-cell front ends — high value for embedded sensor work.
- **Skills demonstrated:** Differential design, CMRR calculation, Monte Carlo, `.noise` analysis.
- **Resume value:** "Designed an instrumentation amplifier and quantified CMRR degradation due to resistor mismatch using Monte Carlo analysis."

### 13. Precision Rectifier & Peak Detector
- **Difficulty:** Intermediate
- **Objective:** Overcome diode forward-drop limitations using op-amp feedback.
- **Circuit overview:** Super-diode precision rectifier followed by a peak-hold capacitor stage.
- **Key components:** Op-amp, diode, hold capacitor, discharge resistor.
- **Simulations:** `.TRAN` with various input amplitudes/frequencies; droop-rate measurement over hold time.
- **Performance metrics:** Rectification accuracy at low amplitude, peak droop rate, response time.
- **Real-world application:** Envelope detection, RF power measurement, audio metering.
- **Skills demonstrated:** Precision analog design, feedback around nonlinear elements.
- **Resume value:** "Designed a precision peak detector and characterized droop rate against hold-capacitor sizing."

### 14. Buck Converter (Non-Isolated Step-Down)
- **Difficulty:** Intermediate
- **Objective:** Enter switching power electronics — your first converter.
- **Circuit overview:** PWM-controlled buck stage: switch, diode/synchronous FET, inductor, output cap; behavioral PWM comparator or use LTspice's built-in voltage-controlled switch.
- **Key components:** Power MOSFET, Schottky diode, inductor, output capacitor, PWM controller (behavioral or IC model).
- **Simulations:** `.TRAN` steady-state and startup; FFT on output ripple and switch node; efficiency calculation (input vs. output power); load-transient step.
- **Performance metrics:** Output ripple (mV), efficiency (%), inductor current ripple, load-transient over/undershoot and recovery time.
- **Real-world application:** Point-of-load regulators on every embedded/digital board (powering FPGAs, MCUs, SoCs).
- **Skills demonstrated:** Switching converter design, efficiency analysis, FFT-based ripple quantification.
- **Resume value:** "Designed a synchronous buck converter achieving [X]% efficiency at [Y] load, validated via transient and FFT ripple analysis."

### 15. Boost Converter (Step-Up)
- **Difficulty:** Intermediate
- **Objective:** Understand right-half-plane zero behavior and CCM/DCM operation.
- **Circuit overview:** Boost topology with PWM control.
- **Key components:** Inductor, power switch, diode, output cap.
- **Simulations:** `.TRAN` across CCM and DCM (vary load to force mode transition); loop-gain `.AC` analysis (using an averaged model or injection technique) to observe RHP zero effect on phase margin.
- **Performance metrics:** Output voltage regulation, CCM/DCM boundary current, phase margin, efficiency.
- **Real-world application:** Battery-powered embedded systems needing higher rail voltage than the battery provides.
- **Skills demonstrated:** Converter mode analysis, RHP zero intuition, small-signal loop analysis of switchers.
- **Resume value:** "Analyzed CCM/DCM behavior of a boost converter and evaluated loop stability in the presence of the RHP zero."

### 16. Flyback Converter (Isolated)
- **Difficulty:** Intermediate→Advanced bridge
- **Objective:** Learn transformer-isolated conversion and leakage inductance effects.
- **Circuit overview:** Flyback with coupled inductor (transformer model), primary switch, secondary rectifier, snubber network.
- **Key components:** Coupled inductor (K statement in LTspice), MOSFET, output diode, RCD snubber.
- **Simulations:** `.TRAN` steady-state; snubber-off vs. snubber-on comparison to show voltage spike suppression; efficiency calc.
- **Performance metrics:** Output regulation, leakage-spike voltage, snubber power loss, efficiency.
- **Real-world application:** Isolated AC-DC adapters, offline power supplies — a core power-electronics interview topic.
- **Skills demonstrated:** Transformer modeling, snubber design, isolated topology tradeoffs.
- **Resume value:** "Modeled a flyback converter with coupled-inductor leakage and designed an RCD snubber to suppress switch-node overshoot."

### 17. Class AB Push-Pull Audio Amplifier
- **Difficulty:** Intermediate
- **Objective:** Learn crossover distortion and biasing solutions.
- **Circuit overview:** Complementary BJT push-pull output stage with diode/Vbe-multiplier bias.
- **Key components:** NPN/PNP pair, bias diodes, driver stage.
- **Simulations:** `.TRAN` with sine input; FFT for THD; compare biased vs. unbiased (Class B) crossover distortion.
- **Performance metrics:** THD (%), output power, crossover distortion magnitude, efficiency.
- **Real-world application:** Audio power amplifiers, motor-drive output stages.
- **Skills demonstrated:** Distortion analysis via FFT, biasing tradeoffs, power-stage design.
- **Resume value:** "Quantified crossover distortion reduction in a Class AB stage using FFT-based THD analysis."

### 18. Bandgap Voltage Reference
- **Difficulty:** Intermediate
- **Objective:** Learn temperature-compensated reference design — a classic IC building block.
- **Circuit overview:** PTAT + CTAT current summation using BJTs to cancel first-order temperature drift.
- **Key components:** BJTs (diode-connected), resistors, op-amp for loop closure.
- **Simulations:** `.DC` sweep with `.STEP TEMP` (e.g., −40°C to 125°C) to plot output vs. temperature; Monte Carlo on resistor/BJT mismatch for output spread.
- **Performance metrics:** Temperature coefficient (ppm/°C), output voltage spread (Monte Carlo σ), PSRR.
- **Real-world application:** Every ADC/DAC, power-management IC, and sensor needs a reference — a top semiconductor-interview topic.
- **Skills demonstrated:** Temperature-compensated design, multi-corner (temp + Monte Carlo) analysis.
- **Resume value:** "Designed a bandgap reference achieving [X] ppm/°C drift across −40°C to 125°C, verified via temperature-stepped Monte Carlo simulation."

### 19. Phase-Locked Loop (PLL) Building Blocks
- **Difficulty:** Intermediate
- **Objective:** Learn phase detector, charge pump, and loop filter design.
- **Circuit overview:** XOR or phase-frequency detector + charge pump + RC loop filter driving a behavioral VCO.
- **Key components:** Digital gates (behavioral), charge-pump current sources, loop-filter RC, behavioral VCO (voltage-controlled behavioral source).
- **Simulations:** `.TRAN` lock-acquisition transient; measure lock time and steady-state phase error; loop-filter component sweep to see lock-time/ripple tradeoff.
- **Performance metrics:** Lock time, reference spur level (via FFT), loop bandwidth, damping factor.
- **Real-world application:** Clock generation/recovery in every SoC, FPGA transceiver, and communication system.
- **Skills demonstrated:** Mixed analog-behavioral modeling, loop-filter design, lock-time characterization.
- **Resume value:** "Built a charge-pump PLL model and characterized lock time and reference spurs — directly applicable to FPGA/SoC clocking."

### 20. Comparator-Based ADC Front End (Flash/SAR Concept Demo)
- **Difficulty:** Intermediate (capstone for this tier)
- **Objective:** Bridge analog design to digital/embedded interfacing.
- **Circuit overview:** Resistor-ladder reference + comparator bank (simple flash ADC) OR a SAR-logic behavioral model with a single comparator + DAC feedback.
- **Key components:** Comparators, resistor ladder or R-2R DAC, behavioral SAR logic (Verilog-A or simple state logic).
- **Simulations:** `.TRAN` with ramp/sine input to generate a digital code sequence; FFT of reconstructed output to estimate ENOB; Monte Carlo on comparator offset/resistor mismatch to see INL/DNL degradation.
- **Performance metrics:** Resolution (bits), ENOB, INL/DNL, conversion time.
- **Real-world application:** Every embedded system's sensor-to-microcontroller interface.
- **Skills demonstrated:** Mixed-signal design, ENOB/INL/DNL extraction, comparator offset analysis.
- **Resume value:** "Modeled a flash/SAR ADC front end and extracted ENOB/INL/DNL under comparator offset and resistor-mismatch variation."

---

# ADVANCED (Projects 21–30)
Goal: IC-level rigor — stability margins, noise budgets, PSRR, process/voltage/temperature (PVT) corners, and system-level power delivery. This tier is what makes a portfolio look like real semiconductor/analog-IC work.

### 21. Low-Dropout Regulator (LDO) with Stability Analysis
- **Difficulty:** Advanced
- **Objective:** Design a full feedback-loop LDO and rigorously verify stability across load/ESR conditions.
- **Circuit overview:** Error amp, pass PMOS, feedback divider, output cap with variable ESR.
- **Key components:** PMOS pass device, op-amp/OTA error amplifier, feedback resistors, output capacitor (swept ESR).
- **Simulations:** `.AC` loop-gain (break-the-loop technique) across load current and output-cap ESR corners; `.TRAN` load-transient (0→full load step); Monte Carlo on error-amp offset for output accuracy.
- **Performance metrics:** Phase margin across all corners, PSRR (dB) via `.AC` injection on the supply, load-transient overshoot/undershoot and settling time, dropout voltage.
- **Real-world application:** Point-of-load regulation for every microcontroller, FPGA, and RF front-end rail.
- **Skills demonstrated:** Full loop-stability methodology, PSRR simulation, corner-based verification.
- **Resume value:** "Designed an LDO maintaining >45° phase margin across a 10x load range and characterized PSRR and load-transient response."

### 22. Current-Mode Buck Converter with Compensator Design
- **Difficulty:** Advanced
- **Objective:** Design and compensate a peak-current-mode-controlled buck converter.
- **Circuit overview:** Buck power stage + current-sense + Type-II/III compensator feeding a PWM comparator.
- **Key components:** Power stage (from Project 14), current-sense element, error amplifier with compensation network, PWM ramp generator.
- **Simulations:** `.AC` loop-gain analysis for crossover frequency and phase margin; `.TRAN` line and load transients; sub-harmonic oscillation check (slope compensation sweep).
- **Performance metrics:** Crossover frequency, phase/gain margin, transient recovery time, sub-harmonic stability boundary.
- **Real-world application:** Industry-standard control scheme for DC-DC converters in laptops, servers, and embedded power rails.
- **Skills demonstrated:** Compensator design (Type II/III), current-mode control theory, sub-harmonic instability analysis.
- **Resume value:** "Designed and compensated a peak-current-mode buck converter, achieving [X] kHz crossover with >60° phase margin."

### 23. Digital-to-Analog Converter (R-2R Ladder, 8-bit)
- **Difficulty:** Advanced
- **Objective:** Design a full DAC and extract static/dynamic performance metrics.
- **Circuit overview:** 8-bit R-2R resistor ladder driven by behavioral digital switches, output buffer op-amp.
- **Key components:** Precision resistor network, CMOS switches (behavioral or transistor-level), output buffer.
- **Simulations:** `.DC` code sweep for INL/DNL; `.TRAN` for settling time per code transition; FFT for SFDR/SNDR with a full-scale sine reconstructed from codes; Monte Carlo on resistor mismatch for INL/DNL spread.
- **Performance metrics:** INL/DNL (LSB), settling time, SFDR (dB), SNDR, ENOB.
- **Real-world application:** Signal generation in test equipment, audio, and sensor-actuation embedded systems.
- **Skills demonstrated:** Full mixed-signal characterization methodology (the same one used for real DAC datasheets).
- **Resume value:** "Designed an 8-bit R-2R DAC and characterized INL/DNL, SFDR, and settling time under resistor-mismatch Monte Carlo analysis."

### 24. Low-Noise Amplifier (LNA) for RF Front End
- **Difficulty:** Advanced
- **Objective:** Learn noise-figure-driven design and impedance matching.
- **Circuit overview:** Single-stage BJT/MOSFET LNA with input matching network, biased for minimum noise figure.
- **Key components:** RF transistor model, matching L/C network, bias network.
- **Simulations:** `.AC` for gain/S-parameters (via LTspice's `.net` or manual impedance calc); `.noise` analysis for noise figure; `.step` sweep of bias current to find NF-vs-gain tradeoff.
- **Performance metrics:** Gain (dB), noise figure (dB), input return loss, 1-dB compression point (via `.TRAN` sweep of input power).
- **Real-world application:** RF receivers — Wi-Fi/BLE/cellular front ends in embedded/IoT systems.
- **Skills demonstrated:** RF matching, noise-figure optimization, compression-point testing.
- **Resume value:** "Designed an LNA achieving [X] dB gain and [Y] dB noise figure, matched for 50Ω input impedance."

### 25. Fully Differential Amplifier with Common-Mode Feedback (CMFB)
- **Difficulty:** Advanced
- **Objective:** Learn fully-differential topology and CMFB loop design — essential for high-precision ADC drivers.
- **Circuit overview:** Differential pair with CMFB sensing network and auxiliary amplifier setting output common-mode.
- **Key components:** Differential MOSFET pair, CMFB resistor/switched-cap sensing, auxiliary op-amp.
- **Simulations:** `.AC` differential-mode loop gain and common-mode loop gain (two separate loop-gain sims); `.TRAN` common-mode step disturbance rejection.
- **Performance metrics:** Differential gain, CMFB loop phase margin, common-mode rejection/settling.
- **Real-world application:** Driver amplifiers for high-speed/high-precision ADCs in data-converter ICs.
- **Skills demonstrated:** Fully-differential design, dual-loop stability analysis (a genuinely advanced analog IC skill).
- **Resume value:** "Designed a fully-differential amplifier with CMFB, independently verifying differential and common-mode loop stability."

### 26. Temperature & Process Corner Analysis of an Analog Block
- **Difficulty:** Advanced
- **Objective:** Learn PVT (process/voltage/temperature) corner methodology used in real tape-outs.
- **Circuit overview:** Reuse the two-stage op-amp (Project 11) or bandgap (Project 18); build device model corner files (fast/slow/typical) using `.model` parameter variation.
- **Key components:** Same as reused project, plus corner model files.
- **Simulations:** Nested `.step` across process corner, supply voltage, and `.step temp`; batch-run and tabulate gain/bandwidth/phase margin per corner.
- **Performance metrics:** Worst-case gain, worst-case phase margin, spec pass/fail table across all corners.
- **Real-world application:** This is literally what analog IC design verification engineers do before tape-out.
- **Skills demonstrated:** PVT corner methodology, batch simulation, worst-case design verification — a strong semiconductor-industry differentiator.
- **Resume value:** "Performed PVT corner analysis on an op-amp design, tabulating worst-case gain and phase margin across process/voltage/temperature variation."

### 27. Switched-Capacitor Filter / Sample-and-Hold Circuit
- **Difficulty:** Advanced
- **Objective:** Learn discrete-time analog design and clock-feedthrough/charge-injection effects.
- **Circuit overview:** Switched-capacitor integrator or S/H stage using behavioral switches with finite on-resistance and clock signals.
- **Key components:** MOSFET switches (with realistic Ron/Coff), sampling/hold capacitors, non-overlapping clock generator.
- **Simulations:** `.TRAN` with clock and analog input; measure charge injection error and clock feedthrough voltage; FFT to check aliasing behavior.
- **Performance metrics:** Hold-mode droop, charge-injection error (mV), clock feedthrough (mV), settling time.
- **Real-world application:** Core of every switched-capacitor ADC, filter, and DC-DC charge pump.
- **Skills demonstrated:** Discrete-time analog design, non-ideal switch modeling.
- **Resume value:** "Designed a switched-capacitor sample-and-hold and quantified charge-injection and clock-feedthrough errors."

### 28. Multi-Rail Power Management Unit (PMU) System Simulation
- **Difficulty:** Advanced
- **Objective:** Integrate several converters into one system-level power tree — the kind of design that powers an FPGA/SoC board.
- **Circuit overview:** Combine a buck (core rail, e.g. 1.0 V), an LDO (analog/IO rail, e.g. 3.3 V), and a sequencing/enable network so rails power up in the correct order.
- **Key components:** Reused buck (Project 14/22) and LDO (Project 21) subcircuits, sequencing logic (RC delay or behavioral).
- **Simulations:** `.TRAN` full system power-up sequence; verify rail sequencing timing; combined load-transient on both rails simultaneously to check cross-rail interaction.
- **Performance metrics:** Power-up sequencing time/order accuracy, cross-rail transient coupling, total system efficiency.
- **Real-world application:** Exactly how FPGA/SoC boards power up multiple rails in the required order — a direct FPGA/embedded-hardware talking point.
- **Skills demonstrated:** System-level integration, subcircuit reuse, power-sequencing verification.
- **Resume value:** "Built a multi-rail PMU simulation integrating buck and LDO subcircuits with verified power-up sequencing for FPGA-class loads."

### 29. Crystal Oscillator with Phase Noise Estimation
- **Difficulty:** Advanced
- **Objective:** Learn oscillator startup, amplitude stabilization, and noise-driven jitter/phase-noise concepts.
- **Circuit overview:** Pierce oscillator using a crystal model (motional RLC + shunt cap) and a CMOS/BJT inverting amplifier with amplitude-limiting bias.
- **Key components:** Crystal (RLC + Cp model), inverter/amplifier, load capacitors, bias resistor.
- **Simulations:** `.TRAN` for startup time and steady-state amplitude; FFT for harmonic content; `.noise` analysis on the active devices to estimate phase-noise contribution.
- **Performance metrics:** Startup time, oscillation frequency accuracy, output amplitude stability, estimated phase noise/jitter.
- **Real-world application:** Clock sources for every MCU/FPGA/SoC — a frequently asked embedded-hardware interview topic.
- **Skills demonstrated:** Oscillator design, startup-condition analysis (loop gain > 1 at startup), noise-to-jitter reasoning.
- **Resume value:** "Designed a Pierce crystal oscillator, verifying startup margin and estimating phase-noise contribution via `.noise` analysis."

### 30. Capstone: Fully-Verified Analog Front End for a Sensor-to-MCU Signal Chain
- **Difficulty:** Advanced (capstone)
- **Objective:** Combine everything into one signal chain, verified end-to-end — the single best portfolio centerpiece.
- **Circuit overview:** Sensor model (e.g., resistive bridge) → instrumentation amp (Project 12) → active anti-aliasing filter (Project 8/upgraded) → SAR-ADC front end (Project 20) → digital code output; powered by your LDO (Project 21).
- **Key components:** All of the above reused as subcircuits, integrated on one schematic sheet with hierarchical blocks.
- **Simulations:** Full `.TRAN` signal-chain simulation from sensor stimulus to digital code; noise budget analysis (`.noise` at each stage, summed to input-referred system noise); Monte Carlo across the whole chain for output-code accuracy; PVT corners on the critical stages (reuse Project 26 methodology).
- **Performance metrics:** End-to-end SNR, system-level ENOB, total noise budget (nV/√Hz equivalent), Monte Carlo yield estimate, power consumption.
- **Real-world application:** This is the literal architecture of sensor-interface ICs and embedded data-acquisition boards used across every target industry (embedded, semiconductor, power, FPGA/ASIC I/O).
- **Skills demonstrated:** System-level integration, hierarchical schematic design, noise budgeting, full verification methodology (functional + Monte Carlo + corners).
- **Resume value:** "Architected and verified a complete sensor-to-digital signal chain in LTspice, performing system-level noise budgeting and Monte Carlo yield analysis — demonstrating IC-level verification methodology."

---

## Quick-reference: simulation technique index
| Analysis | First introduced in | Also used in |
|---|---|---|
| `.AC` (Bode plot) | #1 | nearly every project |
| `.TRAN` | #1 | nearly every project |
| `.DC` sweep | #4 | #6, #10, #23 |
| FFT (via `.TRAN` + View>FFT) | #3 | #17, #23, #27, #29 |
| `.STEP PARAM` | #2 | #8, #15, #22 |
| `.STEP TEMP` | #6 | #18, #26 |
| Monte Carlo (`.step` + `mc()` function or `.func`) | #8 | #12, #18, #21, #23, #30 |
| `.noise` | #12 | #24, #29, #30 |
| Loop-gain / stability (break-the-loop) | #10 | #11, #15, #21, #22, #25 |
| PVT corner batch analysis | #26 | #30 |
