# LIC Lab experiments Repository

# USN : 4NI24EC140

This repository contains weekly lab experiments.

# CS_Amplifier_EXPERIMENT_01_&_02(a,b,c)

## This file contains the Experiment 1 & 2 for CS Amplifier files.

MOSFETs,is short term for Metal Oxide Semiconductor Field Effect Transistors, are extremely important in our everyday lives due to their unique features, beneficial characteristics, and wide range of applications. A MOSFET can function both as a switch and as an amplifier, which are its two main uses. Based on how they are connected in a circuit, MOSFETs are available in different configurations, such as:

1.Common Source Amplifier (CS)

2.Common Gate Amplifier   (CG)

3.Common Drain Amplifier  (CD)

Out of which Common Source Amplifier has an advantage as offers a high voltage gain, good input impedance, and a relatively low output impedance compared to Common Gate and Common  Drain .

The below is the general representation of a CS Amplifier.

![Image](https://github.com/user-attachments/assets/b4af6e83-4f0e-43cd-bf48-05dd4049256e)

We can see that the circuit uses an NMOS (N-channel MOSFET), where the gate terminal is connected to the input voltage. For a conducting channel to be formed and for current to flow through the drain, the applied input voltage Vin 	must be greater than the threshold voltage.

In order to supply power for the circuit , a DC Power supply has been provided at the drain terminal. The Source terminal is connected to the ground.

The drain current flows from supply to the source.Here the applied input is a voltage and we are interested to find the Output Voltage which is been amplified.

Since a MOSFET is a voltage-controlled current device, its output appears in the form of drain current. To obtain a voltage output from this current, Ohm’s law can be applied, where 
V = I*R. Therefore, placing a resistor at the drain terminal converts the drain current into a corresponding voltage.

Thus from the Output curves we know that the amplifier works in Saturation Region of MOSFET

![Image](https://github.com/user-attachments/assets/355e4f53-38ff-442c-b070-0b76902e7f58)

The Q-point (quiescent point) of a MOSFET is established to keep the device operating in its optimal region. This ensures proper amplification with minimal distortion, maintains a stable DC operating condition, and allows the maximum possible signal swing without causing clipping or pushing the device into non-linear operation.

![Image](https://github.com/user-attachments/assets/0bafae23-8bdc-4ad5-834f-42f12564553e)

The input DC Voltage can also be set using the Voltage divider bias rule at the gate terminal.

Capacitors behave as an AC short circuit and a DC open circuit. In simple terms, they allow the AC component to pass through while blocking the DC component. However, the impedance of a capacitor also plays an important role and must be considered when analyzing the system’s response at different frequencies.

![Image](https://github.com/user-attachments/assets/484075a9-8943-4d6b-8196-0f02e17bedb7)

The below is the Voltage Transfer Curve ( Vds VS Vgs ) for a MOSFET.

![Image](https://github.com/user-attachments/assets/c12fe0eb-9a8f-4560-8c02-c3bfd965241b)

Its observed that when Vgs < Vth, the MOSFET is OFF , as a result Vds = Vdd. However When Vgs > Vth the MOSFET is ON , and if Vds >= Vov it works in Saturation Region (as required). Also if Vds < Vov the MOSFET works in Triode Region.

Now, why is the saturation region required? From the characteristic curve, we can observe that the graph becomes nearly linear in this region. When the input signal is applied within this region, the MOSFET provides maximum amplification, resulting in higher gain. Therefore, this near-linear region is very important while setting the Q-point.

An 180 deg phase shift is observed at the output. We observe that :

![Image](https://github.com/user-attachments/assets/fc3c815f-4119-42ac-bc6d-d4a869e4f8e5)

And as a result in the input voltage increases the drain current (Id) increases, as a result the Id*Rd term increases. So the Vds value decreases with increase in Vgs . Thus its inverting.

It is also important to note that the input AC signal applied to the MOSFET must satisfy the condition vgs≪2vov for proper amplifier operation. If the positive peak of the input signal increases beyond this limit, the negative half-cycle shifts the MOSFET into the triode region, resulting in distortion. Similarly, if the negative peak increases excessively, the positive half-cycle drives the MOSFET into the cutoff region, causing signal clipping.

By carefully selecting and calculating all the circuit parameters and applying an AC input signal, it is possible to achieve a very high gain. However, such excessively high gain is usually not desirable. To reduce and stabilize the gain to a practical level, a source resistor is introduced, which provides source degeneration and results in a steady and stable gain. Additionally, using a bypass capacitor increases the gain by allowing the unwanted AC component to bypass the source resistance.

A complete model looks something like this:

![Image](https://github.com/user-attachments/assets/1a555326-9883-4c21-87b3-d5b4f75c2e7b)

Now coming to the frequency response of the CS Amplifier,

![Image](https://github.com/user-attachments/assets/88a55736-efac-4362-9d47-7f62ad536e44)

It is observed that capacitive impedances significantly affect the circuit at lower frequencies, while the internal capacitances of the MOSFET become dominant at higher frequencies. As a result, the frequency range between the lower cutoff frequency and the upper cutoff frequency, known as the midband region, is the range in which capacitive effects are negligible for the common-source amplifier. In this region, all capacitors effectively behave as AC short circuits.

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 
# Q1) To Design CS amplifier using n mosfet in the tsmc 180nm tech.lib in lt spice use VDD=1.8V , P<=1mW , C(load)=10pF , Ln=560nm 

CIRCUIT DIAGRAM: 



![Image description](https://github.com/shreekar-rt/lic/blob/main/Screenshot%202026-02-22%20151907.png)

CALCULATION :

Power = Voltage * Current

Current = Power / Voltage = 1m / 1.8 = 555.55 uA = (ID)

so according to the constraint given regarding power the current should be less than 555.55uA 
so let us consider current (ID) = 400uA which is less than 555.55uA

Since its an Amplifier to make sure that its present in Saturation Region.

Here we observe Vt = 0.366V (given) , Also (Vgs - Vt )= Vov = (Vgs-0.366) < Vds
as Vds= Vdd/2 = 1.8/2 = 0.9V and that implies Vgs < 0.9V + 0.366V
Vgs < 1.266V.
so according to above equation consider Vgs = 0.9V which is also half of Vdd
Thus by fundamental concept , Vds >= Vov , here 0.9V > 0.534V . Its in SATURATION .
as we are provided with the ' W ' value we have to find it now by formula 

ID = (Un Cox W (Vgs-Vt)^2) / 2 Ln

as we also not provided with the value of Cox 
finding it by formula 

Cox = (epslon0 * epslon r ) / tox
we know tox and epslon0 and epslon r by substituting we get 
Cox = 8.638 m F/m^2
Un value is provided as 273.8094*10^-4 m^2
Ln is provided as 560 n m 
by substituting all the given and obtained value we get

W = 6.6755 U m 

DRAIN RESISTANCE CALCULATION (RD) :
RD = Vdd-Vds / ID = (1.8 - 0.9) / 400 UA 
RD = 2.250k ohm


# DC ANALYSIS OPERATING POINT

for W = 6.675Um we got Id as 297 UA and Vout as 0.899V 
as we know varying W we can obtain our desired Vout
so we varied W from 6.675 Um to 9.087 Um we obtained our desired Vout  that is 0.90005V

DC ANALYSIS SIMULATOR IMAGE

![Image description](https://github.com/shreekar-rt/lic/blob/main/Screenshot%202026-02-22%20152111.png)

The above data providing the DC biasing which is required as mentioned earlier to make sure the value of current
matches with power budget and the device is working well in saturation for proper Amplification.

# TRANSIENT ANALYSIS

![Image description](https://github.com/shreekar-rt/lic/blob/main/WhatsApp%20Image%202026-02-20%20at%208.58.21%20PM.jpeg)

for sine wave input we gave 
dc offset = 0.9V
frequency = 1k Hz
amplitude = 10mV 
" WE TOOK AMPLITUDE = 10mV WHICH IS EQUAL TO Vgs AS WE KNOW THAT 

" Vgs << 2 Vov "
OUR CALCULATED Vov = 534mV
2Vov = 1068mV
10m << 1068mV "

FROM THE GRAPH IN SIMULATION: 

Vin(p-p) = 909.633mV - 890.394 mV 
Vin(p-p) = 19.239mV

Vout(p-p) = 931.894mV - 867.896mV
Vout(p-p) = 63.997mV

OVERALL GAIN   Av  (SIMULATION )
Av = Vout(p-p) / Vin(p-p)
Av = 63.997m / 19.239 m
Av = 3.326

Av(dB) = 20log(Av)
Av(dB) = 10.438 dB

OVERALL GAIN Av (THEORITICAL)
Av = gm * RD
where gm = 1/Kn*(Vgs-Vt) = (2ID) / (Vgs-Vt)
gm = 1.4981m mho 
Av = 3.370
Av(dB) = 20log (Av) = 10.55 dB
gain of simulation and theriotical both are nearly equal 
10.438dB NEARLY EQUAL TO 10.55 dB 

# AC ANALYSIS 

simulator output 

![Image description](https://github.com/shreekar-rt/lic/blob/main/WhatsApp%20Image%202026-02-20%20at%208.58.20%20PM.jpeg)


Bandwidth = fH-fL
Bandwidth = 1.2966-0  GHz
3db frequency 1.2966 GHz
With Capacitor CL = 10 pF (given)
BW = 7.328 MHz - 0 7.328 MHz
3dB frequency = 7.328 mHz it is half power frequency 
0dB frequency = 23.29 MHz

(UGB) (unity gain bandwidth) 
UGB = 23.29 MHz
we know by the formula 
UGB = MIDBAND GAIN * f (3dB)

23.29 MHz is nearly equal to 24.37 MHz ...

RESULTS  :      


* DC ANALYSIS            
 Vout = 0.90005V           
 W = 9.087 UA

* TRANSIENT ANALYSIS                    
  simulator    Av(dB) = 10.438 dB         
  theriotical  Av(dB) = 10.550 dB
  
* AC ANALYSIS                                                            
  BW = 1.2966 GHz                                                                      
  UGB = 23.29 MHz                                                       
  Midband gain * f (3dB) = 24.37 MHz                                       
                                                                  

INFERENCE :

Here by fundamental principle , its observed to make the MOSFET work in Saturation region  in almost linear part to get maximum gain.
Hence the operating window should be chosen correctly and the Q point should set in such a way for the Vds, 
such that there will not be any distortion or clipped part of the output signal.

Hence a CS Amplifier of ,  , Ln = 560nm , Vdd = 1.8V  is designed and verified for power budget of P <= 1mW , CL = 10pF . 

We have also verified that P= V*I = 1.8 * 400 UA will provide the value of 0.72mW which is well within the budget of 1mW.

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# EXPERIMENT - 02

## Q2) Design amplifier configuration using tsmc018 tech lib in LT spice 





## a) AMPLIFIER WITH ACTIVE LOAD 

### calculation for nmos 

Given Design Parameters


Parameter	Value

Technology	TSMC 180 nm

Supply Voltage VDD	1.8 V

Power Constraint	≤ 1 mW

NMOS Channel Length	560 nm

PMOS Channel Length	560 nm

NMOS Threshold Voltage Vthn = 0.36 V

PMOS Threshold Voltage Vthp = 0.39

Overdrive Voltage Vov = 0.25 V

CIRCUIT DIAGRAM ;

![Image description](https://github.com/shreekar-rt/lic/blob/main/Screenshot%202026-03-09%20231200.png)

# calculation to find  required unknown parameters.

SOLVE FOR ID 

VDD*ID <= 1mW

1.8 * ID

ID<=555.55 UA

SO BY THIS CONSTRAINT WE CONSIDER ID = 400 UA

SOLVE FOR Vout

Vout = (VDD/2) + ID*Rs

Given that ID*Rs = 0.2 

Vout = 1.1V

SOLVE FOR Rs 

ID*Rs = 0.2

Rs = (0.2/400 UA ) = 500 ohm

SOLVE FOR VB1

VB1 = VGS1 + ID*Rs

Vov = 0.25 V where Vth = 0.36 V 

VB1 = (0.25 + 0.36 ) + 0.2

VB1 = 0.616 + 0.2

VB1 = 0.816 V

NOW WE CHECK THE CONDITON FOR SATURATION 

VDS >= Vov 

VDS >= VGS - VtH

0.9 >= 0.61 - 0.36

0.9 >= 0.25

VERIFIED THAT IT IS IN SATURATION REGION 


NOW LETS FIND THE WIDTH OF NMOS 


ID = (UnCox W (VGS - Vth)^2 ) / 2Ln

Un = 273.8094E-4 m^2

Cox = 8.638E-3 F/m^2

Ln = 560 nm 

ID = 400 UA

Vthn = 0.36 V

after substituting and solving we get 

W = 30.3 Um

### calculations for pmos



VB2 = Vov = 0.25  Vth = 0.39 V

Vov = VSG - |Vthp|

VSG = Vout + Vthp 

VSG = 0.25 + 0.39 

VSG = 0.64 V

VSG = VS - VG

0.64 = VDD - VG 

VG = VDD - 0.64 

VG = VB2 = 1.16 V

### now lets solve for width of pmos

ID = ( Un Cox W (VGS-Vth)^2 ) / 2 Ln

Up = 115.689E-4 m^2

Cox = 8.422E-3 F/m^2

Lp = 560 nm

ID = 400 UA

Vthp = 0.39 V

after substituting all values 

we get W = 73.56 Um

# DC ANALYSIS 

![Image description](https://github.com/shreekar-rt/lic/blob/main/Screenshot%202026-02-22%20152111.png)

while finding DC operating point we got 

NMOS width as 30.3 Um and for desired operating point and desired ID value we changed it to 54 Um


 and we got PMOS widgh as 73.56 Um  and for desired operating point and desired ID value we changed it to 165.255 Um 

by these changes we achieved Vout nearly equal to  1.1
and ID is nearly equal to 400 UA

# TRANSIENT ANALYSIS

ACCORDING TO SIMULATOR

![Image description](https://github.com/shreekar-rt/lic/blob/main/Screenshot%202026-03-10%20225833.png)

Vout(p-p) ->>>>> 1.3752 - 0.840 

Vout(p-p) = 0.5314 V

![Image description](https://github.com/shreekar-rt/lic/blob/main/Screenshot%202026-03-10%20225435.png)

Vin(p-p) ->>>>> ( 825.926 - 806.194 ) mV

Vin(p-p) = 19.768 mV = 0.0197 V

## lets find the simulated gain 



Av =  Vout(p-p) / Vin(p-p) 

Av = 0.5314 m / 0.0197 m 

Av = 26.8818 V/V

## gain in dB 

AvdB = 20log(26.8818)

AvdB = 28.58

# AC  ANALYSIS 

## WITHOUT LOAD 

### simulator frequency response

![Image description](https://github.com/shreekar-rt/lic/blob/main/Screenshot%202026-02-26%20161249.png)

![Image description](https://github.com/shreekar-rt/lic/blob/main/Screenshot%202026-02-26%20161518.png)

according to the simulated value we got 

0 dB frequency as 1.713 gHz  ( without load )

and 3dB frequency as 52.5290 MHz ( without load )

simulated gain  AvdB  = 28.762 dB 

UGB = midbandgain * freq(3dB)

UGB = 26.88 * 52.52 M 

UGB = 1.411 GHz 

## VERIFIED  (WITHOUT LOAD )

UGB IS NEARLY EQUAL TO 0 db frequency

UGB = 1.411 GHz which is nearly equal to 0 dB = 1.713 GHz

## WITH LOAD 

![Image description](https://github.com/shreekar-rt/lic/blob/main/Screenshot%202026-02-26%20161954.png)

![Image description](https://github.com/shreekar-rt/lic/blob/main/Screenshot%202026-02-26%20162227.png)

according to the simulated value we got 

0 dB frequency as 21.216 MHz  ( with load )

and 3dB frequency as 772.338 KHz ( with load )

simulated gain  AvdB  = 28.690 dB 

UGB = midbandgain * freq(3dB)

UGB = 26.881 * 772.338 KHz

UGB = 20.7 MHz

## VERIFIED  (WITH LOAD)

UGB IS NEARLY EQUAL TO 0 db frequency

UGB = 20.7 MHz which is nearly equal to 0 dB = 21.216 MHz

## RESULT


* DC ANALYSIS
  
   ID = 400 UA

   Vout = 1.110 V
 
   (NMOS) W = 54.0 Um

   (PMOS) W = 165.255 Um

* TRANSIENT ANALYSIS
                     
   simulator    Av(dB) = 28.5818 dB
         
* AC ANALYSIS

   WITHOUT LOAD
  
   0 dB = BW = 1.713 GHz
        
   UGB = 1.411GHz 

   WITH LOAD 

   0 dB = BW = 21.216 MHz

   UGB = 20.7 MHz
 
 ## INFERENCE

The common source amplifier with active load was successfully designed using the TSMC 180nm technology library in LTspice while satisfying the power constraint of ≤1 mW. DC analysis confirmed the desired operating point with ID ≈ 400 UA and Vout ≈ 1.1V, ensuring the MOSFET operates in the saturation region. Transient analysis showed a voltage gain of approximately 26.88 V/V (≈28.58 dB) AC analysis verified the frequency response, where the unity gain bandwidth was close to the 0 dB frequency, confirming correct amplifier behavior. Thus, the designed amplifier achieves the expected gain and bandwidth characteristics under the given design constraints.

 


## b) AMPLIFIER WITH ACTIVE LOAD AND CURRENT SOURCE


Given Design Parameters


Parameter	Value

Technology	TSMC 180 nm

Supply Voltage VDD	1.8 V

Power Constraint	≤ 1 mW

NMOS Channel Length	560 nm

PMOS Channel Length	560 nm

NMOS Threshold Voltage Vthn = 0.36 V

PMOS Threshold Voltage Vthp = 0.39

CIRCUIT DIAGRAM ;

![Image description](https://github.com/shreekar-rt/lic/blob/main/Screenshot%202026-03-14%20232621.png)

# calculation to find  required unknown parameters.

SOLVE FOR ID 

VDD*ID <= 1mW

1.8 * ID

ID<=555.55 UA

SO BY THIS CONSTRAINT WE CONSIDER ID = 400 UA

VDD = 1.8 V

## DC analysis


![Image description](https://github.com/shreekar-rt/lic/blob/main/Screenshot%202026-03-14%20235440.png)

P ≤ 1 mW

ID ≤ (1 × 10^-3) / VDD = 555.5 µA

Considering ID = 400 µA

Let us write equations for overdrive voltage

Vov1 = VGS1 − VTN

Vov3 = VGS3 − VTN

Vov2 = VSG2 − |VTP|

Consider the overdrive voltage to be the same so as to maintain symmetry.

Now satisfying the saturation condition to find optimum Vov, Vout and Vin.

## For M3 MOSFET

VDS3 ≥ Vov

Vx ≥ Vov

So,

Vx(min) = Vov

## From M1 MOSFET

VDS1 ≥ Vov

Vout − VDS3 ≥ Vov

Vout ≥ Vov + Vx

## From M2 MOSFET

VSD2 ≥ Vov

VDD − Vout ≥ Vov

VDD − Vov ≥ Vout

If Vov = Vx(min)

Vout(min) = Vov + Vov = 2Vov (from M1)

Vout(max) = VDD − Vov (from M2)

## Output range

2Vov ≤ Vout ≤ VDD − Vov

So, optimum output voltage

Vout = (VDD + Vov) / 2

Vout = VDD/2 + Vov/2


## Here swing range is

Vswing = VDD − 3Vov

For max swing → Vov to be very less

So,

VDD − 3Vov ≥ 0

Vpp = Vovmax

Vovmax = 1.8 / 3 = 0.6 V

Minimum overdrive voltage is (Vov = 0)

Then optimum overdrive voltage is

Vov = 0.6 / 2 = 0.3 V

## For NMOS

VGSmin = 0.366 V

VGSmax = 0.366 + 0.6 = 0.966 V

VGS = 0.666 V

## For PMOS

VSGmin = 0.39 V

VSGmax = 0.39 + 0.6 = 0.99 V

VSG = 0.69 V

So, for M1

Vin = VGS + Vx = 0.3 + 0.666 = 0.966 V

## For M3

Vb2 = VGS = 0.666 V

## For M2

Vb1 = 1.8 − 0.69 = 1.11 V

Voutmin = 2Vov = 0.6 V

Voutmax = 1.8 − 0.3 = 1.5 V

Output voltage swing = 0.9 Vpp

Vout = (VDD / 2) + (Vov / 2)

Vout = 0.9 + 0.15 = 1.05 V

Transient analysis


![Image description](https://github.com/shreekar-rt/lic/blob/main/Screenshot%202026-03-15%20000725.png)

Output voltage
Vout max = 1.080 V
Vout min = 1.021 V

Input voltage
Vin max = 975.56 mV
Vin min = 956.42 mV

Av = Vout / Vin
Av = (1.080 − 1.021) V / (975.56 − 956.42) mV

= 59 / 19.14

Av = 3.08 V/V

Av(dB) = 9.77 dB

AC analysis

![Image description](https://github.com/shreekar-rt/lic/blob/main/Screenshot%202026-03-15%20001149.png)

Midband gain Av(dB) = 9.73 dB
Av = 3.07 V/V

3 dB Bandwidth = 54.978 MHz

Midband gain = 3.08 V/V

Unity gain bandwidth = 162.467 MHz

Verification

UGB = 3 dB Bandwidth × Midband gain

UGB ≈ 54.978 MHz × 3.08 V/V

UGB ≈ 169.33 MHz

## RESULT

DC Analysis Result

The DC operating point of the CS amplifier with active load was successfully established with
Vov = 0.3 V and Vout ≈ 1.05 V.
The output voltage range obtained was 0.6 V to 1.5 V, ensuring all MOSFETs operate in the saturation region.

Transient Analysis Result

The voltage gain obtained from transient analysis was Av ≈ 3.08 V/V (9.77 dB), confirming proper amplification of the input signal.

AC Analysis Result

From AC analysis, the amplifier achieved a midband gain of approximately 3.07 V/V (9.73 dB) with a 3 dB bandwidth of about 54.978 MHz and unity gain bandwidth of approximately 162.467 MHz.

## INFERENCE

From this experiment, the Common Source (CS) amplifier with active load and current source was successfully designed and analyzed using DC, transient, and AC analyses. The DC analysis ensured proper biasing of all MOSFETs in the saturation region with an optimum output operating point around 1.05 V and an output swing between 0.6 V and 1.5 V. Transient analysis confirmed that the circuit provides voltage amplification with a gain of approximately 3.08 V/V (≈9.77 dB). AC analysis showed that the amplifier achieves a midband gain of about 3.07 V/V with a 3 dB bandwidth of approximately 54.98 MHz and a unity gain bandwidth of about 162 MHz. Thus, the CS amplifier with active load provides proper biasing, stable operation, and effective signal amplification with a reasonable bandwidth.

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# c) CS Amplifier with Active Load and Diode Connected MOSFET

## Given Design Parameters


Parameter	Value

Technology	TSMC 180 nm

Supply Voltage VDD	1.8 V

Power Constraint	≤ 1 mW

NMOS Channel Length	560 nm

PMOS Channel Length	560 nm

NMOS Threshold Voltage Vthn = 0.36 V

PMOS Threshold Voltage Vthp = 0.39

## CIRCUIT DIAGRAM ;

![Image description](https://github.com/shreekar-rt/lic/blob/main/Screenshot%202026-03-15%20234829.png)

## Calculations

VDD = 1.8 V

P ≤ 1 mW

ID ≤ (1 × 10⁻³) / VDD
ID ≤ (1 × 10⁻³) / 1.8
ID = 555.55 µA

Considering ID = 400 µA

Let us write equations for overdrive voltage

VOV1 = VGS1 − VTHN
VOV3 = VGS3 − VTHN
VOV2 = VSG2 − |VTP|

Considering VOV to be same for the sake of symmetry and satisfying the saturation condition to find optimum VOV, Vout and Vin.

# DC Analysis 

![Image description](https://github.com/shreekar-rt/lic/blob/main/Screenshot%202026-03-15%20214707.png)


## For M3 MOSFET

VDS3 ≥ VOV
VDS3(min) = VOV

So,

Vx(min) = VDS3(min) = VOV

For M1 MOSFET

VDS1 ≥ VOV
Vout − VDS3 ≥ VOV
Vout ≥ VOV + VDS3
Vout ≥ VOV + Vx

## For M2 MOSFET

VSD2 ≥ VOV
VDD − Vout ≥ VOV
VDD − VOV ≥ Vout

If Vx = VOV

Vout(min) = VOV + VOV
Vout(min) = 2VOV

Vout(max) = VDD − VOV

Output range

2VOV ≤ Vout ≤ VDD − VOV

Optimum output voltage

Vout = (VDD + VOV) / 2

Maximum swing range

Vswing = VDD − 3VOV

For maximum swing VOV should be less

VDD − 3VOV ≥ 0

VOV(max) = VDD / 3
VOV(max) = 1.8 / 3 = 0.6 V

Minimum VOV voltage is (VOV = 0)

Optimal voltage

VOV = 0.6 / 2
VOV = 0.3 V

## For NMOS

VGS(min) = 0.366 V
VGS(max) = 0.366 + 0.6 = 0.966 V
VGS = 0.666 V

## For PMOS

VSG(min) = 0.39 V
VSG(max) = 0.39 + 0.6 = 0.99 V
VSG = 0.69 V

So, for M1

Vin = VGS + Vx
Vin = 0.3 + 0.666
Vin = 0.966 V

## For M3

VGS3 = VDS3 = Vx = 0.3 V

## For M2

VB1 = VDD − VSG
VB1 = 1.8 − 0.69 = 1.11 V

Vout(min) = 2VOV = 0.6 V

Vout(max) = VDD − VOV = 1.5 V

Vout(pp) = 0.9 Vpp

At Vout = 1.05 V

Vout = VDD / 2 + Vx / 2
Vout = 0.9 + 0.15
Vout = 1.05 V

## Width

For NMOS = 430.2 µm
For PMOS = 108.59 µm

# Transient analysis

![Image description](https://github.com/shreekar-rt/lic/blob/main/Screenshot%202026-03-15%20214833.png)

![Image description](https://github.com/shreekar-rt/lic/blob/main/Screenshot%202026-03-15%20214957.png)

## Output Voltage

Vout(max) = 1522.29 mV
Vout(min) = 592.70 mV

## Input Voltage

Vin(max) = 975.99 mV
Vin(min) = 956.02 mV

## Voltage Gain

Av = Vout(pp) / Vin(pp)
Av = 929.59 / 19.97
Av = 46.54 V/V

Av(dB) = 20 log(46.54)
Av(dB) = 33.56 dB

# AC Analysis

![Image description](https://github.com/shreekar-rt/lic/blob/main/Screenshot%202026-03-15%20215305.png)

With capacitor = 10 pF

Midband gain = 35.69 dB = 60.88 V/V

3 dB frequency (Bandwidth) = 1.00 MHz

Unity gain bandwidth = 61.17 MHz

## Verification

UGB = Midband gain × 3 dB frequency

UGB = 60.88 × 1.00 MHz

UGB ≈ 60.88 MHz

# RESULT

## DC Analysis

The DC biasing of the CS amplifier with active load and diode connected MOSFET was successfully calculated. The optimum overdrive voltage was chosen as Vov = 0.3 V for proper saturation operation. The bias voltages obtained are Vin = 0.966 V, VB1 = 1.11 V, and Vx = 0.3 V. The output voltage range was found to be 0.6 V ≤ Vout ≤ 1.5 V, with the optimum output voltage Vout ≈ 1.05 V for maximum symmetrical swing. The transistor widths were designed as Wn = 430.2 µm for NMOS and Wp = 108.59 µm for PMOS.

## Transient Analysis

From transient simulation, the output voltage varied between 1522.29 mV and 592.70 mV, giving a peak-to-peak output voltage of 929.59 mV. The input voltage varied between 975.99 mV and 956.02 mV, resulting in Vin(pp) ≈ 19.97 mV. The voltage gain of the amplifier was calculated as Av = 46.54 V/V, which corresponds to 33.56 dB.

## AC Analysis

From AC analysis with a 10 pF capacitor, the midband gain of the amplifier was found to be 35.69 dB (≈ 60.88 V/V). The 3-dB bandwidth was 1.00 MHz, and the unity gain bandwidth (UGB) was approximately 61.17 MHz. The theoretical verification also satisfies UGB ≈ midband gain × bandwidth, which gives approximately 60.88 MHz, confirming the simulation results.


## INFERENCE

The CS amplifier with active load and diode-connected MOSFET was successfully designed and analyzed. From the DC analysis, proper biasing conditions were achieved to ensure that all MOSFETs operate in the saturation region, providing the required output swing. The transient analysis confirmed that the amplifier produces a stable amplified output signal with a voltage gain of about 46.54 V/V (33.56 dB). The AC analysis showed a midband gain of 35.69 dB, a bandwidth of 1 MHz, and a unity gain bandwidth of approximately 61 MHz. Hence, the simulation results verify the theoretical design, demonstrating that the CS amplifier with active load provides good voltage gain and frequency response suitable for amplification applications.

















