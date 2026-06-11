# FLUID MECHANICS EXPERIMENT REPORT

## 4. Comprehensive Momentum Principle Experiment

**Experimental location: D08-202**

### Experimental Purpose

1. To understand the relationship between fluid momentum and factors such as flow velocity, flow rate and jet direction.
2. To verify the momentum equation for steady incompressible flow through the impact of a water jet on a piston plate.
3. To determine the momentum correction factor of the nozzle jet and understand the working principle of the piston-type force measuring device.

### Experimental Procedure

1. Observe the structure of the apparatus, including the constant head tank, nozzle, piston plate, piezometer tube and digital flowmeter.
2. Start the pump and adjust the water level control valve until the constant head tank overflows steadily.
3. Adjust the piston and piezometer tube so that the piston can move freely and the reading is stable.
4. Under a selected water level, measure the nozzle operating head, the piston water head and the flow rate displayed by the digital flowmeter.
5. Repeat the measurements under three different water levels or flow conditions, such as high, medium and low flow rates.
6. Calculate the jet velocity, momentum force and momentum correction factor, then compare the measured value with the accepted range.

### Data Processing

#### 1. Record relevant information and experimental data

- Experimental equipment name: __________
- Experimental table number: __________
- Experimenter: __________ Experimental date: __________
- Inner diameter of nozzle $d$ =1.205 ×10⁻²m
- Piston diameter $D$ = 2.005×10⁻²m

#### 2. Experimental data recording and calculation results

**Table 4.1 Measurement record and calculation table**

| No. | water head of nozzle$H_0$ /10⁻²m | piston water head$h_c$ /10⁻²m | volume of flow$q_v$ /(10⁻⁶m³/s) | velocity of flow$v$ /(10⁻²m/s) | Momentum force$F$ /10⁻³N | Momentum correction factor$\beta$ |
| --- | ------------------------------------ | --------------------------------- | ------------------------------------ | ---------------------------------- | ---------------------------- | ----------------------------------- |
| 1   | 27.25                                | 17.95                             | 248.5                                 | 218                                | 555                          | 1.03                                |
| 2   | 22.10                                | 14.52                             | 222.7                                 | 195                                | 449                          | 1.03                                |
| 3   | 16.75                                | 10.79                             | 193.5                                 | 170                                | 334                          | 1.02                                |

#### 3. Achievement requirements

(1) Measure the momentum correction factor $\beta$ of the nozzle jet, as shown in table 4.1.

From the three measurements:

$$\beta_1 = \frac{F}{\rho q_v v} = \frac{555 \times 10^{-3}}{1000 \times 248.5 \times 10^{-6} \times 2.18} = 1.027$$

$$\beta_2 = \frac{450}{1000 \times 222.7 \times 10^{-6} \times 1.95} = 1.034$$

$$\beta_3 = \frac{334}{1000 \times 193.5 \times 10^{-6} \times 1.70} = 1.018$$

$$\bar{\beta} = \frac{1.027 + 1.034 + 1.018}{3} = 1.026$$

The measured average $\beta = 1.026$ falls within the recognized range of 1.02–1.05 for turbulent jet flow, confirming the validity of the momentum equation.

(2) Take a certain flow rate, draw a control body diagram, and explain the process of analysis and calculation.

**Using measurement No. 2** ($q_v = 222.7 \times 10^{-6}$ m³/s, $h_c = 14.52$ cm).

Control volume: nozzle exit → impact plate. Jet strikes plate perpendicularly, spreads radially → $v_{2x} = 0$.

**Momentum equation** (x-direction):

$$\sum F_x = \rho q_v(v_{2x} - \beta v_{1x})$$

Plate force on fluid = $-F$, so:

$$-F = \rho q_v(0 - \beta v_1) \quad \Rightarrow \quad F = \beta \rho q_v v_1$$

**Numerical substitution:**

$$A_{nozzle} = \frac{\pi}{4}(1.205 \times 10^{-2})^2 = 1.140 \times 10^{-4} \text{ m²}$$

$$v_1 = \frac{q_v}{A_{nozzle}} = \frac{222.7 \times 10^{-6}}{1.140 \times 10^{-4}} = 1.953 \text{ m/s}$$

$$F = \rho g h_c A_{piston} = 1000 \times 9.81 \times 0.1452 \times 3.157 \times 10^{-4} = 0.450 \text{ N}$$

$$\rho q_v v_1 = 1000 \times 222.7 \times 10^{-6} \times 1.953 = 0.435 \text{ N}$$

$$\beta = \frac{F}{\rho q_v v_1} = \frac{0.450}{0.435} = 1.034$$

---

### Analysis and Reflection

1. Does the measured value of $\beta$ match the recognized value ($\beta$=1.02-1.05)? If it does not meet the requirements, analyze the reasons.

Measured $\beta$ (1.018-1.034, avg 1.026) falls within 1.02-1.05. Scatter sources: residual piston friction, slight water level fluctuations, and piezometer reading uncertainty (±0.5 mm ≈ ±1.5% in $h_c$).

---

2. The plate with vanes gains torque from the jet. Does this affect the analysis of the momentum equation along the x direction for a jet impacting a plate without vanes? Why or why not?

No. Vanes produce torque in the tangential direction (⊥ x-axis), so zero net x-force. They only rotate the piston to convert static friction to smaller dynamic friction, improving measurement sensitivity.

---

3. As shown in Figure 4.2 of the handout, why should the outflow angle of the diverted flow through the small guide tube $a$ be perpendicular to $v_{1x}$?

If outflow had any x-component, $v_{2x} \neq 0$, introducing an unknown into the momentum equation. Perpendicular outflow ensures $v_{2x}=0$, giving the clean form $F = \beta \rho q_v v_1$.

---
