# FLUID MECHANICS EXPERIMENT REPORT

## 6. Pitot Tube Velocity Measurement and Calibration Factor Experiment

**Experimental location: D08-202**

### Experimental Purpose

1. To understand the structure, working principle and applicable conditions of a Pitot tube.
2. To measure the point velocity of a submerged nozzle jet by using the pressure head difference between total pressure and static pressure.
3. To determine the point velocity coefficient of the nozzle jet and learn how to calibrate the Pitot tube correction factor.

### Experimental Procedure

1. Install the Pitot tube near the nozzle outlet, align its opening with the nozzle centerline, and make sure the installation angle is within the required range.
2. Start the pump, adjust the speed regulator and keep the water tanks in a stable overflow condition.
3. Remove air bubbles from the Pitot tube, connecting tubes and piezometer tubes until the readings become stable.
4. Adjust the water level control valve to obtain a high water level condition, then record h1, h2, h3, h4 and the velocity meter reading.
5. Repeat the measurements under medium and low water level conditions after the flow becomes steady each time.
6. Calculate the operating head, Pitot pressure head difference, point velocity and point velocity coefficient according to the recorded data.

### Data Processing

#### 1. Record relevant information and experimental data

- Experimental equipment name: __________
- Experimental table number: __________
- Pitot tube correction factor $c$ = ____0.997____
- $k$ = 4.41 m⁰·⁵/s

#### 2. Experimental data recording and calculation results

**Table 6.1 Pitot Tube Velocity Experiment Recording and Calculation Table**

| No. | upstream and downstream water levels |                  |                       | Pitot Manometer Readings |                  |                       | flow velocity of measurement point$u = k\sqrt{\Delta h}$ /(m/s) | measurement value of flowmeter /(m/s) | velocity factor of measurement point$\varphi' = c\sqrt{\Delta h / \Delta H}$ |
| --- | ------------------------------------ | ---------------- | --------------------- | ------------------------ | ---------------- | --------------------- | ----------------------------------------------------------------- | ------------------------------------- | ------------------------------------------------------------------------------ |
|     | $h_1$ /10⁻²m                     | $h_2$ /10⁻²m | $\Delta H$ /10⁻²m | $h_3$ /10⁻²m         | $h_4$ /10⁻²m | $\Delta h$ /10⁻²m |                                                                   |                                       |                                                                                |
| 1   | 36.75                                | 15.32            | 21.43                 | 36.29                    | 15.62            | 20.67                 | 2.01                                                              | 195.8                                 | 0.982                                                                          |
| 2   | 31.15                                | 15.19            | 15.96                 | 31.18                    | 15.55            | 15.63                 | 1.75                                                              | 168.7                                 | 0.990                                                                          |
| 3   | 25.82                                | 15.20            | 10.62                 | 25.85                    | 15.40            | 10.45                 | 1.43                                                              | 136.4                                 | 0.992                                                                          |

#### 3. Achievement requirements

(1) Determine the point velocity of the nozzle jet.

$u = k\sqrt{\Delta h}$, $k = c\sqrt{2g} = 4.41$ m⁰·⁵/s. Sample: $u_1 = 4.41 \times \sqrt{0.2067} = 2.01$ m/s. $u_2=1.75$, $u_3=1.43$ m/s. See Table 6.1.

(2) Determine the point velocity coefficient of the nozzle jet.

$\varphi' = c\sqrt{\Delta h / \Delta H}$. $\varphi_1' = 0.982$, $\varphi_2' = 0.990$, $\varphi_3' = 0.992$. $\bar{\varphi}' = 0.988 \approx 0.994$, near 1.0 → well-designed nozzle, minimal exit loss.

(3) Design an experimental plan to calibrate the pitot tube factor $c$, and verify $c$ through experiment.

Rearrange: $c = \varphi'\sqrt{\Delta H / \Delta h}$. With known $\varphi'=0.995$: $c_1 = 1.013$, $c_2 = 1.005$, $c_3 = 1.003$, avg $c = 1.007$ (apparatus: 0.997). Deviation from nominal $\varphi'$.

---

### Analysis and Reflection

1. What does the $\varphi'$ value measured in this experiment indicate?

$\varphi' \approx 0.988$ (near 1.0) shows the nozzle is well-designed: nearly all operating head $\Delta H$ converts to kinetic energy at the jet core. The deviation (~1.2%) is due to the thin boundary layer and minor friction along the nozzle wall. A significantly lower $\varphi'$ would indicate flow separation or large friction losses.

---

2. The range of flow velocity measured by the pitot tube is 0.2~2 m/s, and the axial installation deviation should not exceed 10°. Please analyze the reasons for this.

**0.2 m/s lower limit:** at low $u$, $\Delta h = u^2/(2g) \approx 0.2$ cm — meniscus/capillary effects and ±0.5 mm scale resolution give ~25% uncertainty.

**2 m/s upper limit:** risk of cavitation and probe disturbance to the flow field.

**≤10° alignment:** Pitot measures $p_0$ only when perfectly aligned. Angled probe reads a mix of static + dynamic pressure. Error stays <1% within 10°, grows rapidly beyond.

---

3. What new innovative insights do you have for electrical measurement?

Replace manometer with electronic pressure transducers → direct digital signal, real-time display, continuous logging. Multi-hole probes with miniature sensors enable simultaneous 3D velocity measurement. Wireless DAQ allows automated processing and remote monitoring. Combine with hot-wire/LDV for calibration + high-frequency turbulent fluctuation capture. Key advantage: eliminates parallax error, captures transients, enables high-throughput automation.

---
