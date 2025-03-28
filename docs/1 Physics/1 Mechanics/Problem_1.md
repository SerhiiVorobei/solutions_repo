# Problem 1
Sure! Here's a simple solution analyzing how the range of a projectile depends on the angle of projection.

### **Step 1: Define the Range Formula**
For a projectile launched with an initial velocity \( v_0 \) at an angle \( \theta \) (assuming launch and landing at the same height), the range \( R \) is given by:

\[
R = \frac{v_0^2 \sin(2\theta)}{g}
\]

where:

- \( v_0 \) is the initial velocity,
- \( g \) is the acceleration due to gravity (≈ 9.81 m/s²),
- \( \theta \) is the launch angle.

### **Step 2: Analyze the Relationship**
- The function \( R = \sin(2\theta) \) suggests that the range depends on the sine of twice the angle.
- The maximum value of \( \sin(2\theta) \) is 1, which occurs at \( 2\theta = 90^\circ \), meaning the maximum range happens at **\( \theta = 45^\circ \)**.

### **Step 3: Special Cases**
1. **\( \theta = 0^\circ \) or \( \theta = 90^\circ \):** \( R = 0 \) (no horizontal displacement).
2. **\( \theta = 45^\circ \):** Maximum range.

### **Step 4: Visualization (Optional)**
A simple Python plot using Matplotlib can help visualize the range function:

```python
import numpy as np
import matplotlib.pyplot as plt

g = 9.81  # Gravity (m/s^2)
v0 = 10   # Initial velocity (m/s)

angles = np.linspace(0, 90, 100)  # Angle from 0 to 90 degrees
radians = np.radians(angles)  # Convert to radians
ranges = (v0**2 * np.sin(2 * radians)) / g  # Compute range

plt.plot(angles, ranges)
plt.xlabel("Launch Angle (degrees)")
plt.ylabel("Range (m)")
plt.title("Projectile Range vs. Launch Angle")
plt.grid()
plt.show()
```

### **Conclusion**
- The range is **symmetrical** around \( 45^\circ \).
- The maximum range occurs at \( 45^\circ \).
- The function follows a sine wave pattern based on \( \sin(2\theta) \).

Would you like a more detailed breakdown or a different approach? 🚀

