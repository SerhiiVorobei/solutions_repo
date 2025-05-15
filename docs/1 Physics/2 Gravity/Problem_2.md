# Escape Velocities and Cosmic Velocities

## 🚀 Motivation

Escape velocity is fundamental for understanding how an object can break free from a celestial body's gravitational pull. Extending this concept, the **first**, **second**, and **third cosmic velocities** define the speeds needed to achieve low orbit, escape a planet entirely, or even leave a star system. These concepts are critical in space exploration, from satellite launches to interstellar travel.

---

## 1. Definitions and Physical Meaning

- **First cosmic velocity** (\(v_1\)) — the minimum speed needed for an object to maintain a stable circular orbit just above the surface of a celestial body.
- **Second cosmic velocity** (\(v_2\)) — the minimum speed to escape the gravitational field of the celestial body (escape velocity).
- **Third cosmic velocity** (\(v_3\)) — the minimum speed required to escape the gravitational influence of the star system (e.g., the Solar System).

---

## 2. Mathematical Derivations

### First Cosmic Velocity (\(v_1\))

Derived from equating centripetal force and gravitational force for a circular orbit of radius \(r\) (usually the radius of the planet):

\[
v_1 = \sqrt{\frac{G M}{r}}
\]

Where:

- \(G\) — gravitational constant,
- \(M\) — mass of the celestial body,
- \(r\) — radius from the center of the body.

---

### Second Cosmic Velocity (\(v_2\)) — Escape Velocity

Energy needed to reach infinity with zero kinetic energy:

\[
\frac{1}{2} m v_2^2 = \frac{G M m}{r} \implies v_2 = \sqrt{\frac{2 G M}{r}} = \sqrt{2} v_1
\]

---

### Third Cosmic Velocity (\(v_3\)) — Solar System Escape Velocity

Roughly the velocity needed to escape the Sun’s gravitational influence from Earth's orbit, calculated as:

\[
v_3 = \sqrt{v_2^2 + v_{\text{Earth orbit}}^2}
\]

Where:

- \(v_2\) — escape velocity from Earth,
- \(v_{\text{Earth orbit}} \approx 29.78\) km/s is Earth's orbital speed around the Sun.

---

## 3. Calculations for Different Celestial Bodies

| Body    | Mass (kg)            | Radius (m)           | \(v_1\) (km/s) | \(v_2\) (km/s) | Notes                          |
|---------|----------------------|----------------------|----------------|----------------|--------------------------------|
| Earth   | \(5.972 \times 10^{24}\) | \(6.371 \times 10^{6}\) | 7.9            | 11.2           | First and second cosmic velocities |
| Mars    | \(6.39 \times 10^{23}\)  | \(3.389 \times 10^{6}\) | 3.6            | 5.0            | Lower escape velocities          |
| Jupiter | \(1.898 \times 10^{27}\) | \(6.9911 \times 10^{7}\) | 42.1           | 59.5           | Giant planet, very high velocities |

---

## 4. Python Simulation & Visualization

```python
import numpy as np
import matplotlib.pyplot as plt

# Constants
G = 6.67430e-11  # gravitational constant, m^3/kg/s^2

# Celestial bodies data
bodies = {
    'Earth': {'mass': 5.972e24, 'radius': 6.371e6},
    'Mars': {'mass': 6.39e23, 'radius': 3.389e6},
    'Jupiter': {'mass': 1.898e27, 'radius': 6.9911e7}
}

v1_list = []
v2_list = []
names = []

for name, data in bodies.items():
    M = data['mass']
    r = data['radius']
    v1 = np.sqrt(G * M / r) / 1000  # convert to km/s
    v2 = np.sqrt(2) * v1
    v1_list.append(v1)
    v2_list.append(v2)
    names.append(name)

# Plotting
x = np.arange(len(names))
width = 0.35

fig, ax = plt.subplots()
rects1 = ax.bar(x - width/2, v1_list, width, label='First Cosmic Velocity (v1)')
rects2 = ax.bar(x + width/2, v2_list, width, label='Second Cosmic Velocity (v2)')

ax.set_ylabel('Velocity (km/s)')
ax.set_title('Cosmic Velocities for Different Celestial Bodies')
ax.set_xticks(x)
ax.set_xticklabels(names)
ax.legend()
ax.grid(True)

plt.show()

