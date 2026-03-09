# LIC Lab experiments Repository
# USN : 4NI24EC140
This repository contains weekly lab experiments.
# Expt_1_CS_Amplifier_
This file contains the Experiment 1 CS Amplifier files.

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

# AIM  
To Design CS amplifier using n mosfet in the tsmc 180nm tech.lib in lt spice use VDD=1.8V , P<=1mW , C(load)=10pF , Ln=560nm 

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



# EXPERIMENT - 02

# Q2) Design amplifier configuration using tsmc018 tech lib in LT spice 
# a) Amplifier with active load 


