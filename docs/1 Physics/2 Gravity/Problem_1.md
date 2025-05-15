# Orbital Period and Orbital Radius: Kepler's Third Law in Practice

## 🌌 Motivation

Kepler's Third Law reveals the elegant relationship between a planet's orbital period and its distance from the body it orbits. This law provides critical insight into the structure and behavior of planetary systems, allowing astronomers to estimate masses, distances, and even discover exoplanets. It forms a bridge between Newtonian gravity and observed celestial motions.

---

## 🔍 1. Derivation: Kepler's Third Law for Circular Orbits

### Newton's Law of Gravitation:

$F = \frac{G M m}{r^2}$

### Centripetal Force for Circular Motion:

$F = \frac{m v^2}{r}$

Equating gravitational force and centripetal force:

$\frac{G M m}{r^2} = \frac{m v^2}{r}$
$v^2 = \frac{G M}{r}$

Orbital period $T$:

$T = \frac{2\pi r}{v} \Rightarrow v = \frac{2\pi r}{T}$

Substitute into the velocity equation:

$\left( \frac{2\pi r}{T} \right)^2 = \frac{G M}{r} \Rightarrow \frac{4\pi^2 r^2}{T^2} = \frac{G M}{r}$

Rearranged:

$T^2 = \frac{4\pi^2}{G M} r^3$

### Final Form (Kepler's Third Law):

$T^2 \propto r^3$

---

## 💭 2. Implications in Astronomy

* Allows calculation of planetary distances when periods are known.
* Estimating masses of stars or planets from satellite motion.
* Used in orbital mechanics to plan space missions.

**Example: Earth's orbit**

* $T = 1$ year, $r = 1$ AU
* Any other body in the solar system follows: $T^2 / r^3 = 1$

---

## 🌍 3. Real-World Examples

### Moon Around Earth:

* Orbital radius $r \approx 3.84 \times 10^8$ m
* Period $T \approx 27.3$ days

Using Kepler's law, we can estimate Earth's mass or verify the law with actual data.

### Planets in the Solar System:

| Planet  | Radius (AU) | Period (Years) | T^2 / r^3 |
| ------- | ----------- | -------------- | --------- |
| Mercury | 0.39        | 0.24           | 1.01      |
| Venus   | 0.72        | 0.62           | 1.01      |
| Earth   | 1.00        | 1.00           | 1.00      |
| Mars    | 1.52        | 1.88           | 1.01      |
| Jupiter | 5.20        | 11.86          | 1.00      |

---

## 📈 4. Python Simulation of Circular Orbits

```python
import numpy as np
import matplotlib.pyplot as plt

G = 6.67430e-11   # gravitational constant
M = 5.972e24      # mass of Earth (kg)

radii = np.linspace(1e7, 5e8, 100)
periods = 2 * np.pi * np.sqrt(radii**3 / (G * M))

plt.plot(radii / 1e6, periods / 3600, label='T vs r (Earth orbit)')
plt.xlabel('Orbital Radius (10^6 m)')
plt.ylabel('Orbital Period (hours)')
plt.title('Orbital Period vs Radius')
plt.grid(True)
plt.legend()
plt.show()
```

### Verification of Kepler's Law:

```python
T2 = periods**2
r3 = radii**3

plt.plot(r3, T2)
plt.xlabel('r^3')
plt.ylabel('T^2')
plt.title("Kepler's Third Law: T^2 vs r^3")
plt.grid(True)
plt.show()
```

---

## 🔄 5. Extensions to Elliptical Orbits

* For elliptical orbits, $r$ is replaced by the semi-major axis $a$.
* Kepler's Law still holds: $T^2 \propto a^3$
* Applies to comets, asteroids, and binary stars.
* Used to determine masses of galaxies and detect exoplanets.

---

## ✅ Conclusion

Kepler's Third Law elegantly connects time and space for orbiting bodies. From understanding planetary motion to designing satellite systems, the relationship $T^2 \propto r^3$ is fundamental. Through derivation, application, and simulation, this project confirms the law and shows its profound relevance across astronomy and physics.

> Implemented in Python 3 using NumPy and Matplotlib for scientific visualization.
