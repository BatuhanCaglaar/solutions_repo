# Problem 1:

## Motivation

Projectile motion, while seemingly simple, offers a rich playground for exploring fundamental principles of physics. The problem is straightforward: analyze how the range of a projectile depends on its angle of projection. However, beneath this simplicity lies a complex and versatile framework. The equations governing projectile motion involve both linear and quadratic relationships, making them accessible yet deeply insightful.

**Image: Projectile Motion Trajectory**  
![Projectile Motion Trajectory](https://upload.wikimedia.org/wikipedia/commons/6/6c/Projectile_motion_trajectory.gif)

---

## 1. Theoretical Foundation

We begin by deriving the governing equations of motion from fundamental principles. Consider a projectile launched with an initial speed \( v_0 \) at an angle \( \theta \) from the horizontal. Neglecting air resistance and assuming the launch and landing heights are equal, the equations of motion are:

$$
x(t) = v_0 \cos\theta \, t
$$

$$
y(t) = v_0 \sin\theta \, t - \frac{1}{2} g t^2
$$

To find the time of flight \( T \) (ignoring the trivial \( t = 0 \) solution), we set \( y(T) = 0 \):

$$
0 = v_0 \sin\theta \, T - \frac{1}{2} g T^2 \quad \Rightarrow \quad T = \frac{2v_0 \sin\theta}{g}
$$

The horizontal range \( R \) is then:

$$
R = v_0 \cos\theta \, T = \frac{v_0^2 \sin(2\theta)}{g}
$$

**Image: Theoretical Derivation Diagram**  
![Theoretical Derivation](https://upload.wikimedia.org/wikipedia/commons/3/32/Projectile_motion_2.svg)

Variations in the initial speed \( v_0 \) and gravitational acceleration \( g \) lead to a family of solutions, where the range \( R \) changes accordingly. For example, when \( \theta = 45^\circ \), the range is maximized.

---

## 2. Analysis of the Range

The range as a function of the launch angle is expressed as:

$$
R(\theta) = \frac{v_0^2 \sin(2\theta)}{g}
$$

- **Maximum Range:** In the absence of air resistance, the maximum range is achieved when \( \theta = 45^\circ \).
- **Effect of Parameters:**  
  - Increasing \( v_0 \) increases the range quadratically.
  - Increasing \( g \) (e.g., on a planet with stronger gravity) decreases the range.

**Image: Range vs. Angle Graph**  
![Range vs Angle](https://upload.wikimedia.org/wikipedia/commons/4/4e/Projectile_motion_horizontal_range.svg)

---

## 3. Practical Applications

This idealized model of projectile motion finds applications in numerous fields:

- **Sports:**  
  Analyzing the optimal angle for a soccer ball kick or a golf shot.
  
  **Image: Soccer Ball Trajectory**  
  ![Soccer Ball Trajectory](https://upload.wikimedia.org/wikipedia/commons/d/d5/Football_flight_path.svg)
  
- **Engineering:**  
  Designing trajectories for projectiles, such as in ballistics or space missions.
  
  **Image: Rocket Trajectory**  
  ![Rocket Trajectory](https://upload.wikimedia.org/wikipedia/commons/a/af/Launch_of_the_Saturn_V_-_full-scale_model.jpg)
  
- **Astrophysics:**  
  Understanding the effects of different gravitational fields on motion (e.g., on the Moon or Mars).

For more realistic scenarios, factors such as air resistance, wind, and uneven terrain can be incorporated using numerical methods.

---

## 4. Implementation

Below is a Python simulation that visualizes the range as a function of the launch angle. This code uses matplotlib to generate the graph.

```python
import numpy as np
import matplotlib.pyplot as plt

# Constants
g = 9.81  # Gravity (m/s^2)

def projectile_range(v0, theta_deg):
    """Calculate the horizontal range of a projectile given initial speed v0 and launch angle (degrees)."""
    theta = np.radians(theta_deg)
    return (v0**2 * np.sin(2 * theta)) / g

# Parameters
v0 = 20  # Initial speed in m/s
theta_values = np.linspace(0, 90, 180)  # Angles from 0 to 90 degrees

# Compute the range for each angle
ranges = [projectile_range(v0, theta) for theta in theta_values]

# Plot the results
plt.figure(figsize=(10, 6))
plt.plot(theta_values, ranges, label=f'v0 = {v0} m/s', color='blue')
plt.xlabel('Launch Angle (degrees)')
plt.ylabel('Range (m)')
plt.title('Projectile Range vs. Launch Angle')
plt.legend()
plt.grid(True)
plt.show()
