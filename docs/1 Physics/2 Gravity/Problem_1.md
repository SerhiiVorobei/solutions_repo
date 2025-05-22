# 🌌 Orbital Period and Orbital Radius

## 🎯 Motivation

Kepler’s Third Law states that the square of the orbital period \( T \) of a planet is directly proportional to the cube of the semi-major axis \( r \) of its orbit:

\[
T^2 \propto r^3
\]

This relationship is crucial for understanding planetary motion, satellite orbits, and distances in astronomy.

---

## 🧠 Theoretical Derivation

Starting from Newton's Law of Universal Gravitation and the formula for centripetal force:

\[
\frac{G M m}{r^2} = \frac{m v^2}{r}
\]

Canceling \( m \), solving for orbital velocity \( v \), and expressing the orbital period \( T = \frac{2\pi r}{v} \), we get:

\[
T^2 = \frac{4\pi^2 r^3}{GM}
\]

✅ Therefore, \( T^2 \propto r^3 \)

---

## 🧪 Python Simulation of Circular Orbits

```python
import numpy as np
import matplotlib.pyplot as plt

# Constants
G = 6.67430e-11  # gravitational constant (m^3 kg^-1 s^-2)
M = 5.972e24     # mass of Earth (kg)

# Range of orbital radii
radii = np.linspace(1e7, 5e8, 500)
periods_squared = (4 * np.pi**2 * radii**3) / (G * M)

# Plot T^2 vs r^3 (log-log)
plt.figure(figsize=(8, 5))
plt.loglog(radii**3, periods_squared, label=r"$T^2 \propto r^3$", color="royalblue")
plt.xlabel("Orbital Radius³ (m³)")
plt.ylabel("Orbital Period² (s²)")
plt.title("Kepler's Third Law Verification")
plt.grid(True, which="both", linestyle="--", alpha=0.7)
plt.legend()
plt.tight_layout()
plt.show()

