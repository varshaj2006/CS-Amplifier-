# CS Amplifier Design using NMOS (TSMC 180nm)

##  Experiment Details

- Technology: TSMC 180nm
- Tool: LTspice
- Supply Voltage (VDD): 1.2V
- Power Constraint: < 0.4mW
- Load Capacitance (CL): 0.5pF
- Channel Length (Ln): 360nm

- # Introduction

- 
Amplifiers are fundamental building blocks in analog integrated circuits used to increase signal strength. Among MOSFET amplifier configurations — Common Source (CS), Common Drain (CD), and Common Gate (CG) — the Common Source amplifier is most widely used for voltage amplification.

Common Source amplifier provides:

High voltage gain
Moderate input impedance
Good output swing
180° phase shift between input and output
Compared to:

Common Drain → unity gain (buffer)
Common Gate → current amplifier, high-frequency applications
CS amplifier is preferred for general analog voltage amplification.

MOSFET operates as a voltage-controlled current device. A small variation in gate voltage controls drain current which produces amplified voltage across the drain resistor.

For proper amplification MOSFET must operate in saturation:

VGS > VTH
VDS ≥ (VGS − VTH)

In practical ICs, MOSFET contains parasitic capacitances:

Gate–Source capacitance (Cgs)
Gate–Drain capacitance (Cgd)
Drain–Body capacitance (Cdb)
These affect high-frequency response and reduce gain and bandwidth.

When load capacitor is connected:

bandwidth decreases
gain-bandwidth tradeoff observed

---

#  Aim

To design and simulate a Common Source (CS) amplifier using NMOS in TSMC 180nm technology using LTspice such that:

- VDD = 1.2V  
- Power < 0.4mW  
- CL = 0.5pF  
- Ln = 360nm  

---

#  Theory

A Common Source amplifier:

- Provides high voltage gain
- Produces 180° phase shift
- Operates in saturation region

Drain current equation (Saturation):

ID = (1/2) μnCox (W/L) (Vov)^2

Voltage Gain:

Av = -gm RD

Where:

gm = 2ID / Vov

---

# Design Calculations

## Step 1: Power Constraint

P = VDD × ID

ID < 0.4mW / 1.2V  
ID < 0.333mA  

Choose:

ID = 0.3mA  

Power = 1.2 × 0.3mA = 0.36mW https://github.com/varshaj2006/CS-Amplifier-/blob/main/img1.jpg

---

## Step 2: Choose Overdrive Voltage

Assume:

Vov = 0.2V  

---

## Step 3: Calculate W/L

Assume:

μnCox ≈ 300µA/V²  

0.3mA = (1/2)(300µA/V²)(W/0.36)(0.2²)

W ≈ 18µm  

Final Dimensions:

W = 18u  
L = 360n  

---

## Step 4: Drain Resistor

Choose mid-point bias:

VD ≈ 0.6V  

RD = (1.2 - 0.6) / 0.3mA  

RD = 2kΩ  
https://github.com/varshaj2006/CS-Amplifier-/blob/main/img2.jpg

---

#  Circuit Diagram

 Attach LTspice schematic screenshot here

Components:

- VDD = 1.2V  
- RD = 2kΩ  
- NMOS: W=18u, L=360n  
- CL = 0.5pF  
- Gate Bias ≈ 0.7V
- https://github.com/varshaj2006/CS-Amplifier-/blob/main/circuit%20diagram%20of%20cs%20amplifier.jpg

---



```
```

---

#  DC Operating Point Analysis

Procedure:

1. Run .op simulation  
2. Observe ID, VDS, VGS  

Expected Results:

- ID ≈ 0.3mA  
- VDS ≈ 0.6V  
- Power ≈ 0.36mW  

Attach DC Operating Point screenshot here  
https://github.com/varshaj2006/CS-Amplifier-/blob/main/DC%20operating%20point.jpg

---

#  DC Sweep Analysis

Command:

.dc VIN 0 1.2 0.01  

Observation:

- Plot Vout vs Vin  
- Identify saturation region  

 Attach DC Sweep graph screenshot here  
https://github.com/varshaj2006/CS-Amplifier-/blob/main/dc%20sweep.jpg
---

#  Transient Analysis

Command:

.tran 0 50n  

Apply small sine input (10mV).  

Expected Result:

- Output inverted waveform  
- 180° phase shift  

 Attach transient waveform screenshot here  
 https://github.com/varshaj2006/CS-Amplifier-/blob/main/transient%20analysis.jpg

 https://github.com/varshaj2006/CS-Amplifier-/blob/main/transient%20analysis%201.jpg

 https://github.com/varshaj2006/CS-Amplifier-/blob/main/transient%20analysis%202.jpg

---

#  Gain Calculation

Theoretical:

gm = 2ID / Vov  
gm = 2(0.3mA)/0.2  
gm = 3mS  

Av = -gm RD  
Av = -(3mS)(2k)  
Av ≈ -6  

Gain in dB:

20 log(6) ≈ 15.5 dB  

---

#  AC Analysis

Command:

.ac dec 100 1 1G  

Observation:

- Gain ≈ 15.5 dB  
- Bandwidth ≈ 150 MHz  
- Phase shift ≈ -180°  

 Attach Bode plot screenshot here  
 https://github.com/varshaj2006/CS-Amplifier-/blob/main/AC%20analysis%20without%20capacitor.jpg
 https://github.com/varshaj2006/CS-Amplifier-/blob/main/AC%20analysis%20with%20capacitor.jpg

---

# Results

- Successfully designed CS amplifier  
- Gain ≈ -6  
- Power < 0.4mW  
- Verified saturation operation  
- Verified 180° phase shift  

---

#  Conclusion

The Common Source amplifier using TSMC 180nm technology was successfully designed and simulated in LTspice. The circuit satisfies the given power constraint and provides the expected gain and bandwidth performance.

---

# Inference

- Increasing W increases gain  
- Increasing RD increases gain but reduces bandwidth  
- Increasing CL reduces bandwidth  
- Proper biasing ensures saturation operation  


#Experiment 04 - differential amplifier
Differential Amplifier Analysis
Aim
To design and simulate three MOSFET differential amplifier configurations using LTspice by performing DC, Transient, and AC analyses, and to compare their performance based on gain, bandwidth, and power efficiency.

Introduction
A differential amplifier is one of the most fundamental building blocks in analog circuit design. It amplifies the difference between two input signals while rejecting common-mode signals, making it highly useful in noise-sensitive applications.

MOSFET-based differential amplifiers are widely used in integrated circuits such as operational amplifiers, comparators, and analog signal processing systems due to their high gain, good noise immunity, and efficient performance.

In this experiment, three different MOSFET differential amplifier configurations are analyzed using LTspice. The behavior of each circuit is studied through DC, Transient, and AC analyses to understand their gain, bandwidth, and overall performance characteristics.

Theory
A differential amplifier is a circuit that amplifies the difference between two input signals while rejecting any signal that is common to both inputs. This property is known as common-mode rejection and is an important feature in analog circuit design.

A basic MOS differential amplifier consists of two matched MOSFETs (M1 and M2) whose sources are connected together and biased using a constant current source. The drains are connected to load elements such as resistors or active loads.

When a differential input voltage is applied:

v
i
d
=
v
i
n
1
−
v
i
n
2

the total current is steered between the two transistors depending on the input difference. If 
v
i
n
1
>
v
i
n
2
, transistor M1 conducts more current, and if 
v
i
n
2
>
v
i
n
1
, transistor M2 conducts more.

For small differential inputs, both transistors operate in the saturation region, and the circuit behaves linearly. The differential gain of the amplifier is given by:

A
v
=
g
m
R
o
u
t

where 
g
m
 is the transconductance of the MOSFET and 
R
o
u
t
 is the effective output resistance.

The transconductance is defined as:

g
m
=
2
I
D
V
o
v

where 
I
D
 is the drain current and 
V
o
v
 is the overdrive voltage.

For larger differential inputs:

v
i
d
>
2
V
o
v

one transistor turns OFF while the other carries the entire current, resulting in non-linear operation.

The performance of the differential amplifier depends on the type of load used:

Resistive load → moderate gain
Active load → higher output resistance and higher gain
Current mirror load → maximum gain and improved output characteristics
Thus, by changing the circuit configuration, the gain, bandwidth, and overall performance of the differential amplifier can be significantly affected.
