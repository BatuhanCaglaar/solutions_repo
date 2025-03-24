# Problem 1

## Investigating the Range as a Function of the Angle of Projection

### Motivation
Projectile motion, while seemingly simple, offers a rich playground for exploring fundamental principles of physics. The problem is straightforward: analyze how the range of a projectile depends on its angle of projection. Yet, beneath this simplicity lies a complex and versatile framework. The equations governing projectile motion involve both linear and quadratic relationships, making them accessible yet deeply insightful.

What makes this topic particularly compelling is the number of free parameters involved in these equations, such as initial velocity, gravitational acceleration, and launch height. These parameters give rise to a diverse set of solutions that can describe a wide array of real-world phenomena, from the arc of a soccer ball to the trajectory of a rocket.

## 1. Theoretical Foundation

Projectile motion is governed by Newton’s Second Law. Considering only gravitational acceleration and assuming no air resistance, the equations of motion are derived as follows:

Newton’s Second Law:

$$ \mathbf{F} = m\mathbf{a} $$

With gravity as the only force:

$$ \mathbf{F} = -mg\hat{j}, \quad \mathbf{a} = -g\hat{j}. $$

Breaking into components:

$$ a_x = 0, \quad a_y = -g. $$

Integrating to find velocity:

$$ v_x = v_0 \cos\theta, \quad v_y = v_0 \sin\theta - gt. $$

Integrating again to find position:

$$ x(t) = v_0 \cos\theta \cdot t, $$

$$ y(t) = v_0 \sin\theta \cdot t - \frac{1}{2} g t^2. $$

The time of flight (when $ y = 0 $) is:

$$ T = \frac{2 v_0 \sin\theta}{g}. $$

Thus, the range $ R $ is:

$$ R = \frac{v_0^2 \sin 2\theta}{g}. $$

## 2. Analysis of the Range

The range depends on the launch angle $ \theta $, initial velocity $ v_0 $, and gravitational acceleration $ g $. The maximum range occurs when:

$$ \theta = 45^\circ. $$

To investigate further, let's implement a computational approach.

## 3. Implementation

The following Python script simulates projectile motion and plots the range as a function of launch angle:

```python
import numpy as np
import matplotlib.pyplot as plt

def projectile_range(v0, g):
    angles = np.linspace(0, 90, num=100)  # Angles from 0 to 90 degrees
    ranges = (v0**2 * np.sin(2 * np.radians(angles))) / g
    
    plt.figure(figsize=(8, 5))
    plt.plot(angles, ranges, label="Range vs. Angle", color='b')
    plt.axvline(x=45, linestyle='--', color='r', label='Max Range at 45°')
    plt.xlabel("Launch Angle (degrees)")
    plt.ylabel("Range (m)")
    plt.title("Projectile Range as a Function of Launch Angle")
    plt.legend()
    plt.grid()
    plt.show()

# Example usage
projectile_range(v0=20, g=9.81)
```

## 4. Practical Applications

This model applies to various real-world situations:
- **Sports:** Understanding projectile motion helps optimize the trajectory of balls in soccer, basketball, and golf.
- **Engineering:** Designing artillery shells and missiles for maximum range.
- **Aerospace:** Calculating flight paths and rocket launches.

## 5. Limitations and Improvements

- The model assumes no air resistance. In reality, drag and wind can significantly alter the projectile's path.
- Uneven terrain affects landing position and range.
- Real-world applications require computational fluid dynamics for more accurate predictions.

### Conclusion
The projectile motion equations provide a deep understanding of how range varies with launch angle. The computational model visually confirms that maximum range occurs at $ 45^\circ $. Future improvements could include drag forces for more realistic simulations.
