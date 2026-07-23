# LTspice Analog & Power Electronics Portfolio

30 fully-simulated circuits spanning passive filters, transistor-level amplifier design, switching power converters, mixed-signal building blocks (ADC/DAC), and IC-level verification techniques (loop stability, PSRR, PVT corners, Monte Carlo, noise budgeting).

Built to demonstrate practical analog/mixed-signal design and verification skills for **embedded systems, analog electronics, power electronics, semiconductor, and FPGA/ASIC** roles. Each project includes hand-calculated design equations, LTspice schematics, simulation plots, and a comparison of theoretical vs. simulated performance.

---

## Highlights

| Project | Result |
|---|---|
| [#14 Buck Converter](02-intermediate/14-buck-converter/) | Synchronous buck achieving [X]% efficiency at [Y] load, verified via transient + FFT ripple analysis |
| [#18 Bandgap Reference](02-intermediate/18-bandgap-reference/) | Temperature-compensated reference: [X] ppm/°C drift across −40°C to 125°C |
| [#21 LDO with Stability Analysis](03-advanced/21-ldo-stability/) | Loop-stability verified with >45° phase margin across a 10x load range; full PSRR characterization |
| [#30 Capstone: Sensor-to-Digital Signal Chain](capstone/30-signal-chain/) | End-to-end sensor → in-amp → filter → ADC signal chain with system-level noise budgeting and Monte Carlo yield analysis |

*(Replace bracketed values with your actual measured results before publishing.)*

---

## Repository Structure

```
ltspice-analog-portfolio/
├── 01-beginner/            projects 1–10
├── 02-intermediate/        projects 11–20
├── 03-advanced/            projects 21–29
├── capstone/               project 30
└── docs/
    ├── concepts-glossary.md
    └── simulation-cheatsheet.md
```

Each project folder contains:
```
schematic.asc
plots/
README.md
```

---

## Full Project Index

### Beginner
| # | Project | Key Skill |
|---|---|---|
| 1 | [RC Low-Pass & High-Pass Filters](01-beginner/01-rc-filters/) | Bode plots, AC analysis |
| 2 | [RLC Series Resonant Circuit](01-beginner/02-rlc-resonance/) | Second-order response, Q factor |
| 3 | [Diode Rectifier Family](01-beginner/03-rectifiers/) | Diode modeling, FFT ripple analysis |
| 4 | [Zener Voltage Regulator](01-beginner/04-zener-regulator/) | Line/load regulation |
| 5 | [BJT Common-Emitter Amplifier](01-beginner/05-bjt-ce-amp/) | Biasing, small-signal gain |
| 6 | [MOSFET Common-Source Amplifier](01-beginner/06-mosfet-cs-amp/) | Transconductance, temp sweeps |
| 7 | [Op-Amp Inverting/Non-Inverting Amps](01-beginner/07-opamp-amps/) | Feedback theory |
| 8 | [Sallen-Key Active Filter](01-beginner/08-sallen-key-filter/) | Active filter design, Monte Carlo intro |
| 9 | [555 Timer Circuits](01-beginner/09-555-timer/) | Timing circuit design |
| 10 | [Discrete Linear Regulator](01-beginner/10-linear-regulator/) | Feedback regulation, loop intro |

### Intermediate
| # | Project | Key Skill |
|---|---|---|
| 11 | [Two-Stage Miller-Compensated Op-Amp](02-intermediate/11-two-stage-opamp/) | Frequency compensation, phase margin |
| 12 | [Instrumentation Amplifier](02-intermediate/12-in-amp/) | CMRR, noise analysis |
| 13 | [Precision Rectifier & Peak Detector](02-intermediate/13-precision-rectifier/) | Precision analog design |
| 14 | [Buck Converter](02-intermediate/14-buck-converter/) | Switching converter, efficiency |
| 15 | [Boost Converter](02-intermediate/15-boost-converter/) | CCM/DCM, RHP zero |
| 16 | [Flyback Converter](02-intermediate/16-flyback-converter/) | Isolated topology, transformer modeling |
| 17 | [Class AB Push-Pull Amplifier](02-intermediate/17-class-ab-amp/) | THD/FFT distortion analysis |
| 18 | [Bandgap Voltage Reference](02-intermediate/18-bandgap-reference/) | Temperature compensation |
| 19 | [Phase-Locked Loop Building Blocks](02-intermediate/19-pll/) | Loop-filter design, lock time |
| 20 | [Flash/SAR ADC Front End](02-intermediate/20-adc-front-end/) | ENOB, INL/DNL |

### Advanced
| # | Project | Key Skill |
|---|---|---|
| 21 | [LDO with Stability Analysis](03-advanced/21-ldo-stability/) | Loop stability, PSRR |
| 22 | [Current-Mode Buck + Compensator](03-advanced/22-current-mode-buck/) | Type II/III compensation |
| 23 | [8-bit R-2R DAC](03-advanced/23-r2r-dac/) | Full mixed-signal characterization |
| 24 | [RF Low-Noise Amplifier](03-advanced/24-lna/) | Noise figure, impedance matching |
| 25 | [Fully-Differential Amp with CMFB](03-advanced/25-cmfb-amp/) | Dual-loop stability |
| 26 | [PVT Corner Analysis](03-advanced/26-pvt-corners/) | Process/voltage/temp verification |
| 27 | [Switched-Capacitor Sample-and-Hold](03-advanced/27-sc-sample-hold/) | Discrete-time analog design |
| 28 | [Multi-Rail PMU System](03-advanced/28-multi-rail-pmu/) | System-level power integration |
| 29 | [Crystal Oscillator + Phase Noise](03-advanced/29-crystal-oscillator/) | Oscillator startup, phase noise |

### Capstone
| # | Project | Key Skill |
|---|---|---|
| 30 | [Sensor-to-Digital Signal Chain](capstone/30-signal-chain/) | System integration, noise budgeting, Monte Carlo yield |

---

## Methodology

Every project follows the same verification discipline used in industry analog design:
- Hand-calculated design equations *before* simulation
- Theoretical vs. simulated performance comparison
- Appropriate analysis type per circuit (DC, AC, transient, FFT, noise, Monte Carlo, or PVT corners)
- Explicit discussion of discrepancies and design limitations

## Tools
- LTspice XVII
