# Zener Voltage Regulator

This project studies a simple shunt voltage regulator. A series resistor limits current from the input supply, while a zener diode holds the output near its breakdown voltage. The circuit is evaluated for **line regulation** (input-voltage changes) and **load regulation** (load changes).

## Learning Goals

- Explain how a zener diode maintains an approximately constant output voltage.
- Select a series resistor that limits current safely.
- Determine the operating range in which the zener remains in breakdown.
- Measure line and load regulation in LTspice.
- Compare ideal hand calculations with the non-ideal zener model.

## Circuit Topology

```text
			 R_S
 V_IN o----/\/\/\/----+----o V_OUT
					  |
					 |<|  Zener
					  |
					  +---- R_LOAD ----+
					  |                |
 GND  o---------------+----------------+
```

The zener is connected in reverse bias, with its cathode at `V_OUT` and anode at ground. When the output reaches the zener voltage, additional input current is diverted through the zener instead of producing a proportional rise in output voltage.

The LTspice source file is [schematic.asc](schematic.asc). The available plot assets are [Line_Regulations.jpg](Plots/Line_Regulations.jpg) and [Load_Regulations.jpg](Plots/Load_Regulations.jpg).

## Component Roles

| Element | Role |
|---|---|
| `R_S` | Limits total current from the source and absorbs input-voltage variation. |
| Zener diode | Operates in reverse breakdown and establishes the voltage reference. |
| `R_LOAD` | Represents the circuit powered by the regulator. |
| `V_IN` | DC input supply, swept for line-regulation analysis. |

## Operating Principle

The current through the series resistor divides between the load and the zener:

$$I_S = I_L + I_Z$$

where

$$I_S = \frac{V_{IN}-V_{OUT}}{R_S}, \qquad I_L = \frac{V_{OUT}}{R_{LOAD}}$$

When the zener is regulating, the output is approximately its breakdown voltage:

$$V_{OUT} \approx V_Z$$

The zener can regulate only while its current remains within the model's useful operating range:

$$I_{Z,min} \leq I_Z \leq I_{Z,max}$$

If the load draws too much current, or the input voltage falls too low, $I_Z$ drops below $I_{Z,min}$ and the output voltage falls. If the input voltage is too high or the load is too light, zener power may exceed its rating.

## Design Equations

### Series-resistor selection

For a target zener voltage $V_Z$, choose the resistor using the worst-case input and load conditions:

$$R_S \leq \frac{V_{IN,min}-V_Z}{I_{L,max}+I_{Z,min}}$$

The resistor must also limit current at the highest input voltage and lightest load:

$$R_S \geq \frac{V_{IN,max}-V_Z}{I_{Z,max}+I_{L,min}}$$

These inequalities define a valid resistor range. If no range exists, the regulator cannot meet the requirements with this topology.

### Zener power

The zener's instantaneous power is:

$$P_Z = V_Z I_Z$$

The design must satisfy:

$$P_Z \leq P_{Z,max}$$

Use the worst-case combination of high input voltage and light load when checking this limit.

### Series-resistor power

The resistor dissipates:

$$P_{R_S} = I_S^2 R_S = \frac{(V_{IN}-V_{OUT})^2}{R_S}$$

Choose a resistor with an appropriate power rating and include practical derating.

## Regulation Metrics

### Line regulation

Line regulation measures output change caused by an input-voltage change while the load is held constant:

$$\text{Line regulation} = \frac{\Delta V_{OUT}}{\Delta V_{IN}}$$

It is commonly reported in V/V, mV/V, or as a percentage:

$$\text{Line regulation (\%)} = 100\frac{V_{OUT,max}-V_{OUT,min}}{V_{OUT,nom}}$$

The corresponding plot is [Line_Regulations.jpg](Plots/Line_Regulations.jpg).

### Load regulation

Load regulation measures output change as the load changes while the input remains constant:

$$\text{Load regulation (\%)} = 100\frac{V_{NL}-V_{FL}}{V_{FL}}$$

Here, $V_{NL}$ is the no-load output and $V_{FL}$ is the full-load output. A smaller value indicates better regulation. The corresponding plot is [Load_Regulations.jpg](Plots/Load_Regulations.jpg).

## LTspice Procedure

1. Add a DC source, series resistor, reverse-biased zener model, and load resistor to [schematic.asc](schematic.asc).
2. Run an operating-point analysis and record `V(OUT)`, `I(R_S)`, `I(ZENER)`, and component power.
3. Sweep `V_IN` while keeping `R_LOAD` fixed to generate the line-regulation curve.
4. Sweep `R_LOAD` or its load current while keeping `V_IN` fixed to generate the load-regulation curve.
5. Confirm that each measurement point remains inside the zener's specified current and power limits.
6. Exclude startup or non-regulating regions when calculating the regulated slope.

Typical sweep directives are:

```spice
.dc V1 8 16 0.1
.step param RLOAD 100 1000 100
```

The exact source name and sweep limits must match the completed schematic and selected zener model.

## What to Observe

- In the regulated region, `V(OUT)` changes much less than `V(IN)`.
- At low input voltage, the zener current approaches zero and the output begins to collapse.
- With a heavier load, more series current is consumed by the load and less remains for the zener.
- With a lighter load, zener current increases and zener power becomes the limiting concern.
- A real zener has dynamic resistance, so its output voltage is not perfectly constant:

$$r_Z = \frac{\Delta V_Z}{\Delta I_Z}$$

Lower dynamic resistance produces better load regulation.

## Limitations

This topology is simple and useful for low-current references, but it is inefficient at light load because the zener continuously dissipates power. It also has limited current capability, poor efficiency compared with a switching regulator, and no inherent protection against excessive input voltage or short-circuit conditions.

## Key Takeaways

A zener regulator works by converting excess source voltage into current through the zener. The series resistor protects both the zener and the load, while the zener's breakdown behavior establishes the output voltage. Good design requires checking regulation, zener current, resistor power, and zener power across the full input and load ranges.
