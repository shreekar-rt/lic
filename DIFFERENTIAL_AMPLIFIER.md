# USN  4NI24EC140

# EXPERIMENT - 04 

# DIFFERENTIAL AMPLIFIER CIRCUIT 1 
## Aim

To design and simulate three MOSFET differential amplifier configurations using LTspice by performing DC, Transient, and AC analyses, and to compare their performance based on gain, bandwidth, and power efficiency.

## INTRODUCTION

A differential amplifier is an electronic circuit that amplifies the difference between two input signals while rejecting any common signal present at both inputs. It is one of the most fundamental building blocks in analog circuit design and is widely used in operational amplifiers, comparators, and communication systems.

The key advantage of a differential amplifier is its ability to eliminate noise and interference that appear equally on both input terminals, known as common-mode signals. This makes it highly suitable for applications requiring high precision and noise immunity.

In MOSFET-based differential amplifiers, transistors are operated in the saturation region to achieve proper amplification. The circuit typically consists of a pair of matched transistors with a constant current source, ensuring stable operation and balanced signal amplification.

## THEORY

A basic differential amplifier consists of two identical transistors (BJT or MOSFET) whose sources (or emitters) are connected together and biased using a constant current source known as the tail current (I_SS). The inputs are applied to the gates (or bases), and the output is taken from the drains (or collectors).

When equal input voltages are applied, the current splits equally between the two transistors, resulting in equal output voltages. When a differential input is applied, the current distribution changes, causing one transistor to conduct more while the other conducts less. This leads to a difference in output voltages, thereby amplifying the input difference.

The performance of a differential amplifier is characterized by parameters such as differential gain, common-mode gain, and Common Mode Rejection Ratio (CMRR). A high CMRR indicates better rejection of unwanted noise signals.

For proper operation, the transistors must remain in the saturation region, which ensures linear amplification. The biasing conditions, including tail current, load resistance, and transistor dimensions, play a crucial role in determining the gain and operating point of the amplifier.

![Image description](https://github.com/shreekar-rt/lic/blob/main/The-Basic-MOSFET-Differential-Pair-(1).jpg)

# Circuit 1: Differential Amplifier with Resistive Load

## CIRCUIT DIAGRAM

![Image description](https://github.com/shreekar-rt/lic/blob/main/Screenshot%202026-03-27%20175618.png)


## GIVEN PARAMETERS
Technology: TSMC 180nm
Supply voltage, 
VDD = +0.9V Negative supply, VSS = −0.9V
Power constraint, 
P ≤ 2.2 m W
Channel length, 
Ln = 540nm
Input common-mode voltage, 
Vin,CM=0V
Output common-mode voltage, 
VO,CM=0V
Tail node voltage, 
Vp = − 0.7 V
Load capacitance, L = 10p F
Threshold voltage, VT ≈ 0.36V

 ## Power Constraint

The total power consumed by the differential amplifier is given by:

P = (V_DD − V_SS) · I_SS

Total supply voltage:

V_DD − V_SS = 0.9 − (−0.9) = 1.8 V

Since the maximum allowed power is 1.8 mW,

P ≤ 1.8 × 10^−3

(V_DD − V_SS) · I_SS ≤ 1.8 × 10^−3

1.8 · I_SS ≤ 2.2 × 10^−3

I_SS ≤ 1.222 mA

To fully utilize the available power budget, we choose:

I_SS = 1.222 mA

Power dissipated:

P = 1.8 × 1.222 mA = 2.2 mW

Since 2.2 mW ≤ 2.2 mW, the power constraint is satisfied.


## Drain Current Calculation

In a balanced differential amplifier, the tail current splits equally between both transistors:

I_D1 = I_D2 = I_SS / 2

Substituting:

I_D1 = I_D2 = 1.222 mA / 2

I_D1 = I_D2 = 0.611 mA

## Load Resistance Calculation

Given:

V_OCM = 0 V

So,

V_out1 = V_out2 = 0 V

The output voltage is given by:

V_out = V_DD − I_D R_D

Substituting:

0 = 0.9 − I_D R_D

I_D R_D = 0.9

Solving for resistance:

R_D = 0.9 / I_D

Substituting:

R_D = 0.9 / (0.611 × 10^−3)

R_D =  1.472 kΩ

## Bias Point Calculation

Given:

V_in,CM = 0 V

So,

V_G1 = V_G2 = 0 V

Source Voltage

Given:

V_p = −0.7 V

Assuming:

V_S = V_p

V_S = −0.7 V

Gate-Source Voltage

V_GS = V_G − V_S

V_GS = 0 − (−0.7)

V_GS = 0.7 V

## Overdrive Voltage

Given:

V_T ≈ 0.36 V

V_OV = V_GS − V_T

V_OV = 0.7 − 0.36

V_OV = 0.34 V

## Drain Voltage

From previous calculation:

V_out1 = V_out2 = 0 V

## Drain-Source Voltage

V_DS = V_D − V_S

V_DS = 0 − (−0.7)

V_DS = 0.7 V

## Saturation Check

Condition:

V_DS > V_OV

0.7 > 0.34

Hence, both transistors operate in saturation.

Final Bias Point

V_G = 0 V

V_S = −0.7 V

V_D = 0 V

V_GS = 0.7 V

V_DS = 0.7 V

## Width Calculation

The drain current in saturation is given by:

I_D = (1/2) μ_n C_ox (W/L) (V_GS − V_T)^2

Rewriting:

I_D = (1/2) μ_n C_ox (W/L) (V_OV)^2

Rearranging to find width:

W = (2 I_D L) / (μ_n C_ox (V_OV)^2)

Substituting Values:

I_D = 0.6 mA = 0.6 × 10^−3 A

L = 540 nm = 540 × 10^−9 m

μ_n C_ox = 236.5 μA / V^2 = 2.365 × 10^−4 A / V^2

V_OV = 0.34 V

Calculation:

W = (2 × 0.6 × 10^−3 × 540 × 10^−9) / (2.365 × 10^−4 × (0.34)^2)

W = (540 × 10^−12) / (2.732 × 10^−5)

W = (540 / 2.732) × 10^(−12 + 5)

W ≈ 197.6 × 10^−7

W ≈ 1.976 × 10^−5 m

W ≈ 19.76 μm

The width obtained from first-order analysis is only an approximate estimate, as it assumes ideal conditions such as constant carrier mobility and perfect saturation behavior. In real MOSFET operation, various non-ideal effects like channel length modulation, mobility degradation, and variations in device parameters influence the actual operating point..

To strictly satisfy the given condition:

V_p = V_S = −0.7 V

The transistor width was optimized through simulation. By varying the width, the drain current was regulated so that the source node voltage accurately reached the desired value.

Final width obtained:

W ≈ 73 μm

Therefore, the difference from the theoretical width is due to non-ideal characteristics of the device and the requirement to achieve precise biasing conditions during simulation.

# DC Analysis

![Image description](https://github.com/shreekar-rt/lic/blob/main/Screenshot%202026-03-28%20163208.png)

## Input Common Mode Range (ICMR)

The input common-mode range is defined as the range of input voltage for which all transistors remain in saturation.

Minimum Input Common Mode Voltage

For proper operation, the tail current source must remain active and the NMOS transistors must stay in saturation.

Condition:
V_GS ≥ V_T

Using:
V_GS = V_ICM - V_S

So,
V_ICM(min) = V_S + V_T

Substituting values:
V_S = -0.7 V
V_T = 0.36 V

V_ICM(min) = -0.7 + 0.36

V_ICM(min) = -0.34 V

## Maximum Input Common Mode Voltage

For maximum input voltage, the NMOS transistors must remain in saturation.

Condition:
V_DS ≥ V_OV

Using:
V_D = 0 V
V_S = -0.7 V

V_DS = V_D - V_S = 0 - (-0.7) = 0.7 V

Now,
V_ICM(max) = V_D + V_T

Substituting:
V_ICM(max) = 0 + 0.36

V_ICM(max) = 0.36 V

Final Input Common Mode Range:
-0.34 V ≤ V_ICM ≤ 0.36 V

## Output Common Mode Range

The output common-mode voltage range is determined by ensuring that the NMOS transistors remain in saturation and the circuit operates properly.

Maximum Output Voltage

The maximum output voltage occurs when the drain voltage is at its highest possible value, which is limited by the supply voltage:

V_OCM(max) ≤ V_DD

However, to maintain current flow through the load resistor:

V_OCM(max) = V_DD

V_OCM(max) = 0.9 V

Minimum Output Voltage

For proper operation, the NMOS transistors must remain in saturation:

V_DS ≥ V_OV

Using:
V_DS = V_D - V_S

At the edge of saturation:
V_D - V_S = V_OV

So,
V_D = V_S + V_OV

Since:
V_D = V_OCM(min)

V_OCM(min) = V_S + V_OV

Substituting values:
V_S = -0.7 V
V_OV = 0.34 V

V_OCM(min) = -0.7 + 0.34

V_OCM(min) = -0.36 V

Final Output Common Mode Range:
-0.36 V ≤ V_OCM ≤ 0.9 V


## Differential Input Voltage Range (Linear Region)

The differential amplifier behaves linearly only when both transistors operate in saturation and the current is approximately equally shared between them.

For a MOS differential pair, linear operation is maintained when the differential input voltage is small compared to the overdrive voltage.

Condition for Linear Operation

|V_id| ≤ 2V_OV

Substituting Values:
V_OV = 0.34 V

|V_id| ≤ 2 × 0.34

|V_id| ≤ 0.68 V

Final Linear Range:
-0.68 V ≤ V_id ≤ 0.68 V

# TRANSIENT ANALSIS

Condition for Linearity

|V_id| < √2 V_OV

√2 V_OV = 1.414 × 0.34 = 0.48 V


## situation 1 : Linear Region

Input applied:
V_id = 10 mV < 0.48 V


![Image description](https://github.com/shreekar-rt/lic/blob/main/Screenshot%202026-03-28%20165531.png)

## Observation:

• The output signal appears sinusoidal in nature  
• No noticeable distortion is present  
• Both transistors remain in the saturation region  
• The amplifier operates in a linear manner  

## situation 2: Non-Linear Region

input applied ; V_id = 490m V

490 m V > 0.48 V

![Image description](https://github.com/shreekar-rt/lic/blob/main/Screenshot%202026-03-28%20171644.png)

Observation:

• The output waveform is no longer clean and shows distortion  
• Signal clipping can be clearly seen  
• One transistor turns OFF (enters cutoff region)  
• The amplifier deviates from linear operation  


