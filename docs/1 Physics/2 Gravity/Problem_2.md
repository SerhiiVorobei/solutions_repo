# Problem 2
# Escape Velocities and Cosmic Velocities 🌌

## 📘 Motivation

Escape velocity determines the minimum speed required to break free from a celestial body's gravity. This idea leads to the **first**, **second**, and **third cosmic velocities** — critical for understanding orbits, escapes, and interplanetary missions.

---

## 🚀 Definitions

- **First Cosmic Velocity** — Orbital velocity: speed needed to stay in a circular orbit close to the planet's surface.
- **Second Cosmic Velocity** — Escape velocity: speed needed to leave the planet's gravitational field entirely.
- **Third Cosmic Velocity** — Interplanetary escape velocity: speed needed to leave the Solar System from Earth.

---

## 📐 Mathematical Derivations

### 1. First Cosmic Velocity \( v_1 \)

\[
v_1 = \sqrt{\frac{G M}{R}}
\]

Where:
- \( G \) = gravitational constant
- \( M \) = mass of the planet
- \( R \) = radius of the planet

---

### 2. Second Cosmic Velocity (Escape Velocity) \( v_2 \)

\[
v_2 = \sqrt{2} \cdot v_1 = \sqrt{\frac{2GM}{R}}
\]

---

### 3. Third Cosmic Velocity \( v_3 \)

Approximated from Earth's orbit around the Sun:

\[
v_3 = \sqrt{2} \cdot v_{\text{earth orbit}} \approx 42.1 \, \text{km/s}
\]

---

## 🌍 Celestial Body Parameters

We'll compare Earth, Mars, and Jupiter.

| Body     | Mass (kg)         | Radius (m)        |
|----------|-------------------|-------------------|
| Earth    | 5.972×10²⁴        | 6.371×10⁶         |
| Mars     | 6.417×10²³        | 3.390×10⁶         |
| Jupiter  | 1.898×10²⁷        | 6.991×10⁷         |

---

## 🧪 Python Simulation

```python
import numpy as np
import matplotlib.pyplot as plt

# Gravitational constant
G = 6.67430e-11  # m^3/kg/s^2

# Celestial bodies: name, mass (kg), radius (m)
bodies = {
    "Earth": (5.972e24, 6.371e6),
    "Mars": (6.417e23, 3.390e6),
    "Jupiter": (1.898e27, 6.991e7),
}

# Store results
names, v1s, v2s = [], [], []

for name, (M, R) in bodies.items():
    v1 = np.sqrt(G * M / R) / 1000     # First cosmic velocity [km/s]
    v2 = np.sqrt(2 * G * M / R) / 1000 # Second cosmic velocity [km/s]
    
    names.append(name)
    v1s.append(v1)
    v2s.append(v2)

# Plot
x = np.arange(len(names))
width = 0.35

plt.figure(figsize=(8, 5))
plt.bar(x - width/2, v1s, width, label='1st Cosmic Velocity')
plt.bar(x + width/2, v2s, width, label='2nd Cosmic Velocity')

plt.xticks(x, names)
plt.ylabel("Velocity (km/s)")
plt.title("Cosmic Velocities of Planets")
plt.legend()
plt.grid(True, axis='y')
plt.tight_layout()
plt.show()
import numpy as np

G = 6.67430e-11         # gravitational constant [m^3 kg^-1 s^-2]
M_sun = 1.989e30        # mass of the Sun [kg]
R_earth_sun = 1.496e11  # average Earth-Sun distance [m]

v3 = np.sqrt(2 * G * M_sun / R_earth_sun) / 1000  # [km/s]
print(f"Third Cosmic Velocity (from Earth orbit): {v3:.2f} km/s")
Third Cosmic Velocity (from Earth orbit): 42.12 km/s
