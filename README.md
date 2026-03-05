# MOSFET Amplifier Configurations (TSMC 180 nm)
Linear Integrated Circuits Laboratory

# Experiment 2

This project demonstrates the design and simulation of different MOSFET amplifier configurations using TSMC 180 nm CMOS models in LTspice.
The goal is to study biasing conditions, gain behavior, and frequency response of common analog amplifier structures.

Objective

Design and analyze the following MOS amplifier circuits:

Source Degenerated Common Source Amplifier

Cascode Amplifier

Current Mirror Loaded Common Source Amplifier

The circuits are simulated to observe DC operating points, transient response, voltage gain, and frequency behavior.

# Simulation Environment
| Item            | Description   |
| --------------- | ------------- |
| Simulation Tool | LTspice       |
| Technology      | TSMC 180 nm   |
| Supply Voltage  | 1.5 V         |
| Devices Used    | NMOS and PMOS |


# MOSFET Amplifier Theory

MOSFET amplifiers are typically biased in the saturation region, where the drain current becomes largely independent of drain voltage.

Operating in this region provides:

- Stable voltage gain
- High transconductance
- Predictable small-signal behavior
- Better linearity for analog signals

# Important Equations
| Parameter         | Equation                   |
| ----------------- | -------------------------- |
| Drain Current     | ID = (1/2) μCox (W/L) Vov² |
| Transconductance  | gm = 2ID / Vov             |
| Output Resistance | ro = 1 / (λID)             |
| Voltage Gain      | Av = −gm × Rout            |

# Technology Parameters
Parameter	Value
| Parameter            | Value  |
| -------------------- | ------ |
| Technology Node      | 180 nm |
| Supply Voltage       | 1.5 V  |
| Target Drain Current | 200 µA |
| Overdrive Voltage    | 0.25 V |
| Channel Length       | 180 nm |

# Mobility Values
| Device | Mobility           |
| ------ | ------------------ |
| NMOS   | 273.8 × 10⁻⁴ m²/Vs |
| PMOS   | 115.7 × 10⁻⁴ m²/Vs |

# Oxide Parameters
| Parameter          | Value            |
| ------------------ | ---------------- |
| Oxide Thickness    | 4.1 nm           |
| Oxide Permittivity | 3.54 × 10⁻¹¹ F/m |

Gate oxide capacitance:

Cox = εox / tox

Cox ≈ 8.63 mF/m²

# Process Transconductance
| Device | Value     |
| ------ | --------- |
| μnCox  | 236 µA/V² |
| μpCox  | 100 µA/V² |

# Transistor Size Calculation

Using the MOSFET saturation equation:

ID = (1/2) μCox (W/L) Vov²

Calculated Dimensions
| Device | Width (µm) | Length (µm) | W/L   |
| ------ | ---------- | ----------- | ----- |
| NMOS   | 5          | 0.18        | 27.78 |
| PMOS   | 11.83      | 0.18        | 65.72 |


PMOS width is larger due to lower hole mobility.

# Circuit 2A – Source Degenerated Common Source Amplifier
Design Goal

Design a MOS amplifier that:

- Operates at 200 µA drain current

- Provides maximum symmetric output swing

DC Bias Design
| Parameter | Value   |
| --------- | ------- |
| VDD       | 1.5 V   |
| ID        | 200 µA  |
| VTHn      | 0.36 V  |
| VTHp      | −0.39 V |

# Drain Voltage Selection
For maximum output swing:

- VDS = VDD / 2

- VDS = 0.75 V

# Source Voltage

Chosen value:

- VS = 0.2 V

This improves bias stability.

# Output Voltage

VDS = Vout − VS

- 0.75 = Vout − 0.2

- Vout = 0.95 V

# Source Resistor

- RS = VS / ID

- RS = 1 kΩ

# Gate Voltage

- VGS = VTH + Vov

- VGS = 0.61 V

- VG = VGS + VS

- VG = 0.81 V

# PMOS Gate Voltage

- VSG = Vov + |VTHp|

- VSG = 0.64 V

- VGp = VDD − VSG

- VGp = 0.86 V

# Saturation Verification
| Device | Condition | Result |
| ------ | --------- | ------ |
| NMOS   | VDS ≥ Vov | ✔      |
| PMOS   | VSD ≥ Vov | ✔      |


Both transistors remain in saturation.

# Final Operating Point
| VS    | VDS    | Vout   | VG     | VGp    | ID     | RS   | Vov    |
| ----- | ------ | ------ | ------ | ------ | ------ | ---- | ------ |
| 0.2 V | 0.75 V | 0.95 V | 0.81 V | 0.86 V | 200 µA | 1 kΩ | 0.25 V |

# Width Optimization (Simulation)

Practical widths used in LTspice:

| Device | Width   |
| ------ | ------- |
| NMOS   | 13.2 µm |
| PMOS   | 37.5 µm |

Widths were increased slightly to obtain ID ≈ 200 µA with realistic MOS models.

# Transient Analysis
| Parameter | Value  |
| --------- | ------ |
| Frequency | 1 kHz  |
| Amplitude | 10 mV  |
| DC Bias   | 0.81 V |

LTspice input source:

- Vin = SINE(0.81 10m 1k)
# Input Waveform
images/input_waveform.png
# Output Waveform
images/output_waveform.png
# Input and Output Comparison
images/input_output.png
# Practical Gain Calculation
| Measurement | Value     |
| ----------- | --------- |
| Vin(p-p)    | 9.667 mV  |
| Vout(p-p)   | 99.885 mV |


Voltage gain:

- Av = Vout / Vin

- Av ≈ 10.33

- Gain in dB:

- Gain = 20.28 dB

# AC Frequency Response
| Parameter    | Value     |
| ------------ | --------- |
| Midband Gain | 20.278 dB |
| −3 dB Gain   | 17.278 dB |
| Bandwidth    | 315 MHz   |

# Circuit 2B – Cascode Amplifier

The cascode structure combines a common source stage with a common gate stage to improve output resistance and gain.

# DC Node Voltages
| Node | Voltage |
| ---- | ------- |
| VS2  | 0 V     |
| VS1  | 0.30 V  |
| Vout | 1.05 V  |


All devices remain in saturation.

# Practical Transistor Widths
| Transistor        | Width   |
| ----------------- | ------- |
| M1 (Cascode NMOS) | 16.6 µm |
| M2 (Bottom NMOS)  | 16.6 µm |
| M3 (PMOS Load)    | 38.5 µm |

# Transient Gain Measurement
| Signal | Peak-to-Peak |
| ------ | ------------ |
| Vin    | 0.019 V      |
| Vout   | 0.03256 V    |


Voltage Gain:

- Av = 1.71 V/V

- Gain in dB:

- Gain = 4.66 dB

# AC Analysis Results
| Parameter    | Value   |
| ------------ | ------- |
| Maximum Gain | 4.64 dB |
| −3 dB Gain   | 1.64 dB |
| Bandwidth    | 277 MHz |
