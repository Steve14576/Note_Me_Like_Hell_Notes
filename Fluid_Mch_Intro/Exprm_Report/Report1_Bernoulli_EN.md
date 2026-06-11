# FLUID MECHANICS EXPERIMENT REPORT

## 1. Comprehensive Experiment on Bernoulli's Equation for Steady Total Flow

**Experimental location: D08-202**

### Experimental Purpose

1. To understand the physical meaning of Bernoulli's equation for steady total flow and the relationship among elevation head, pressure head, velocity head and total head.
2. To observe how the piezometric head line and total head line change along a pipe with different cross-sections.
3. To verify the energy equation experimentally and analyze the influence of flow rate and local pipe geometry on head distribution.

### Experimental Procedure

1. Start the pump and adjust the apparatus until the water flow becomes steady and the water tank maintains a stable overflow condition.
2. Record the pipe diameters, distances between measuring points, water surface elevation and pipe axis elevation required for calculation.
3. Adjust the flow control valve to obtain the first steady flow condition, then read and record the piezometric heads at the required measuring points.
4. Measure and record the corresponding flow rate using the flow measuring device.
5. Change the valve opening to obtain another steady flow condition, and repeat the readings of piezometric heads and flow rate.
6. Calculate the velocity head and total head at each selected section, then draw and compare the piezometric head line and total head line.

### Data Processing

#### 1. Record relevant information and experimental data

- Experimental equipment name: __________
- Experimental table number: __________
- Experimenter: __________ Experimental date: __________
- Uniform section $d_1$ = 1.45 ×10⁻²m
- Throat section $d_2$ = 1.02 ×10⁻²m
- Expansion section $d_3$ = 2.00 ×10⁻²m
- Tank water surface elevation $V_0$ = 44.78 ×10⁻²m
- Elevation of the upper pipeline axis $V_a$ = 19.35 ×10⁻²m

(The reference plane is selected at the zero point of the ruler)

#### 2. Experimental data recording and calculation results

**Table 1.1 Pipe diameter record table**

| Measurement point number                 | ①*  | ② ③ | ④   | ⑤   | ⑥* ⑦ | ⑧* ⑨ | ⑩ ⑪ | ⑫* ⑬ | ⑭* ⑮ | ⑯* ⑰ | ⑱* ⑲ |
| ---------------------------------------- | ---- | ----- | ---- | ---- | ------ | ------ | ----- | ------ | ------ | ------ | ------ |
| pipe diameter$d$ /10⁻²m              | 1.45 | 1.45  | 1.45 | 1.02 | 1.45   | 1.45   | 1.45  | 1.45   | 1.45   | 2.00   | 1.45   |
| Distance between two points$l$/10⁻²m | 4    | 4     | 6    | 6    | 4      | 13.5   | 6     | 10     | 29.5   | 16     | 16     |

**Table 1.2 Piezometric head $h_i$, Flow measurement and recording table**

(where $h_i = z_i + \frac{p_i}{\rho g}$, unit is 10⁻²m, $i$ is the measurement point number)

| experiment times | $h_2$ | $h_3$ | $h_4$ | $h_5$ | $h_7$ | $h_9$ | $h_{10}$ | $h_{11}$ | $h_{13}$ | $h_{15}$ | $h_{17}$ | $h_{19}$ | $q_V$ /(10⁻⁴m³/s) |
| ---------------- | ------- | ------- | ------- | ------- | ------- | ------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------------------- |
| 1                | 46.52   | 46.52   | 46.36   | 46.28   | 38.65   | 41.65   | 41.82      | 40.10      | 42.32      | 38.88      | 39.48      | 39.86      | 80.3                   |
| 2                | 41.92   | 41.10   | 40.90   | 41.02   | 24.62   | 29.80   | 30.26      | 25.29      | 31.65      | 23.10      | 24.56      | 20.26      | 137.0                  |

**Table 1.3 Calculation Value Table**

$A = \pi d^2/4$, $v = q_V/A$, $v^2/2g$ with $g = 9.81$ m/s², $\alpha = 1.0$.

**(1) Velocity head** ($q_V$ in 10⁻⁶ m³/s, $A$ in 10⁻⁴ m², $v$ in 10⁻² m/s, $v^2/2g$ in 10⁻² m)

**$q_{V1}=80.3$**

| $d$ /cm | $A$ | $v$ | $v^2/2g$ |
|---------|------|-----|----------|
| 1.45 | 1.651 | 48.6 | 1.21 |
| 1.02 | 0.817 | 98.3 | 4.92 |
| 2.00 | 3.142 | 25.6 | 0.33 |

**$q_{V2}=137.0$**

| $d$ /cm | $A$ | $v$ | $v^2/2g$ |
|---------|------|-----|----------|
| 1.45 | 1.651 | 83.0 | 3.51 |
| 1.02 | 0.817 | 167.7 | 14.33 |
| 2.00 | 3.142 | 43.6 | 0.97 |

**(2) Total head** $H_i = h_i + \alpha v_i^2/(2g)$ (unit: 10⁻²m)

| No. | $H_2$ | $H_4$ | $H_5$ | $H_7$ | $H_9$ | $H_{13}$ | $H_{15}$ | $H_{17}$ | $H_{19}$ | $q_V$ /10⁻⁶m³/s |
|-----|-------|-------|-------|-------|-------|----------|----------|----------|----------|-----------------|
| 1   | 47.73 | 47.57 | 51.20 | 39.86 | 42.86 | 43.53 | 40.09 | 39.81 | 41.07 | 80.3 |
| 2   | 45.43 | 44.41 | 55.35 | 28.13 | 33.31 | 35.16 | 26.61 | 25.53 | 23.77 | 137.0 |

#### 3. Achievement requirements

(1) Calculate velocity heads and total heads (see Table 1.3).

**Sample calculation** (d = 1.45 cm, $q_{V1}=80.3 \times 10^{-6}$ m³/s):

$$A = \frac{\pi}{4}(0.0145)^2 = 1.651 \times 10^{-4} \text{ m²}$$

$$v = \frac{q_V}{A} = \frac{80.3 \times 10^{-6}}{1.651 \times 10^{-4}} = 0.486 \text{ m/s}$$

$$\frac{v^2}{2g} = \frac{0.486^2}{2 \times 9.81} = 1.21 \times 10^{-2} \text{ m}$$

Other diameters computed likewise. See Table 1.3(1).

**Total head:** $H_i = h_i + \alpha v_i^2/(2g)$, with $h_i$ from Table 1.2 and $v_i^2/2g$ matched by pipe diameter. Results in Table 1.3(2).

**Comparison:** Low flow ($q_{V1}$): $H$ uniform (39.8–51.2 cm), losses small. High flow ($q_{V2}$): $H$ drops from 45.43 cm (②) to 23.77 cm (⑲) — losses $\propto v^2$.

---

(2) Draw the total head line and piezometric head line for the maximum flow rate from the above results.

Data from Experiment 2 ($q_{V2} = 137.0 \times 10^{-6}$ m³/s), units: 10⁻² m.

| Point | ② | ④ | ⑤ | ⑦ | ⑨ | ⑬ | ⑮ | ⑰ | ⑲ |
|-------|-----|-----|-----|-----|-----|------|------|------|------|
| HGL ($h_i$) | 41.92 | 40.90 | 41.02 | 24.62 | 29.80 | 31.65 | 23.10 | 24.56 | 20.26 |
| EGL ($H_i$) | 45.43 | 44.41 | 55.35 | 28.13 | 33.31 | 35.16 | 26.61 | 25.53 | 23.77 |

**Observations:** EGL always slopes downward (energy dissipation). HGL rises/falls with kinetic–pressure energy interchange: drops sharply at throat ⑤ (acceleration), rises at expansion ⑰ (deceleration). Gap EGL − HGL = $v^2/2g$.

### Analysis and Reflection

1. What are the differences in the trend of changes between the piezometric head line and the total head line? Why?

EGL always decreases monotonically — mechanical energy is irreversibly dissipated by friction. HGL can rise or fall because pressure and kinetic energy interchange: at the throat, acceleration lowers pressure (HGL drops); in the expansion, deceleration recovers pressure (HGL rises). The gap EGL − HGL = $v^2/2g$.

---

2. When the valve is opened wider, increasing the flow rate, how does the piezometric head line change? Why?

The entire HGL shifts downward and steepens. Two reasons: (i) higher $v$ means more pressure energy converts to kinetic energy; (ii) losses $\propto v^2$, so EGL drops faster, dragging HGL with it. In our data, $h_{19}$ falls from 39.86 to 20.26 cm.

---

3. There is generally a difference between the total head line measured by the Pitot tube and the total head line drawn based on the average flow velocity of the measured cross-section. Please analyze the reasons for this.

The Pitot tube measures centerline $u_{max}$, while the HGL/EGL are drawn from cross-sectional average $\bar{v}$. Since $u_{max} > \bar{v}$ (velocity profile is non-uniform), $u_{max}^2/2g > \bar{v}^2/2g$, so Pitot-based total head is higher. The kinetic energy correction factor $\alpha = \frac{1}{A}\int_A (u/\bar{v})^3 dA > 1$ accounts for this. We used $\alpha = 1.0$, so our EGL lies slightly below Pitot measurements.

---

4. Why can't a rapidly varied flow section be chosen as the calculation section for the energy equation?

In rapidly varied flow (e.g., downstream of a sudden expansion), streamlines are curved and non-parallel, so the hydrostatic pressure assumption breaks down — $z + p/\rho g$ is not constant across the section. A single wall piezometer reading cannot represent the cross-sectional average. The energy equation requires gradually varied flow where streamlines are nearly parallel and pressure is hydrostatic.
