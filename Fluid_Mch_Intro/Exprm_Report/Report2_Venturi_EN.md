# FLUID MECHANICS EXPERIMENT REPORT

## 2. Comprehensive Venturi Experiment

**Experimental location: D08-202**

### Experimental Purpose

1. To understand the working principle and applicable conditions of the Venturi flowmeter.
2. To measure the pressure head difference between the upstream section and the throat section of a Venturi tube under different flow rates.
3. To determine the discharge coefficient of the Venturi flowmeter and analyze the difference between theoretical flow rate and actual flow rate.

### Experimental Procedure

1. Start the pump, remove trapped air from the connecting tubes and piezometer tubes, and make sure the flow in the apparatus is steady.
2. Record the diameters of the upstream section and throat section, the water temperature, water level elevation and pipe axis elevation.
3. Adjust the flow control valve to obtain a steady flow rate, then read and record the piezometer readings at each pressure measuring point.
4. Measure and record the actual flow rate displayed by the flowmeter or measured by the apparatus.
5. Change the flow rate several times from low to high or from high to low, and repeat the readings after each condition becomes stable.
6. Calculate the theoretical flow rate, Reynolds number and discharge coefficient, then analyze the variation of the discharge coefficient with flow condition.

### Data Processing

#### 1. Record relevant information and experimental data

- Experimental equipment name: __________
- Experimental table number: __________
- Experimenter: __________ Experimental date: __________
- $d_1$ = 1.4 ×10⁻²m, $d_2$ = 0.695 ×10⁻²m
- Water temperature $t$ = 17.9 °C
- $\nu = \frac{0.01775 \times 10^{-4}}{1 + 0.0337t + 0.000221t^2}$ = 1.060 ×10⁻⁴ m²/s
- Water level elevation $V_0$ = 39.0 ×10⁻²m
- Pipeline axis elevation $V_a$ = ______ ×10⁻²m

(The reference plane is selected at the zero point of the ruler)

#### 2. Experimental data recording and calculation results

**Table 2.1 Record table**

| Times | $h_1$ /10⁻²m | $h_2$ /10⁻²m | $h_3$ /10⁻²m | $h_4$ /10⁻²m | volume of flow$q_V$ /(10⁻⁶m³/s) |
| ----- | ---------------- | ---------------- | ---------------- | ---------------- | ------------------------------------ |
| 1     | 58.00            | 11.60            | 53.46            | 13.60            | 104.0                                |
| 2     | 51.36            | 18.26            | 46.20            | 22.40            | 83.3                                 |
| 3     | 47.78            | 23.20            | 41.10            | 27.95            | 66.8                                 |
| 4     | 44.00            | 26.86            | 37.96            | 32.26            | 52.1                                 |
| 5     | 41.80            | 29.40            | 35.48            | 35.25            | 38.2                                 |
| 6     | 40.00            | 31.16            | 33.60            | 37.40            | 24.3                                 |

**Table 2.2 Calculation table** $\quad K = 173.4$ ×10⁻⁶m²·⁵/s

| Times | $q_V$ /(10⁻⁶m³/s) | $\Delta h = h_1 - h_2 + h_3 - h_4$ /10⁻²m | $q_V' = K\sqrt{\Delta h}$ /(10⁻⁶m³/s) | $Re$ | $\mu = \frac{q_V}{q_V'}$ |
| ----- | ---------------------- | --------------------------------------------- | -------------------------------------------- | ------ | -------------------------- |
| 1     | 104.0                  | 86.26                                         | 161.0                                        | 8920   | 0.646                      |
| 2     | 83.3                   | 56.90                                         | 130.8                                        | 7145   | 0.637                      |
| 3     | 66.8                   | 37.73                                         | 106.5                                        | 5730   | 0.627                      |
| 4     | 52.1                   | 22.84                                         | 82.9                                         | 4469   | 0.629                      |
| 5     | 38.2                   | 12.63                                         | 61.6                                         | 3277   | 0.620                      |
| 6     | 24.3                   | 5.04                                          | 38.9                                         | 2084   | 0.624                      |

### Analysis and Reflection

1. What are the installation requirements and applicable conditions for the Venturi flowmeter?

Upstream ≥10$d_1$, downstream ≥6$d_1$ of straight pipe, near-horizontal, pipe full with steady incompressible flow. Best for clean fluids at turbulent $Re>4000$ where $\mu$ is approximately constant. Not suitable for highly viscous or solids-laden fluids.

---

2. What are the factors that affect the flow factor of the Venturi flowmeter in this experiment? Which factor is most sensitive? For the pipeline in this experiment, if the value of $(d_2 - 0.01) \times 10^{-2}$ m is mistakenly used instead of the above $d_2$ value due to machining inaccuracy, what will be the $\mu$ value at maximum flow rate in this experiment?

$\mu$ depends on $Re$, $\beta = d_2/d_1$, surface roughness, and diffuser angle. Throat diameter $d_2$ is most sensitive (appears to the 4th power).

If $d_2 = 0.685$ cm (off by 0.01 cm): $K' = 168.1 \times 10^{-6}$ m²·⁵/s. At max flow ($q_V=104.0$, $\Delta h=86.26$ cm): $q_V' = 156.2 \times 10^{-6}$ m³/s, $\mu' = 104.0/156.2 = 0.666$. A 1.4% error in $d_2$ shifts $\mu$ by ~3.1%.

---

3. Why is the calculated flow volume not equal to the actual flow volume?

Theoretical $q_V'$ assumes ideal (inviscid) Bernoulli flow. In reality, viscous friction, non-uniform velocity profile ($\alpha>1$), and minor flow separation all dissipate energy. Some $\Delta h$ is consumed overcoming friction rather than accelerating flow, so $q_V' > q_V$. The discharge coefficient $\mu \approx 0.62$-$0.65$ accounts for these losses.

---

4. Using dimensional analysis, explain the hydraulic characteristics of Venturi flowmeter.

6 variables ($\Delta p$, $v$, $\rho$, $\mu_f$, $d_1$, $d_2$) → 3 dimensionless groups:

$$\mu = \frac{q_V}{q_V'} = f\left(Re, \beta, \frac{\varepsilon}{d_1}\right)$$

Key conclusions: (1) at high $Re$, $\mu$ depends only on geometry ($\beta$, roughness); (2) at low $Re$, $\mu$ varies with flow rate, requiring calibration; (3) smaller $\beta$ → larger $\Delta h$ (better sensitivity) but higher permanent loss; (4) standardized Venturi geometry (convergent ~21°, divergent 5–15°) is optimized from dimensional analysis.
