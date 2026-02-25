# CS Amplifier Design using NMOS (TSMC 180nm)

##  Experiment Details

- Technology: TSMC 180nm
- Tool: LTspice
- Supply Voltage (VDD): 1.2V
- Power Constraint: < 0.4mW
- Load Capacitance (CL): 0.5pF
- Channel Length (Ln): 360nm

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

Power = 1.2 × 0.3mA = 0.36mW 

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

.
