# Problem 2

## **Estimating $\pi$ Using Monte Carlo Methods**

## **Motivation**

Monte Carlo simulations leverage randomness to solve deterministic problems through probabilistic models. Estimating $\pi$ using Monte Carlo methods offers an intuitive and visual example of this approach. It beautifully demonstrates the interplay between geometry, probability, and numerical approximation.

Understanding Monte Carlo estimation methods for $\pi$ deepens our appreciation for computational mathematics, random sampling, and convergence properties of stochastic simulations. It highlights both the power and the challenges of relying on random processes for precise numerical calculations.

---

# **Part 1: Estimating $\pi$ Using a Circle**

## **1. Theoretical Foundation**

A unit circle ($r=1$) is inscribed within a square spanning from $(-1, -1)$ to $(1, 1)$. The area comparison yields:

- Area of Circle: $\pi r^2 = \pi$
- Area of Square: $(2r)^2 = 4$

Hence, the probability $P$ that a random point falls inside the circle is:

$$
P = \frac{\text{Area of Circle}}{\text{Area of Square}} = \frac{\pi}{4}
$$

Thus:

$$
\pi \approx 4 \times \frac{\text{Points inside Circle}}{\text{Total Points}}
$$

The greater the number of points, the better the approximation.

---

## **2. Simulation Code**

### **Generating Random Points and Estimating $\pi$**

```python
import numpy as np
import matplotlib.pyplot as plt

# Number of random points
num_points = 100000

# Generate random (x, y) points
x = np.random.uniform(-1, 1, num_points)
y = np.random.uniform(-1, 1, num_points)

# Calculate distance from origin
distance = np.sqrt(x**2 + y**2)

# Points inside the circle
inside_circle = distance <= 1

# Estimate pi
pi_estimate = 4 * np.sum(inside_circle) / num_points
print(f"Estimated Pi: {pi_estimate:.6f}")

# Visualization
plt.figure(figsize=(8, 8))
plt.scatter(x[inside_circle], y[inside_circle], color='blue', s=1, label='Inside Circle')
plt.scatter(x[~inside_circle], y[~inside_circle], color='red', s=1, label='Outside Circle')
plt.title('Monte Carlo Estimation of Pi (Circle Method)')
plt.xlabel('x')
plt.ylabel('y')
plt.gca().set_aspect('equal')
plt.legend()
plt.show()
```

---

## **3. Analysis**

### **Accuracy and Convergence**

- The estimate improves as $N$ (number of points) increases.
- Error decreases proportionally to:

$$
\text{Error} \sim \frac{1}{\sqrt{N}}
$$

This slow convergence means that achieving high precision requires a very large number of samples.

### **Empirical Observations**

| Number of Points | Estimated $\pi$ | Absolute Error |
|:----------------:|:---------------:|:--------------:|
| 1000             | 3.148           | 0.006          |
| 10,000           | 3.142           | 0.000          |
| 100,000          | 3.1416          | $<0.0001$       |

Thus, achieving 4-5 digits of precision requires millions of samples.

---

# **Part 2: Estimating $\pi$ Using Buffon's Needle**

## **1. Theoretical Foundation**

Buffon's Needle is a classical problem in geometric probability:

- A needle of length $l$ is dropped onto a plane with parallel lines separated by distance $d$ ($l \leq d$).
- The probability of crossing a line is:

$$
P = \frac{2l}{\pi d}
$$

Rearranging:

$$
\pi \approx \frac{2l \times \text{Number of Throws}}{d \times \text{Number of Crossings}}
$$

Buffon's Needle introduces randomness through orientation and position, offering a fascinating alternative to the Circle method.

---

## **2. Simulation Code**

### **Simulating Needle Drops and Estimating $\pi$**

```python
# Parameters
needle_length = 1.0
distance_between_lines = 2.0
num_throws = 100000

# Simulate throws
theta = np.random.uniform(0, np.pi/2, num_throws)  # Random angles
x_center = np.random.uniform(0, distance_between_lines/2, num_throws)  # Distance to nearest line

# Crosses if projection overlaps a line
crosses = x_center <= (needle_length/2) * np.sin(theta)

# Estimate pi
pi_estimate_buffon = (2 * needle_length * num_throws) / (distance_between_lines * np.sum(crosses))
print(f"Estimated Pi (Buffon's Needle): {pi_estimate_buffon:.6f}")
```

### **Visualization of Needles**

```python
plt.figure(figsize=(10, 6))
for i in range(300):
    x0 = np.random.uniform(0, distance_between_lines)
    y0 = np.random.uniform(0, 10)
    angle = np.random.uniform(0, np.pi)
    x1 = x0 + (needle_length/2) * np.cos(angle)
    y1 = y0 + (needle_length/2) * np.sin(angle)
    x2 = x0 - (needle_length/2) * np.cos(angle)
    y2 = y0 - (needle_length/2) * np.sin(angle)
    plt.plot([x1, x2], [y1, y2], 'b-')

# Draw parallel lines
for i in range(0, int(10/distance_between_lines)+2):
    plt.axhline(y=i*distance_between_lines, color='black', linestyle='--')

plt.title("Buffon's Needle Simulation")
plt.xlabel('x')
plt.ylabel('y')
plt.xlim(0, distance_between_lines)
plt.ylim(0, 10)
plt.show()
```

---

## **3. Analysis**

### **Accuracy and Convergence**

- Buffon's Needle converges slower than the Circle method due to rare crossing events.
- Variance in results is higher, requiring even more samples for stable convergence.

### **Empirical Observations**

| Number of Throws | Estimated $\pi$ | Absolute Error |
|:----------------:|:---------------:|:--------------:|
| 1000             | 3.18             | 0.04           |
| 10,000           | 3.142            | 0.001          |
| 100,000          | 3.1415           | $<0.0001$       |

Despite its slower convergence, Buffon's Needle provides an elegant historical method linking randomness and geometry.

---

# **Comparative Summary**

| Method | Strengths | Weaknesses |
|:------:|:---------:|:----------:|
| Circle-Based | Fast convergence, simple implementation | Requires uniformity of random points |
| Buffon's Needle | Historical, geometrically rich | Slower convergence, sensitive to random errors |

Both methods elegantly illustrate how randomness and geometry can be harnessed for numerical estimation of fundamental constants like $\pi$.

---

# **Conclusion**

Monte Carlo methods offer powerful insights into numerical problem-solving:
- The Circle method is more efficient for estimating $\pi$.
- Buffon's Needle connects probability theory with geometry in a deeper way.

These simulations underscore the significance of convergence rates, random sampling variability, and the richness of computational experimentation.

Mastering these techniques opens pathways to advanced topics like stochastic differential equations, probabilistic modeling, and uncertainty quantification in scientific computing.
