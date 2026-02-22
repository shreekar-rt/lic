# LIC Lab experiments Repository

This repository contains weekly lab experiments.
# Expt_1_CS_Amplifier_4NI24EC140
This file contains the Experiment 1 CS Amplifier files.

MOSFETs or Metal Oxide Semiconductor Field Effect Transistor plays an important role in our day to day life because of its advantages, characteristics and numerous applications.
It can be used as a "Switch" as well as an "Amplifier". These are the 2 primary applications of MOSFETS.
There are different configurations of MOSFETs being used namely 

1.Common Source Amplifier (CS)

2.Common Gate Amplifier   (CG)

3.Common Drain Amplifier  (CD)

Out of which Common Source Amplifier has an advantage as offers a high voltage gain, good input impedance, and a relatively low output impedance compared to Common Gate and Common  Drain .

The below is the general representation of a CS Amplifier.

![Image](https://github.com/user-attachments/assets/b4af6e83-4f0e-43cd-bf48-05dd4049256e)

We observe that it consists of an NMOS ( N Channel MOSFET ) , whose gate terminal is connected with the Input voltage, the Vin applied has to be greater than the threshold voltage for the channel to form such that the current flows( drain ).

In order to supply power for the circuit , a DC Power supply has been provided at the drain terminal. The Source terminal is connected to the ground.

The drain current flows from supply to the source.Here the applied input is a voltage and we are interested to find the Output Voltage which is been amplified.

Since the MOSFET is a voltage controlled Current device , the output is the drain current. To convert this current to voltage. By Ohm's Law we observe V= I * R. Thus by applying a Resistor at the drain terminal converts this drain current to voltage.

Thus from the Output curves we know that the amplifier works in Saturation Region of MOSFET

![Image](https://github.com/user-attachments/assets/355e4f53-38ff-442c-b070-0b76902e7f58)

A Q-point (quiescent point) is set in a MOSFET to ensure it operates within its optimal region, providing the desired level of amplification and minimizing distortion and providing a stable DC operating point and also allowing for the largest possible signal swing without clipping or entering non-linear regions.

![Image](https://github.com/user-attachments/assets/0bafae23-8bdc-4ad5-834f-42f12564553e)The input DC Voltage can also be set using the Voltage divider bias rule at the gate terminal.

Capacitors are the components which act as AC Short and DC open. In other words , it allows AC Component and blocks the DC Component. However the impedance of capacitor also comes into play which will be taken during the various frequency resposnse of the system.

![Image](https://github.com/user-attachments/assets/484075a9-8943-4d6b-8196-0f02e17bedb7)

The below is the Voltage Transfer Curve ( Vds VS Vgs ) for a MOSFET.

![Image](https://github.com/user-attachments/assets/c12fe0eb-9a8f-4560-8c02-c3bfd965241b)

Its observed that when Vgs < Vth, the MOSFET is OFF , as a result Vds = Vdd. However When Vgs > Vth the MOSFET is ON , and if Vds >= Vov it works in Saturation Region (as required). Also if Vds < Vov the MOSFET works in Triode Region.

Now, why do we need Saturation Region ? If observed in the figure we get to know that the curve becomes almost linear in the saturation region. In an input is applied to this region the amplification is at maximum ( higher gain ). So this almost-linear region plays an important role during setting the Q-point.

An 180 deg phase shift is observed at the output. We observe that :

![Image](https://github.com/user-attachments/assets/fc3c815f-4119-42ac-bc6d-d4a869e4f8e5)

And as a result in the input voltage increases the drain current (Id) increases, as a result the Id*Rd term increases. So the Vds value decreases with increase in Vgs . Thus its inverting.

It should also be noted that the input ac signal that we are providing has to be vgs << 2vov for proper operation of amplifier. Other wise if the positive peak is increased, then the negative side will go into the triode region and causes distortion. Also, if the negative side is increased, then the positive side will go into the cutoff region leading to clipping off of signal.

By carefully going and calculating all the parameters and applying an AC signal, its possible to get a very high gain. However we are not interested in such a high value of gain. In order to reduce and stabilize the gain at a good level, we apply a source resistor that acts as source degeneration leading to steady and stable gain.Also, by applying a bypass Capacitor the Gain increases as it helps the unwanted AC signal to bypass the source resistance.

A complete model looks something like this:

![Image](https://github.com/user-attachments/assets/1a555326-9883-4c21-87b3-d5b4f75c2e7b)

Now coming to the frequency response of the CS Amplifier,

![Image](https://github.com/user-attachments/assets/88a55736-efac-4362-9d47-7f62ad536e44)

Its observed that capacitive impedances come into play for lower frequencies and Mosfet capacitances also play a role at higher frequencies. Thus the difference between the Upper Cutoff frequency and Lower Cutoff frequency that is the midband frequency is the frequency range where no capacitive effect comes into play for the CS Amplifier and all the Capacitors acts as AC Short.

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Q1.Design CS amplifier using n mosfet in the tsmc 180nm tech.lib in lt spice use VDD=1.8V , P<=1mW , C(load)=10pF , Ln=560nm 

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
