# Problem 3


## **Motivation**

When a payload is released from a moving rocket near Earth, its subsequent trajectory is governed by initial conditions and gravitational forces. Analyzing these trajectories is essential for applications such as satellite deployment, re-entry missions, and understanding orbital mechanics.

---

## **1. Analysis of Possible Trajectories**

The path of a payload released near Earth can take various forms, primarily determined by its initial velocity relative to Earth's surface:

- **Elliptical Orbit:** If the payload's velocity is below Earth's escape velocity but sufficient to avoid atmospheric drag, it will enter an elliptical orbit around Earth.

- **Parabolic Trajectory:** At exactly Earth's escape velocity (~11.2 km/s), the payload will follow a parabolic trajectory, escaping Earth's gravitational influence but not entering into orbit around another body.

- **Hyperbolic Trajectory:** If the payload's velocity exceeds the escape velocity, it will follow a hyperbolic trajectory, escaping Earth's gravity with residual velocity.

- **Suborbital Trajectory:** If the velocity is insufficient to achieve orbit, the payload will follow a suborbital path, re-entering the atmosphere and impacting Earth's surface.

---

## **2. Numerical Analysis of Payload Path**

To compute the payload's trajectory, we can numerically integrate the equations of motion under Earth's gravitational field. The primary forces to consider are:

- **Gravitational Force:** Given by Newton's law of gravitation.

- **Atmospheric Drag:** Significant at lower altitudes, opposing the payload's motion.

### **Equations of Motion**

The acceleration due to gravity at a distance $r$ from Earth's center is:

$$
\mathbf{a}_g = -\frac{GM}{r^2} \hat{\mathbf{r}}
$$

The acceleration due to atmospheric drag is:

$$
\mathbf{a}_d = -\frac{1}{2} C_d \frac{\rho v^2 A}{m} \hat{\mathbf{v}}
$$

The total acceleration $\mathbf{a}$ is the sum:

$$
\mathbf{a} = \mathbf{a}_g + \mathbf{a}_d
$$

### **Python Simulation Code**

```python
import numpy as np
from scipy.integrate import solve_ivp
import matplotlib.pyplot as plt

# Constants
G = 6.67430e-11
M = 5.972e24
R = 6371e3
C_d = 2.2
A = 0.1
m = 100

def atmospheric_density(h):
    rho_0 = 1.225
    h_scale = 8500
    return rho_0 * np.exp(-h / h_scale)

def equations_of_motion(t, y):
    x, y_pos, vx, vy = y
    r = np.sqrt(x**2 + y_pos**2)
    h = r - R
    if h < 0:
        return [0, 0, 0, 0]
    v = np.sqrt(vx**2 + vy**2)
    rho = atmospheric_density(h)
    a_g = -G * M / r**2
    a_d = -0.5 * C_d * rho * v**2 * A / m
    ax = a_g * (x / r) + a_d * (vx / v)
    ay = a_g * (y_pos / r) + a_d * (vy / v)
    return [vx, vy, ax, ay]

# Initial Conditions
altitude = 400e3
speed = 7.8e3
x0 = R + altitude
y0 = 0
vx0 = 0
vy0 = speed
y0_vec = [x0, y0, vx0, vy0]
t_span = (0, 7200)

solution = solve_ivp(equations_of_motion, t_span, y0_vec, method='RK45', max_step=10)

x = solution.y[0]
y = solution.y[1]

plt.figure(figsize=(8, 8))
plt.plot(x / 1e3, y / 1e3, label='Payload Trajectory')
plt.xlabel('x (km)')
plt.ylabel('y (km)')
plt.title('Trajectory of a Freely Released Payload Near Earth')
plt.legend()
plt.grid(True)
plt.axis('equal')
plt.show()
```

---

## **3. Orbital Insertion, Re-entry, and Escape Scenarios**

- **Orbital Insertion:** Requires velocity adjustment to achieve a stable orbit.

- **Re-entry:** Occurs when velocity is too low to sustain orbit. Important for return missions.

- **Escape:** Exceeds escape velocity, used in missions targeting other celestial bodies.

---

## **4. Simulation and Visualization Tool**

This tool models payload trajectories under Earth gravity:

- Uses Newtonian mechanics and atmospheric drag
- Simulates over time with adjustable initial conditions
- Visualizes trajectory in 2D Cartesian space

This framework can be extended to:
- Include different planets
- Vary drag parameters
- Test different payload masses and speeds

---

## **Conclusion**

Understanding the trajectories of freely released payloads is fundamental for mission planning in aerospace engineering and planetary science. Through mathematical analysis and simulation, this problem offers insight into gravitational dynamics and the real-world constraints of space travel.

