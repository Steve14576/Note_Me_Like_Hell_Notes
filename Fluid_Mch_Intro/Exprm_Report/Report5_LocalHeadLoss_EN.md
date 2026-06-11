# FLUID MECHANICS EXPERIMENT REPORT

## 5. Local Head Loss Experiment

**Experimental location: D08-202**

### Experimental Purpose

1. To understand the mechanism of local head loss caused by sudden expansion, sudden contraction and other local pipe structures.
2. To learn how to measure local resistance coefficients by using the three-point method and the four-point method.
3. To compare the measured resistance coefficients with theoretical or empirical values and analyze the causes of experimental error.

### Experimental Procedure

1. Start the pump and keep the constant head tank in a stable overflow condition.
2. Close the experimental flow control valve, open the air release valve, and remove trapped air from the pipeline and piezometer tubes.
3. Check whether all piezometer tube liquid levels are normal, and repeat the bleeding process if bubbles remain.
4. Adjust the flow control valve to obtain a steady flow rate, then record the flow rate and the readings of piezometer tubes h1 to h6.
5. Change the flow rate two or three times, including one relatively large flow rate, and repeat the readings after each condition becomes stable.
6. Use the recorded data to calculate the local head losses and local resistance coefficients for the sudden expansion and sudden contraction sections.

### Data Processing

#### 1. Record relevant information and experimental data

- Experimental equipment name: __________
- Experimental table number: __________
- Experimenter: __________ Experimental date: __________
- Experimental pipe segment diameter:
  - $d_1 = D_1$ = 1.00 ×10⁻²m
  - $d_2 = d_3 = d_4 = D_2$ = 2.00 ×10⁻²m
  - $d_5 = d_6 = D_3$ = 1.00 ×10⁻²m
- Experimental pipe segment length:
  - $l_{1-2}$ = 12.0 ×10⁻²m, $l_{2-3}$ = 24.0 ×10⁻²m, $l_{3-4}$ = 12.0 ×10⁻² m
  - $l_{4-5}$ = 12.0 ×10⁻²m, $l_{5-6}$ = 24.0 ×10⁻²m

#### 2. Experimental data recording and calculation results

**Table 5.1 Local Head Loss Experiment records table**

| No. | volume of flow$q_V$ /(10⁻⁶m³/s) | piezometer value /10⁻²m |         |         |         |         |         |
| --- | ------------------------------------ | ------------------------- | ------- | ------- | ------- | ------- | ------- |
|     |                                      | $h_1$                   | $h_2$ | $h_3$ | $h_4$ | $h_5$ | $h_6$ |
| 1   | 96.2                                 | 16.81                     | 19.53   | 19.42   | 19.38   | 5.61    | 1.83    |
| 2   | 86.5                                 | 20.97                     | 23.33   | 22.99   | 23.10   | 12.72   | 10.26   |
| 3   | 62.5                                 | 26.66                     | 28.16   | 28.00   | 27.85   | 21.90   | 20.20   |

**Table 5.2 Local Head Loss Experimental calculation table**

| No. | Resistance form    | volume of flow$q_V$ /(10⁻⁶m³/s) | upstream section                   |                   | downstream section                 |                   | $h_j$ /10⁻²m | theoretical value$\zeta$ | empirical value$\zeta$ |
| --- | ------------------ | ------------------------------------ | ---------------------------------- | ----------------- | ---------------------------------- | ----------------- | ---------------- | -------------------------- | ------------------------ |
|     |                    |                                      | $\frac{\alpha v^2}{2g}$ /10⁻²m | $E_1'$ /10⁻²m | $\frac{\alpha v^2}{2g}$ /10⁻²m | $E_2'$ /10⁻²m |                  |                            |                          |
| 1   | sudden expansion   | 96.2                                 | 7.65                               | 24.46             | 0.48                               | 20.01             | 4.39             | 0.5625                     | 0.5746                   |
| 2   | sudden expansion   | 86.5                                 | 6.18                               | 27.15             | 0.39                               | 23.72             | 3.27             | 0.5625                     | 0.5283                   |
| 3   | sudden expansion   | 62.5                                 | 3.23                               | 29.89             | 0.20                               | 28.36             | 1.45             | 0.5625                     | 0.4480                   |
| 1   | Sudden contraction | 96.2                                 | 0.48                               | 19.84             | 7.65                               | 17.04             | 2.80             | —                          | 0.3663                   |
| 2   | Sudden contraction | 86.5                                 | 0.39                               | 23.54             | 6.18                               | 21.36             | 2.18             | —                          | 0.3525                   |
| 3   | Sudden contraction | 62.5                                 | 0.20                               | 27.98             | 3.23                               | 26.83             | 1.15             | —                          | 0.3560                   |

Notes: $\zeta$ is corresponding to $v_1$ of the expansion segment or $v_5$ of the contraction segment.

#### 3. Achievement requirements

(1) Measure the local head loss factor $\zeta$ value of the sudden expansion section, compare and analyze it with the theoretical value. As shown in Table 5.2.

For sudden expansion, the theoretical coefficient (Borda-Carnot formula) is:

$$\zeta_{theory} = \left(1 - \frac{A_1}{A_2}\right)^2 = \left(1 - \frac{d_1^2}{d_2^2}\right)^2 = \left(1 - \frac{1.00^2}{2.00^2}\right)^2 = 0.5625$$

The measured $\zeta$ values (0.5746, 0.5283, 0.4480) show reasonable agreement with theory at higher flow rates, with increasing deviation at lower flow rates due to greater relative uncertainty in the small friction-loss correction term $h_{f1-2} = (h_2 - h_3)/2$.

(2) Measure the local head loss factor $\zeta$ value of the sudden contraction section, compare and analyze it with the empirical value. As shown in Table 5.2.

The empirical formula for sudden contraction is:

$$\zeta_{emp} = 0.5\left(1 - \frac{A_3}{A_2}\right) = 0.5\left(1 - \frac{1.00^2}{2.00^2}\right) = 0.3750$$

The measured $\zeta$ values (0.3663, 0.3525, 0.3560, average 0.3583) are consistently close to the empirical value of 0.3750, with a relative deviation of approximately 4.5%. The agreement validates both the four-point method and the empirical correlation.

---

### Analysis and Reflection

1. For pipes with the same diameter ratio d1/d2 (d1<d2) and same flow rate, within what range of the ratio is the head loss for sudden expansion greater than that for sudden contraction?

Sudden expansion loss is always larger. From Table 5.2: at $q_v=96.2$, $h_{j,exp}=4.39$ cm vs $h_{j,con}=2.80$ cm (ratio ≈ 1.57). Expansion creates a large recirculation zone with intense dissipation; contraction has a smaller vena contracta region. Theoretically $\zeta_{exp}=0.5625$ vs $\zeta_{con}=0.3750$ for $A_1/A_2=0.25$, and with different reference velocities, expansion loss is typically 40-60% greater.

---

2. Analyze the mechanism of local resistance loss, by combining the hydraulic phenomena of the flow demonstration instrument. Where are the main locations of local head loss caused by sudden expansion and contraction? How to reduce local head loss?

Mechanism: abrupt geometry change → flow separates from wall → recirculation zones → energy dissipated as heat.

**Sudden expansion:** main loss immediately downstream of expansion plane — high-velocity jet forms large annular recirculation zone; mixing between jet core and recirculation fluid dissipates energy.

**Sudden contraction:** loss at (a) acceleration zone upstream (small separation at sharp corner), and (b) vena contracta re-expansion downstream (essentially a mini sudden expansion, accounting for most loss).

**Reduction:** use gradual transitions — conical diffusers (angle ≤8°) instead of sudden expansion, bell-mouth inlets instead of sudden contraction.

---

3. There are many types of local resistances. Except for sudden expansion, whose formula is derived theoretically, most local resistance coefficients are obtained experimentally as empirical formulas. What are the approaches to obtaining empirical formulas?

(1) Systematic experimentation over a range of $Re$ and geometry; (2) dimensional analysis to identify dimensionless groups ($\zeta = f(\text{geometry}, Re)$); (3) data correlation, typically $\zeta = f(\text{geometry}) \cdot g(Re)$ where $g(Re)$ → constant at high $Re$; (4) validation against independent datasets. Standard handbooks (e.g., Idelchik) compile thousands of such correlations; CFD supplements experiments for complex geometries.

---
