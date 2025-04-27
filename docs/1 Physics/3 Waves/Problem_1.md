# Problem 1


## **Motivation**

Interference occurs when two or more waves overlap, leading to the formation of new wave patterns. On a water surface, interference is visually striking and demonstrates fundamental wave properties such as constructive and destructive interference. Studying these patterns provides deep insights into wave mechanics and their real-world applications in fields such as acoustics, optics, and engineering.

This project explores the behavior of waves from multiple coherent sources arranged at the vertices of a regular polygon. We aim to simulate and analyze the resulting interference patterns using both mathematical formulation and computational modeling.

---

## **1. Mathematical Background**

### **Single Wave Source**

The disturbance at any point $(x, y)$ on a water surface due to a single wave source located at $(x_0, y_0)$ is described by:

$$
\eta(x, y, t) = \frac{A}{\sqrt{r}} \cos(kr - \omega t + \phi)
$$

where:
- $A$ is the amplitude of the wave,
- $k = \frac{2\pi}{\lambda}$ is the wave number,
- $\omega = 2\pi f$ is the angular frequency,
- $r = \sqrt{(x - x_0)^2 + (y - y_0)^2}$ is the distance from the source to point $(x, y)$,
- $\phi$ is the initial phase of the wave.

### **Wave Superposition**

If multiple sources emit coherent waves, the resulting displacement at any point is the **sum** of the individual displacements:

$$
\eta_{\text{sum}}(x, y, t) = \sum_{i=1}^{N} \eta_i(x, y, t)
$$

where $N$ is the number of sources.

Superposition leads to regions of:
- **Constructive Interference**: Waves amplify each other.
- **Destructive Interference**: Waves cancel each other.

---

## **2. Problem Setup**

### **Choosing the Polygon**

We select a **square** (4 sources) centered at the origin for its symmetry and simplicity. Each vertex is equidistant from the center, creating a predictable and analyzable interference pattern.

### **Source Coordinates**

Vertices of a square of radius $R$:
- $(R, R)$
- $(-R, R)$
- $(-R, -R)$
- $(R, -R)$

---

## **3. Computational Simulation**

### **Constants**
- Amplitude $A = 1$
- Wavelength $\lambda = 1.0$ m
- Frequency $f = 1.0$ Hz
- Radius $R = 2.0$ m
- Time snapshot $t = 0$

### **Python Code Implementation**

```python
import numpy as np
import matplotlib.pyplot as plt

# Constants
A = 1
lambda_wave = 1.0
k = 2 * np.pi / lambda_wave
f = 1.0
omega = 2 * np.pi * f
R = 2.0
N = 4
t = 0

# Source positions (square)
sources = [
    (R, R),
    (-R, R),
    (-R, -R),
    (R, -R)
]

# Grid definition
x = np.linspace(-5, 5, 500)
y = np.linspace(-5, 5, 500)
X, Y = np.meshgrid(x, y)

# Initialize the sum of waves
eta_sum = np.zeros_like(X)

# Superposition principle
for (x0, y0) in sources:
    r = np.sqrt((X - x0)**2 + (Y - y0)**2)
    r = np.where(r == 0, 1e-10, r)
    eta_sum += A / np.sqrt(r) * np.cos(k * r - omega * t)

# Plotting
plt.figure(figsize=(12, 10))
plt.pcolormesh(X, Y, eta_sum, shading='auto', cmap='viridis')
plt.colorbar(label='Displacement (m)')
plt.title('Interference Pattern from Four Point Sources (Square Configuration)')
plt.xlabel('x (meters)')
plt.ylabel('y (meters)')
plt.axis('equal')
plt.show()
```

### **Grid and Calculation Details**
- The grid is composed of 500x500 points covering $[-5, 5]$ meters in both $x$ and $y$ directions.
- For each point on the grid, the displacement from each source is computed and summed.

---

## **4. Detailed Analysis of Patterns**

### **Constructive Interference**
Occurs where waves from different sources meet in phase, resulting in amplified wave heights.

### **Destructive Interference**
Occurs where waves meet out of phase, canceling each other and leading to minimal displacement.

### **Symmetry and Regularity**
- The pattern shows fourfold rotational symmetry due to the square arrangement.
- Interference fringes form a crisscross lattice structure.

### **Physical Interpretation**
- Points equidistant from multiple sources experience enhanced constructive interference.
- Nodes (points of destructive interference) appear as grid-like intersections.

### **Time Dependence**
- Though a single snapshot at $t=0$ is shown, the pattern dynamically evolves over time.
- The moving interference fringes reflect the wave's propagation.

---

## **5. Extensions and Improvements**

- **Use Different Polygons**: Try triangle, pentagon, hexagon arrangements.
- **Vary Phase**: Introduce different initial phases $\phi$ for sources.
- **Time Animation**: Animate the evolution of interference patterns.
- **Non-Coherent Sources**: Study effects of incoherence.

---

## **Conclusion**

The superposition of waves from multiple coherent sources results in complex and beautiful interference patterns. Analyzing these patterns deepens our understanding of wave behavior, such as constructive and destructive interference, and shows fundamental concepts applicable to light, sound, and water waves.

Through mathematical modeling and computational simulation, we achieved a detailed visualization of interference on a water surface. This exercise bridges theoretical physics and visual understanding, showcasing the elegance of wave phenomena.

---
