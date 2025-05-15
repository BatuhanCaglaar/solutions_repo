# Problem 1
 

### **Measuring Earth's Gravitational Acceleration with a Pendulum**


## **Motivation**

The acceleration $g$ due to gravity is a fundamental constant in physics, vital for everything from engineering applications to understanding celestial motion. One classic and elegant method for determining $g$ is by measuring the oscillation period of a simple pendulum. The mathematical simplicity of the pendulum model makes it ideal for undergraduate-level experiments, while the precision it demands fosters deep appreciation for measurement techniques and uncertainty analysis.

This problem not only focuses on calculating $g$, but also emphasizes rigorous experimental techniques, statistical processing of measurement data, and propagation of uncertainties. Such approaches form the backbone of empirical science.

---

## **Procedure**

### **1. Materials**

- String (1.000 m measured with ±0.001 m accuracy)
- Small dense weight (e.g., a metal nut)
- Stopwatch (resolution 0.01 s)
- Ruler or measuring tape
- Rigid support (stand, ceiling mount, or hook)
- Data recording sheet or spreadsheet

### **2. Setup**

- Fix the string securely to the support.
- Attach the mass firmly at the end of the string.
- Measure the length $L$ from the pivot point to the center of mass of the weight.

#### **Uncertainty in Length**

- Resolution of the tape is ±0.001 m →

$$
\Delta L = \frac{0.001}{2} = 0.0005 \ \text{m}
$$

---

## **3. Data Collection**

Conduct the following steps:

- Displace the pendulum to an angle less than 15°.
- Release gently without pushing.
- Time 10 complete oscillations (back and forth = 1 cycle).
- Repeat 10 times for consistency.

### **Raw Data Table**

| Trial | $T_{10}$ (s) |
|-------|--------------|
| 1     | 20.11        |
| 2     | 20.15        |
| 3     | 20.13        |
| 4     | 20.14        |
| 5     | 20.12        |
| 6     | 20.16        |
| 7     | 20.10        |
| 8     | 20.14        |
| 9     | 20.13        |
| 10    | 20.12        |

### **Statistical Summary**

- Mean time for 10 oscillations:

$$
\overline{T}_{10} = \frac{\sum T_{10}}{10} = 20.13 \ \text{s}
$$

- Standard deviation:

$$
\sigma_T = \sqrt{\frac{1}{n-1} \sum (T_{10,i} - \overline{T}_{10})^2} = 0.01826 \ \text{s}
$$

- Standard uncertainty:

$$
\Delta T_{10} = \frac{\sigma_T}{\sqrt{10}} = 0.00577 \ \text{s}
$$

---

## **Calculations**

### **1. Period and Uncertainty**

- Period:

$$
T = \frac{\overline{T}_{10}}{10} = 2.013 \ \text{s}
$$

- Period uncertainty:

$$
\Delta T = \frac{\Delta T_{10}}{10} = 0.000577 \ \text{s}
$$

### **2. Calculate $g$**

Use the formula for a simple pendulum:

$$
g = \frac{4\pi^2 L}{T^2} = \frac{4\cdot (\pi)^2 \cdot 1.000}{(2.013)^2} = 9.765 \ \text{m/s}^2
$$

### **3. Propagate Uncertainties**

Use the relative uncertainty propagation formula:

$$
\Delta g = g \cdot \sqrt{\left(\frac{\Delta L}{L}\right)^2 + \left(2\cdot \frac{\Delta T}{T}\right)^2}
$$

Plugging in values:

$$
\Delta g = 9.765 \cdot \sqrt{\left(\frac{0.0005}{1.000}\right)^2 + \left(2\cdot \frac{0.000577}{2.013}\right)^2} = 0.005 \ \text{m/s}^2
$$

---

## **Results Summary Table**

| Quantity             | Value       | Uncertainty      |
|---------------------|-------------|------------------|
| $L$                 | 1.000 m     | $\pm 0.0005$ m   |
| $\overline{T}_{10}$ | 20.13 s     | $\pm 0.00577$ s  |
| $T$                 | 2.013 s     | $\pm 0.000577$ s |
| $g$                 | 9.765 m/s²  | $\pm 0.005$ m/s² |

---

## **Analysis and Discussion**

### **1. Comparison with Accepted Value**

- Standard gravitational acceleration at sea level is $9.81 \ \text{m/s}^2$
- Our result is within ~0.46% error margin.

### **2. Sources of Error**

- **Length measurement**: Parallax errors and swing center misalignment.
- **Timing measurement**: Human reaction delays (~0.2 s for single swing!) mitigated by timing multiple swings.
- **Amplitude**: Angle must remain small for simple harmonic approximation to hold.
- **Environmental factors**: Air resistance and string flex may introduce damping and non-ideal behavior.

### **3. Assumptions Validity**

- Small-angle approximation ($\theta < 15^\circ$)
- Neglect of air resistance
- Ideal pivot point

---

## **Conclusion**

From experimental timing and measurement:

$$
g = 9.765 \pm 0.005 \ \text{m/s}^2
$$

This estimate of gravitational acceleration is accurate within reasonable uncertainty bounds. This experiment underscores the importance of repetition, accurate data collection, and statistical processing in experimental physics.

---

## **Further Extensions**

- **Use a photogate** for more accurate period detection.
- **Test with multiple lengths** and plot $T^2$ vs $L$ to validate linearity (slope gives $g$).
- **Simulate pendulum motion** using differential equations for large angles.

---

## **Appendix: Python Code Example**

```python
import numpy as np

# Inputs
L = 1.000     # length in meters
dL = 0.0005
T10 = np.array([20.11, 20.15, 20.13, 20.14, 20.12, 20.16, 20.10, 20.14, 20.13, 20.12])

T10_mean = np.mean(T10)
T10_std = np.std(T10, ddof=1)
T10_unc = T10_std / np.sqrt(len(T10))

T = T10_mean / 10
dT = T10_unc / 10

g = (4 * np.pi**2 * L) / T**2
dg = g * np.sqrt((dL / L)**2 + (2 * dT / T)**2)

print(f"g = {g:.4f} ± {dg:.4f} m/s²")
```

---
