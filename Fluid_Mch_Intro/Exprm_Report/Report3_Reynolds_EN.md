# FLUID MECHANICS EXPERIMENT REPORT

## 3. Reynolds Experiment

**Experimental location: D08-202**

### Experimental Purpose

1. To observe the flow patterns of laminar flow, transitional flow and turbulent flow in a circular pipe.
2. To understand the physical meaning of the Reynolds number and its role in judging flow regimes.
3. To determine the lower critical Reynolds number experimentally by observing the shape and stability of the dyed water thread.

### Experimental Procedure

1. Start the apparatus and adjust the water supply until the flow in the test pipe is steady and free of visible disturbances.
2. Open the dye valve slightly and introduce a thin dyed water thread into the pipe centerline.
3. Begin with a small valve opening and observe whether the dyed thread remains straight and stable, indicating laminar flow.
4. Gradually increase the flow rate and record the flow rate and dye-thread shape when the flow changes from laminar to transitional or turbulent.
5. Then gradually decrease the flow rate from turbulent flow and record the flow condition when the dyed thread becomes stable again.
6. Calculate the Reynolds number for each condition and determine the lower critical Reynolds number from repeated measurements.

### Data Processing

#### 1. Record relevant information and experimental data

- Experimental equipment name: __________
- Experimental table number: __________
- Experimenter: __________ Experimental date: __________
- Pipe diameter $d$ = 1.40 ×10⁻² m
- Water temperature $t$ = 18.0 °C
- Kinematic viscosity $\nu = \frac{0.01775 \times 10^{-4}}{1 + 0.0337t + 0.000221t^2}$ (m²/s) = 1.058 ×10⁻⁴ m²/s
- Calculation constants $K = \frac{4}{\pi \nu d}$ = 85.99 ×10⁶ s/m³

#### 2. Experimental data recording and calculation results

**Table 3.1 Reynolds experiment recording and calculation table**

| No. | Shape of dyed water thread | volume of flow$q_v$ (10⁻⁶m³/s) | Reynolds number$Re$ | opening of valve increase (↑) or decrease (↓) | Remarks        |
| --- | -------------------------- | ----------------------------------- | --------------------- | ----------------------------------------------- | -------------- |
| 1   | scatter to straight        | 27.3                                | 2347                  | ↓                                              | lower critical |
| 2   | scatter to straight        | 28.6                                | 2459                  | ↓                                              | lower critical |
| 3   | scatter to straight        | 25.6                                | 2201                  | ↓                                              | lower critical |
| 4   | scatter to straighter      | 25.4                                | 2184                  | ↓                                              | lower critical |
| 5   | scatter to straight        | 26.4                                | 2270                  | ↓                                              | lower critical |
| 6   | straight to scatter        | 28.9                                | 2485                  | ↑                                              | upper critical |
| 7   | straight to scatter        | 31.9                                | 2743                  | ↑                                              | upper critical |

Measured lower critical Reynolds number (average) $Re_c$ = 2292

#### 3. Achievement requirements

(1) Measure the lower critical Reynolds number (2-4 times, take the average), as shown in Table 3.1.

$$Re_c = \frac{2347 + 2459 + 2201 + 2184 + 2270}{5} = 2292$$

The measured lower critical Reynolds number $Re_c = 2292$ agrees well with the standard value of 2300 for circular pipe flow.

(2) Measure the upper critical Reynolds number (1-2 times, record separately), as shown in Table 3.1.

The two measurements give $Re_c' = 2485$ and $2743$. The large variation confirms that the upper critical Reynolds number is unstable and sensitive to disturbances.

(3) Determine the generalized Reynolds number expression and the measured value.

For a circular pipe, the hydraulic radius is $R = A/\chi = (\pi d^2/4)/(\pi d) = d/4 = 0.35 \times 10^{-2}$ m. The generalized Reynolds number is:

$$Re_g = \frac{vR}{\nu} = \frac{Re}{4}$$

Therefore, the generalized lower critical Reynolds number is:

$$Re_{g,c} = \frac{Re_c}{4} = \frac{2292}{4} = 573$$

---

### Analysis and Reflection

1. Why is it believed that the upper critical Reynolds number has no practical significance, while lower critical Reynolds number is used as a criterion for laminar and turbulent flow?

Upper $Re_c'$ is sensitive to external disturbances (inlet conditions, vibrations, roughness) and is not reproducible — useless as a universal criterion. Lower $Re_c \approx 2300$ is stable: regardless of upstream turbulence, once $Re$ drops below it, viscosity always damps disturbances and flow returns to laminar.

---

2. Based on the observation of turbulence mechanism experiments, analyze the mechanism of transition from laminar to turbulence flow.

At low $Re$, viscosity dominates: disturbances are damped, dye thread stays straight. As $Re$ rises, inertia overtakes viscosity — perturbations grow instead of decaying. Intermittent turbulent spots appear, grow, and merge until the flow becomes fully chaotic with 3D mixing. The transition is an instability governed by $Re$ = inertia/viscosity.

---
