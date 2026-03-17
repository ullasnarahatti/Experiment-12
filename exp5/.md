# MOSFET Amplifier Configurations (TSMC 180 nm)
Linear Integrated Circuits Laboratory

# Experiment 2

![Image](https://github.com/ullasnarahatti/Experiment-12/blob/483f8cc9e3cc4bb25205635ef02c7c52e51012f7/LIC%20FRONT.png)

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
| Technology      | TSMC 180 nm   |
| Supply Voltage  | 1.5 V         |
| Devices Used    | NMOS and PMOS |


# MOSFET Amplifier Theory

MOSFET amplifiers are typically biased in the saturation region, where the drain current becomes largely independent of drain voltage.

#  First we take all  type of information Date

 # Equations
| Parameter         | Equation                   |
| ----------------- | -------------------------- |
| Drain Current     | ID = (1/2) μCox (W/L) Vov² |
| Transconductance  | gm = 2ID / Vov             |
| Output Resistance | ro = 1 / (λID)             |
| Voltage Gain      | Av = −gm × Rout            |

# All Parameters for NMOS and PMOS
Parameter	Value
| Parameter            | Value  |
| -------------------- | ------ |
| Technology Node      | 180 nm |
| Supply Voltage       | 1.5 V  |
| Target Drain Current | 200 µA |
| Overdrive Voltage    | 0.25 V |
| Channel Length       | 180 nm |

#  Values
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

# For NMOS  Process Transconductance

| Parameter  | Value     |
| ---------- | ----------|
| μnCox      | 236 µA/V² |

# Calculated Dimensions

| Device | Width (µm) | Length (µm) | W/L   |
| ------ | -----------| ------------| ------|
| NMOS   | 5          | 0.18        | 27.78 |

# For PMOS  Process Transconductance
| μpCox  | 100 µA/V² |

# Calculated Dimensions
| Device | Width (µm) | Length (µm) | W/L   |
|--------|------------|-------------|-------|
| PMOS   | 11.83      | 0.18        | 65.72 |


# Transistor Size Calculation

Using the MOSFET saturation equation:

ID = (1/2) μCox (W/L) Vov²


PMOS width is larger due to lower hole mobility.

# Circuit 2A – Source Degenerated Common Source Amplifier

For Design  a MOS amplifier that:

- Operates at 200 µA drain current

- Provides maximum symmetric output swing

DC Bias Design
| Parameter | Value   |
| --------- | ------- |
| ID        | 200 µA  |
| VTHn      | 0.36 V  |   = For NMOS
| VTHp      | −0.39 V |   = For PMOS
| VDD       | 1.5 V   |


# Drain Voltage Selection
For maximum output swing:

- VDS = VDD / 2   ,1.5/2

- VDS = 0.75 V

# Source Voltage

Chosen value:

- VS = 0.2 V

This improves bias stability.

# Output Voltage
- Vout = VDD/2+0.2 
- Vout = 1.5/2+0.2= 0.95

# Source Resistor   
 -  IDRD = VS = 0.2

- RS = IDRD / ID   0.2/200µA

- RS = 1 kΩ

# Gate Voltage

- VGS = VTH + Vov = 0.36=0.25

- VGS = 0.61 V

- VG = VGS + IDRD = 0.61+0.2

- VG = 0.81 V

# PMOS Gate Voltage

- VSG = Vov + |VTHp|

- VSG = 0.64 V

- VGp = VDD − VSG

- VGp = 0.86 V

# Saturation Verification
| Device | Condition | 
| ------ | --------- | 
| NMOS   | VDS ≥ Vov | 
| PMOS   | VSD ≥ Vov | 


Both transistors remain in saturation.

![Image](https://github.com/ullasnarahatti/Experiment-12/blob/fd089c678c43f0bb77d9d8059f67a78a3be9a1b2/DC%20op.png)

# Final Operating Point
| VS    | VDS    | Vout   | VG     | VGp    | ID     | RS   | Vov    |
| ----- | ------ | ------ | ------ | ------ | ------ | ---- | ------ |
| 0.2 V | 0.75 V | 0.95 V | 0.81 V | 0.86 V | 200 µA | 1 kΩ | 0.25 V |

# Width Optimization
Practical widths used in LTspice:

| Device | Width   |
| ------ | ------- |
| NMOS   | 15.2 µm |
| PMOS   | 37.5 µm |

Widths increas to get ID ≈ 200 µA 

# Transient Analysis
| Parameter | Value  |
| --------- | ------ |
| Frequency | 1 kHz  |
| Amplitude | 10 mV  |
| DC Bias   | 0.81 V |

LTspice input source:
- Vin = SINE(0.81 10m 1k)
  
# Input Waveform
# Output Waveform
![Image](https://github.com/ullasnarahatti/Experiment-12/blob/fea78624b45158a632674a14a3320a57fcb70bd8/Transint%20analysis.png)

# Input and Output Comparison
images/input_output.png
# Practical Gain Calculation
| Measurement | Value     |
| ----------- | --------- |
| Vin(p-p)    | 19.6 mV  |
| Vout(p-p)   | 186 mV |


Voltage gain:

- Av = Vout / Vin

- Av ≈ 9.487

- Gain in dB:

- Gain = 19.5 dB

# AC Frequency Response
| Parameter    | Value     |
| ------------ | --------- |
| Midband Gain | 19.487 dB |
| −3 dB Gain   | 16.487 dB |
| Bandwidth    | 233.8 MHz |

![Image](https://github.com/ullasnarahatti/Experiment-12/blob/8bc53798959670725f77b90df2811ab7c9ebf82a/AC%20Analysis.png)

# experiment 2b

# Cascode MOSFET Amplifier with Active Load -- LTspice Study

## Overview

This document describes the simulation and analysis of a **cascode
MOSFET amplifier** that uses an **active load**.\
The circuit is implemented and tested using LTspice. The cascode
structure is commonly used in analog IC design because it improves
output resistance and reduces the Miller capacitance effect. These
improvements allow the amplifier to achieve better gain and wider
bandwidth compared with a simple common‑source stage.

![Circuit](https://github.com/ullasnarahatti/Experiment-12/blob/b85fac1bec67d38e79eec47292ea06f485421eff/exp4/2%20design.png)

------------------------------------------------------------------------

## DC Design Parameters

The initial conditions used for biasing the amplifier are shown below.

  Parameter                Selected Value
  ------------------------ ----------------
  Supply Voltage (VDD)     1.5 V
  Target Drain Current     200 µA
  NMOS Threshold Voltage   0.36 V
  PMOS Threshold Voltage   −0.39 V

These parameters are chosen so that each transistor can operate in the
saturation region.

------------------------------------------------------------------------

## Bias Conditions

For proper analog amplification, MOS transistors must remain in
saturation.\
The following limits are considered during the design.

  Quantity   Minimum    Maximum   Reason
  ---------- ---------- --------- ----------------------------
  NMOS VGS   ≥ 0.36 V   ≤ 1.5 V   Enables channel conduction
  NMOS VDS   ≥ VOV      ≤ VDD     Keeps NMOS in saturation
  PMOS VSG   ≥ 0.39 V   ≤ VDD     Allows PMOS current flow
  PMOS VSD   ≥ VOV      ≤ VDD     Ensures saturation region

------------------------------------------------------------------------

## Overdrive Voltage

The overdrive voltage determines the effective gate drive applied to the
transistor.

VGS = VTH + VOV

Using the selected values:

VGS = 0.36 + 0.25 = **0.61 V**

Therefore,

VOV = VGS − VTH = **0.25 V**

To maintain proper operation, the drain voltage is chosen near half of
the supply voltage:

VDS ≈ VDD / 2 ≈ **0.75 V**

The selected overdrive voltage satisfies the condition:

0 \< VOV \< 0.75 V

This value provides a good balance between transistor gain and voltage
headroom.

------------------------------------------------------------------------

## Intermediate Node Voltage

In a cascode arrangement, the drain of the lower NMOS is connected to
the source of the upper NMOS.

To ensure the lower transistor remains in saturation:

VDS ≥ VOV

Since its source is grounded,

VS2 = 0

Thus,

VDS2 = VS1

This leads to:

VS1 ≥ 0.25 V

The chosen value is

VS1 ≈ **0.3 V**

------------------------------------------------------------------------

## Output Voltage Level

To allow a symmetrical signal swing, the output node is positioned near
the center of the available voltage range.

VDS ≈ VDD / 2 ≈ **0.75 V**

Therefore,

Vout = VDS + VS1

Vout = 0.75 + 0.3 = **1.15 V**

------------------------------------------------------------------------

## Saturation Verification

The operating point of each transistor is checked to confirm saturation.

  Transistor        Requirement   Check
  ----------------- ------------- ------------
  M2 (Lower NMOS)   VDS ≥ VOV     0.3 ≥ 0.25
  M1 (Upper NMOS)   VDS ≥ VOV     0.9 ≥ 0.25
  M3 (PMOS Load)    VSD ≥ VOV     0.6 ≥ 0.25

All transistors operate correctly in the saturation region.

------------------------------------------------------------------------

## DC Operating Point

The node voltages obtained from the LTspice operating point simulation
are:

  Node                Voltage
  ------------------- ---------
-   VS2                 0 V
-   VS1                 0.3 V
 -  Vout                1.05 V
-   Drain Current       200 µA
 -  Overdrive Voltage   0.25 V

![Operating
Point](https://github.com/ullasnarahatti/Experiment-12/blob/f8ce53c9928016d073d60af4f37ce6300611ae68/DC12.png)

------------------------------------------------------------------------

## Transistor Dimension Selection

The transistor widths are initially estimated using the MOSFET
square‑law equation so that the drain current is approximately 200 µA.

 | Device              |Estimated Width  |  Final Width   |
 | --------------------| ----------------| -------------  |
 | - M1 (NMOS Cascode)  | 5 µm            |  16 µm         |
 |- M2 (NMOS Input)    | 5 µm            | 16 µm          |
 |- M3 (PMOS Load)     | 11 µm           |38 µm          | |

After simulation, small adjustments were made to account for practical
effects such as channel length modulation and mobility variations.

------------------------------------------------------------------------

## Transient Simulation

### Input Signal

  Parameter     Value
  ------------- ------------
  Signal Type   Sinusoidal
  Frequency     1 kHz
  Amplitude     10 mV
  DC Offset     0.916 V

Simulation command:

.tran 0 5m

------------------------------------------------------------------------

### Input Waveform

![Input](https://github.com/ullasnarahatti/Experiment-12/blob/04e1485e19d12692b73178512fcf37cebbe10bd3/experimenet3/4experiment/ip12.png)

------------------------------------------------------------------------

### Output Waveform

![Output](https://github.com/ullasnarahatti/Experiment-12/blob/04e1485e19d12692b73178512fcf37cebbe10bd3/experimenet3/4experiment/op12.png)

------------------------------------------------------------------------

### Comparison of Input and Output

![Comparison](https://github.com/ullasnarahatti/Experiment-12/blob/40ed3591c3ef304226802ff11a2ba8cca8dc4f24/experimenet3/4experiment/ipop.png)

------------------------------------------------------------------------

## Voltage Gain

The voltage gain of the amplifier is determined from the measured input
and output values.

Av = Vout / Vin

From the waveform data:

Av = (1.072 − 1.039) / (0.9195 − 0.9005)

Av ≈ **1.77**

Gain expressed in decibels:

Gain(dB) = 20 log10(Av)

Gain ≈ **4.95 dB**

------------------------------------------------------------------------

## AC Frequency Response

AC analysis is performed to study the gain variation with frequency and
to estimate the bandwidth.

Simulation directive:

.ac dec 1000 0.1 1G

The AC source magnitude is set to **1 V**.

![AC
Gain](https://github.com/ullasnarahatti/Experiment-12/blob/04e1485e19d12692b73178512fcf37cebbe10bd3/experimenet3/4experiment/ac123.png)

------------------------------------------------------------------------

## Performance Summary

  Parameter         Result
  ----------------- -----------
 -  Midband Gain      ≈ 4.645 dB
 -  Calculated Gain   ≈ 4.95 dB
 -  −3 dB Frequency   276.8 MHz

------------------------------------------------------------------------

## Final Remarks

The cascode amplifier with an active load was successfully implemented
in LTspice.\
The circuit maintains a stable bias current near **200 µA** and
demonstrates a gain of about **4.8 dB**. In addition, the amplifier
provides a large bandwidth close to **276.8 MHz**.

Because the cascode configuration increases output resistance and
reduces capacitance effects, it offers improved performance compared
with a standard common‑source amplifier stage.
