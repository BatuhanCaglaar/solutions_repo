# Problem 1


# **Problem 1: Investigating the Range as a Function of the Angle of Projection**

## **Motivation**
Projectile motion is a fundamental topic in physics that provides insights into various real-world applications, such as sports, engineering, and aerospace. This study aims to analyze how the range of a projectile depends on the angle of projection, using both theoretical derivations and computational simulations.

## **Theoretical Foundation**
The equations governing projectile motion are derived from Newton's laws. The horizontal and vertical positions of the projectile at time $t$ are given by:

$$ x(t) = v_0 \cos(\theta) t $$
$$ y(t) = v_0 \sin(\theta) t - \frac{1}{2} g t^2 $$

where:
- $v_0$ is the initial velocity,
- $\theta$ is the launch angle,
- $g = 9.81 \text{ m/s}^2$ is the acceleration due to gravity.

To find the range $R$, we determine the time of flight by setting $y(t) = 0$:

$$ t_f = \frac{2 v_0 \sin(\theta)}{g} $$

Substituting into $x(t)$, the range equation is:

$$ R = \frac{v_0^2 \sin(2\theta)}{g} $$

## **Python Simulation**
The following Python script simulates projectile motion and plots the range as a function of the launch angle:

```python
import numpy as np
import matplotlib.pyplot as plt

def projectile_range(v0, theta, g=9.81):
    """
    Compute the range of a projectile given initial velocity and launch angle.
    :param v0: Initial velocity (m/s)
    :param theta: Launch angle (degrees)
    :param g: Acceleration due to gravity (m/s^2)
    :return: Range (m)
    """
    theta_rad = np.radians(theta)  # Convert angle to radians
    return (v0**2 * np.sin(2 * theta_rad)) / g

# Define parameters
v0 = 20  # Initial velocity in m/s
theta_values = np.linspace(0, 90, 100)  # Angles from 0 to 90 degrees
ranges = [projectile_range(v0, theta) for theta in theta_values]

# Plot the results
plt.figure(figsize=(8, 5))
plt.plot(theta_values, ranges, label=f'Initial velocity: {v0} m/s')
plt.xlabel('Launch Angle (degrees)')
plt.ylabel('Range (m)')
plt.title('Projectile Range as a Function of Launch Angle')
plt.legend()
plt.grid()
plt.show()
```

## **Results and Discussion**
The plot of range versus launch angle confirms that the maximum range occurs at $\theta = 45^\circ$, as predicted by the theory. Variations in initial velocity and gravitational acceleration affect the overall range but maintain the same parabolic trend.

### **Practical Applications**
- **Sports:** Optimizing throw angles in javelin and basketball.
- **Engineering:** Designing projectile-based systems such as missile trajectories.
- **Astronomy:** Predicting the motion of celestial bodies.

### **Limitations and Future Work**
- This model assumes no air resistance.
- Future work could incorporate drag force and different initial heights.


[Interact with the Projectile Motion Simulation](projectile_simulation.html)
