# 3-Month LTspice Learning Roadmap
### From near-total beginner to a portfolio-ready analog/power/mixed-signal design skillset
Here is the **3-Month** roadmap for LTspice.

Pairs with `ltspice_30_projects.md`. Roughly 8–10 hrs/week assumed; adjust pace as needed, but don't skip the order — each week's concepts unlock the next.

---

## Month 1 — Foundations (Projects 1–10)
**Concepts to master:** schematic capture, DC operating point, DC sweep, AC/Bode analysis, transient analysis, basic FFT, diode/BJT/MOSFET/op-amp behaviour, first- and second-order systems.

| Week | Projects | Concepts to master | Simulation techniques | Milestone |
|---|---|---|---|---|
| 1 | #1 RC filters, #2 RLC resonance | Passive filter theory, resonance/Q | `.AC`, `.TRAN`, basic `.step param` | First Bode plot read correctly; GitHub repo initialised |
| 2 | #3 Rectifiers, #4 Zener regulator | Diode nonlinearity, ripple, line/load regulation | FFT for ripple, `.DC` sweep | Two projects with full README |
| 3 | #5 BJT CE amp, #6 MOSFET CS amp | Biasing, small-signal gain, gm | `.OP`, `.TEMP` sweep | Comfortable setting bias points from scratch |
| 4 | #7 Op-amp amps, #8 Sallen-Key filter | Feedback, active filters, intro Monte Carlo | Monte Carlo basics | First Monte Carlo histogram produced |
| 5 (buffer/catch-up) | #9 555 timer, #10 Discrete regulator | Timing circuits, first stability/loop concept | Loop-gain intro (break-the-loop) | Month 1 portfolio review — 10 projects documented |

**Documentation habit to build this month:** for every project, write the README *before* you consider it "done" — this forces you actually to understand what you built (see template below).

---

## Month 2 — Intermediate Analog & Power (Projects 11–20)
**Concepts to master:** multi-stage amplifier design, loop stability/phase margin, switching converter fundamentals (buck/boost/flyback), CMRR, temperature-compensated references, PLLs, ADC basics (INL/DNL/ENOB).

| Week | Projects | Concepts to master | Simulation techniques | Milestone |
|---|---|---|---|---|
| 6 | #11 Two-stage op-amp | Differential pairs, current mirrors, Miller compensation | Loop-gain `.AC`, phase margin extraction | Can explain phase margin in an interview |
| 7 | #12 Instrumentation amp, #13 Precision rectifier | CMRR, precision analog | `.noise`, Monte Carlo | First noise-analysis plot |
| 8 | #14 Buck converter, #15 Boost converter | Switching converter basics, CCM/DCM, efficiency | FFT ripple, efficiency calc | First working switcher with measured efficiency |
| 9 | #16 Flyback, #17 Class AB amp | Isolated topologies, transformer modeling, THD | Snubber design, FFT-THD | Comfortable with coupled-inductor (`K`) statements |
| 10 | #18 Bandgap reference, #19 PLL basics | Temperature compensation, phase-locked loops | `.STEP TEMP`, lock-time transient | Reference design with ppm/°C spec |
| 11 | #20 ADC front end | Mixed-signal basics, ENOB/INL/DNL | Code-sweep DC analysis, FFT-based ENOB | First mixed-signal characterization report |

**Concept deep-dive to run alongside simulation this month:** read/skim one analog IC design chapter or datasheet per week that matches the project (e.g., a real LDO or buck-converter datasheet) — connect your sim results to what a real datasheet reports.

---

## Month 3 — Advanced / IC-Level Rigor + Capstone (Projects 21–30)
**Concepts to master:** full loop-stability methodology, PSRR, current-mode control/compensator design, RF noise figure, fully-differential/CMFB, PVT corner methodology, switched-capacitor circuits, system-level power trees, oscillator startup/phase noise.

| Week | Projects | Concepts to master | Simulation techniques | Milestone |
|---|---|---|---|---|
| 12 | #21 LDO with stability analysis | Full loop-stability + PSRR methodology | Corner sweep of ESR/load, PSRR injection | LDO spec sheet: phase margin table across corners |
| 13 | #22 Current-mode buck compensator | Type II/III compensation, sub-harmonic instability | Loop-gain + slope-comp sweep | Can design a compensator from a power-stage transfer function |
| 14 | #23 R-2R DAC, #24 LNA | Full DAC characterization, RF noise figure/matching | INL/DNL extraction, `.noise` NF | Two advanced characterization reports |
| 15 | #25 Fully-differential CMFB, #26 PVT corners | Dual-loop stability, PVT methodology | Nested `.step` (process × voltage × temp) | Worst-case corner table for a prior project |
| 16 | #27 Switched-cap S/H | Discrete-time analog, charge injection | Non-overlapping clocks, transient error measurement | Comfortable with realistic switch modeling |
| 17 | #28 Multi-rail PMU | System-level integration, sequencing | Hierarchical subcircuits, system `.TRAN` | Multi-rail system schematic reusing 2+ prior blocks |
| 18–19 | #29 Crystal oscillator, #30 Capstone signal chain | Oscillator startup, noise budgeting, full-chain verification | `.noise` phase-noise estimate, full Monte Carlo + corner capstone | **Capstone repo finished**: sensor → in-amp → filter → ADC → digital code, fully documented |
| 20 (buffer) | Polish + interview prep | — | — | Portfolio complete, mock interviews done |

---

## Analog design concepts checklist (tick off as mastered)
- [ ] Ohm's law / KVL / KCL sanity-checking sim results by hand
- [ ] Small-signal vs. large-signal analysis
- [ ] BJT and MOSFET biasing (and why bias point matters for gain/distortion)
- [ ] Feedback theory (negative feedback, loop gain, phase margin)
- [ ] First- and second-order system response (Bode, damping, resonance)
- [ ] Filter design (passive and active, Sallen-Key/Butterworth basics)
- [ ] Switching converter fundamentals (buck/boost/flyback, CCM/DCM, efficiency)
- [ ] Compensator design (Type I/II/III) for switching loops
- [ ] Noise analysis and noise budgeting (input-referred noise, `.noise` interpretation)
- [ ] CMRR / PSRR concepts and measurement technique
- [ ] Mixed-signal metrics: INL, DNL, ENOB, SFDR, SNDR
- [ ] PVT corner-based worst-case verification methodology
- [ ] Monte Carlo yield/tolerance analysis
- [ ] Oscillator startup condition (loop gain > 1) and phase noise intuition

## Simulation technique checklist
- [ ] `.OP` — operating point/bias verification
- [ ] `.DC` — DC sweep (line/load regulation, transfer curves)
- [ ] `.AC` — frequency response / Bode plots
- [ ] `.TRAN` — time-domain / transient response
- [ ] FFT (via `.TRAN` output + View > FFT) — harmonic/ripple/THD analysis
- [ ] `.STEP PARAM` — parametric sweeps
- [ ] `.STEP TEMP` — temperature sweeps
- [ ] Monte Carlo (`mc()`/`.step` with tolerance functions) — yield/sensitivity
- [ ] `.noise` — noise analysis
- [ ] Loop-gain / break-the-loop technique — stability, phase margin
- [ ] Nested corner sweeps — PVT worst-case tables

---

## Documentation tips (do this for every single project)
Each project folder should contain:
```
/project-XX-name/
    schematic.asc
    plots/            (Bode plots, transient waveforms, FFT, Monte Carlo histograms)
    README.md
```

**README.md template:**
```markdown
# Project XX: [Title]

## Objective
One sentence: what this circuit does and why it matters.

## Circuit Description
Brief topology explanation + schematic screenshot.

## Design Equations
Key hand-calculated formulas used to size components (shows you didn't just guess values).

## Simulation Results
- Plot 1: [Bode/transient/FFT] — what it shows
- Plot 2: ...
Include measured values vs. hand-calculated/theoretical values in a small table.

## Performance Summary Table
| Metric | Target | Simulated |
|---|---|---|

## What I'd Improve
1–2 sentences — shows engineering judgment, not just task completion.

## Real-World Application
1–2 sentences connecting this to an actual product/industry use case.
```

Habits that make documentation interview-ready:
- Always include a **hand-calculation vs. simulation** comparison — this is what distinguishes an engineer from someone who just clicked "run."
- Screenshot plots with axis labels and units visible (LTspice lets you add text labels — use them).
- Note any discrepancy between theory and simulation and explain *why* (parasitic effects, model limitations, etc.) — this is a favorite interview question.
- Keep a running "lessons learned" doc across all 30 projects — this becomes your interview story bank.

---

## GitHub portfolio structure
```
ltspice-analog-portfolio/
├── README.md                     ← portfolio overview (see below)
├── 01-beginner/
│   ├── 01-rc-filters/
│   ├── 02-rlc-resonance/
│   ├── ... (through project 10)
├── 02-intermediate/
│   ├── 11-two-stage-opamp/
│   ├── ... (through project 20)
├── 03-advanced/
│   ├── 21-ldo-stability/
│   ├── ... (through project 30)
├── docs/
│   ├── concepts-glossary.md       ← your own plain-English notes on each concept
│   └── simulation-cheatsheet.md   ← your personal LTspice syntax reference
└── capstone/
    └── 30-signal-chain/           ← flagship project, linked prominently from top README
```

**Top-level README.md should include:**
- A one-paragraph summary of what this repo demonstrates and which roles it targets.
- A table listing all 30 projects with difficulty, one-line objective, and a link to each folder.
- A "Highlights" section pinning your 3–4 best projects (suggest: #14 Buck Converter, #18 Bandgap Reference, #21 LDO, #30 Capstone) with their key result plots embedded directly in the README so recruiters see results without clicking through.
- Your target roles/industries stated explicitly (embedded, analog, power, semiconductor, FPGA/ASIC) so the repo's purpose is unambiguous.

---

## Interview preparation (weeks 18–20, alongside capstone)
**Be ready to explain, from any of your 30 projects:**
1. Why you chose each component value (design equations, not guesses).
2. What phase margin is and why it matters (pull up your LDO or op-amp Bode plot and walk through it).
3. The difference between DNL/INL and why both matter for a DAC/ADC.
4. Why switching converters need compensation and what happens without it (show a sub-harmonic oscillation plot if you generated one in Project 22).
5. How Monte Carlo differs from corner analysis, and when you'd use each.
6. One real discrepancy you found between hand calculations and simulation, and what caused it.

**Suggested practice format:**
- Pick 3 projects per week (weeks 18–20) and do a 5-minute "whiteboard walkthrough" out loud — objective, topology, key result, one thing you'd improve.
- For embedded/FPGA-leaning interviews, emphasise Projects 14, 20, 28, 29 (power delivery, ADC interfacing, sequencing, clocking) — these map directly onto board-level embedded work.
- For semiconductor/analog-IC-leaning interviews, emphasise Projects 11, 18, 21, 25, 26 (op-amp design, bandgap, LDO stability, CMFB, PVT corners) — these map to IC design-verification interview questions.
- For power-electronics-leaning interviews, emphasise Projects 14–16, 22, 28 (buck/boost/flyback, current-mode control, multi-rail systems).
- Keep one "if I had more time" answer ready per project — interviewers value knowing your circuit's limitations as much as its performance.

---

## Suggested weekly time allocation (8–10 hrs/week)
- 40% — building/simulating the week's project(s)
- 25% — hand-calculations before simulating (do this *first*, not after)
- 20% — documentation (README, plots, GitHub commit)
- 15% — concept review (datasheet reading, glossary notes, revisiting a prior week's weak spot)

---

## End-of-roadmap deliverables checklist
- [ ] 30 fully simulated, documented projects in a public GitHub repo
- [ ] Top-level README with highlights and role targeting
- [ ] Personal concepts glossary and simulation cheat-sheet (your own notes, reusable for interview review)
- [ ] Capstone signal-chain project as the portfolio centrepiece
- [ ] 3–4 "whiteboard-ready" project walkthroughs memorised for interviews
- [ ] At least one PVT corner and one Monte Carlo analysis you can explain in depth
