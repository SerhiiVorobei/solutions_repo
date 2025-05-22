# Interference Patterns from Point Sources on a Regular Polygon

---

## Problem Description

Interference happens when waves from multiple sources overlap, creating regions of increased (constructive) or decreased (destructive) wave amplitude.

In this project, we simulate interference patterns formed by circular waves emitted from point sources placed at the vertices of a regular polygon.

---

## Theory

Each wave from a source is described by:

\[
\eta_i(\mathbf{r}, t) = A \cos(k r_i - \omega t + \phi_i)
\]

- \(A\) = amplitude  
- \(k = \frac{2\pi}{\lambda}\) = wave number  
- \(\omega = 2\pi f\) = angular frequency  
- \(r_i\) = distance from source \(i\) to observation point \(\mathbf{r}\)  
- \(\phi_i\) = initial phase (same for all sources here)  
- \(t\) = time  

The total displacement is:

\[
\eta(\mathbf{r}, t) = \sum_{i=1}^N \eta_i(\mathbf{r}, t)
\]

---

## Python Code

```python
import numpy as np
import matplotlib.pyplot as plt

# Parameters
N = 5              # Number of sources (e.g. 5 for pentagon)
R = 5.0            # Radius of the circumscribed circle
A = 1.0            # Wave amplitude
wavelength = 2.0   # Wavelength
k = 2 * np.pi / wavelength  # Wave number
frequency = 1.0
omega = 2 * np.pi * frequency
phi = 0            # Initial phase
t = 0              # Time snapshot

# Source positions (vertices of a regular polygon)
angles = np.linspace(0, 2 * np.pi, N, endpoint=False)
sources_x = R * np.cos(angles)
sources_y = R * np.sin(angles)

# Grid for calculation
grid_size = 300
x = np.linspace(-10, 10, grid_size)
y = np.linspace(-10, 10, grid_size)
X, Y = np.meshgrid(x, y)

# Calculate total wave displacement at each point
eta_total = np.zeros_like(X)
for x_s, y_s in zip(sources_x, sources_y):
    r = np.sqrt((X - x_s)**2 + (Y - y_s)**2) + 1e-6  # Avoid division by zero
    eta_total += A * np.cos(k * r - omega * t + phi)

# Plotting
plt.figure(figsize=(10, 8))
plt.title(f'Interference Pattern from {N}-sided Polygon Sources', fontsize=16)
plt.xlabel('x')
plt.ylabel('y')
plt.pcolormesh(X, Y, eta_total, shading='auto', cmap='RdBu')
plt.colorbar(label='Wave displacement')
plt.scatter(sources_x, sources_y, c='black', s=100, label='Sources')
plt.legend()
plt.axis('equal')
plt.tight_layout()
plt.show()
