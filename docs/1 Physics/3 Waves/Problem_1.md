# 🌊 Interference Patterns on a Water Surface

## Motivation
Interference patterns provide a vivid, intuitive view of wave behavior. On a water surface, these patterns arise when waves from different sources overlap. The resulting pattern reveals how waves interact constructively or destructively depending on their relative phases and distances. This simple yet powerful model helps us grasp key concepts of wave physics.

---

## 🔧 Problem Setup

### Regular Polygon Selection
We choose a **regular pentagon** (5-sided polygon) for placing our wave sources.

### Parameters
- **Amplitude (A):** 1.0  
- **Wavelength (λ):** 1.0 unit  
- **Frequency (f):** 1.0 Hz  
- **Wave number (k):** \( k = \frac{2\pi}{\lambda} \)  
- **Angular frequency (ω):** \( \omega = 2\pi f \)  
- **Phase (ϕ):** 0 (coherent sources)

---

## 🧮 Wave Equation

For a single source at location \(\vec{r}_i = (x_i, y_i)\), the wave displacement at point \(\vec{r} = (x, y)\) and time \(t\) is:

\[
\psi_i(x, y, t) = A \cdot \cos(k d_i - \omega t + \phi)
\]

where:
- \(d_i = \sqrt{(x - x_i)^2 + (y - y_i)^2}\)

The total wave displacement from all sources is:

\[
\Psi(x, y, t) = \sum_{i=1}^{N} \psi_i(x, y, t)
\]

---

## 🧑‍💻 Python Simulation Code

```python
import numpy as np
import matplotlib.pyplot as plt

# Parameters
A = 1.0
wavelength = 1.0
k = 2 * np.pi / wavelength
f = 1.0
omega = 2 * np.pi * f
phi = 0
N_sources = 5  # regular pentagon

# Time snapshot
t = 0.0

# Grid
x = np.linspace(-5, 5, 500)
y = np.linspace(-5, 5, 500)
X, Y = np.meshgrid(x, y)

# Position sources at vertices of a regular pentagon
radius = 2.0
angles = np.linspace(0, 2*np.pi, N_sources, endpoint=False)
source_positions = [(radius * np.cos(a), radius * np.sin(a)) for a in angles]

# Superpose waves from all sources
Z = np.zeros_like(X)

for (x0, y0) in source_positions:
    R = np.sqrt((X - x0)**2 + (Y - y0)**2)
    Z += A * np.cos(k * R - omega * t + phi)

# Visualization
plt.figure(figsize=(8, 6))
plt.contourf(X, Y, Z, levels=100, cmap='viridis')
plt.colorbar(label='Wave Displacement')
plt.scatter(*zip(*source_positions), color='red', label='Sources')
plt.title('Interference Pattern from 5 Point Sources (Pentagon)')
plt.xlabel('x')
plt.ylabel('y')
plt.legend()
plt.axis('equal')
plt.show()
```

---

## 🔍 Analysis of Interference Patterns

### Constructive Interference
Occurs where the waves from all sources arrive **in phase** — seen as bright (high-displacement) fringes.

### Destructive Interference
Occurs where the waves are **out of phase** — seen as dark (low-displacement) regions.

### Symmetry Observed
The pattern has **pentagonal symmetry**, reflecting the geometry of the source configuration. Regions of symmetry correspond to central lines between source pairs.

---

## 📈 Conclusion

This simulation of interference patterns from point sources arranged in a regular pentagon reveals:
- **Radial and angular symmetries** matching the source geometry.
- **Rich, periodic structures** caused by constructive and destructive interference.
- **A powerful way to explore wave superposition**, using a visually intuitive and computationally accessible method.


