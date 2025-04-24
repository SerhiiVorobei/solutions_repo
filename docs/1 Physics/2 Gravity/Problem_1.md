# Problem 1
# Orbital Period and Orbital Radius – Kepler's Third Law

## 📘 Motivation

Kepler's Third Law reveals the relationship between a celestial body's orbital period and its distance from the central mass. This law not only predicts how planets and satellites move but also helps astronomers measure mass and distance across the universe.

---

## 📐 Derivation of the Law (Circular Orbits)

Using Newton's law of gravitation and the formula for centripetal force:

\[
\frac{G M m}{r^2} = \frac{m v^2}{r}
\]

Solving for orbital speed \( v \):

\[
v = \sqrt{\frac{G M}{r}}
\]

Now the orbital period \( T \):

\[
T = \frac{2\pi r}{v} = 2\pi \sqrt{\frac{r^3}{G M}}
\]

Squaring both sides:

\[
T^2 = \frac{4\pi^2}{G M} r^3
\]

---

## 🔭 Applications in Astronomy

- Calculate mass of planets/stars from satellite orbits
- Estimate distances of celestial bodies
- Universal law: applies to satellites, moons, planets, exoplanets, binary stars

---

## 🌍 Example: Moon Orbit

- Radius ≈ 384,400 km  
- Period ≈ 27.3 days  
- \( T^2 \propto r^3 \) holds true

---

## 🧪 Simulation in Python

```python
import numpy as np
import matplotlib.pyplot as plt

# Constants
G = 6.67430e-11  # m^3 kg^-1 s^-2
M_earth = 5.972e24  # kg

# Function to compute orbital period
def orbital_period(r, M=M_earth):
    return 2 * np.pi * np.sqrt(r**3 / (G * M))

# Radii (m)
radii = np.linspace(1e7, 5e8, 100)
periods = orbital_period(radii)

# Plotting T² vs r³
plt.figure(figsize=(8, 6))
plt.plot(radii**3, periods**2)
plt.xlabel("Orbital Radius Cubed (r³) [m³]")
plt.ylabel("Orbital Period Squared (T²) [s²]")
plt.title("Kepler's Third Law: T² vs r³")
plt.grid(True)
plt.show()
