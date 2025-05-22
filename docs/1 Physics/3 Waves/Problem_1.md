# Interference Patterns from Point Sources at Vertices of a Regular Polygon

---

## Problem Description

Interference occurs when waves from different sources overlap, creating characteristic patterns of constructive and destructive interference.

In this task, we study interference patterns formed on a water surface by waves emitted from point sources located at the vertices of a regular polygon.

---

## Theory

Each circular wave emitted from a source is described by:

\[
\eta_i(\mathbf{r}, t) = A \cos(k r_i - \omega t + \phi_i)
\]

where:

- \(A\) is the wave amplitude,
- \(k = \frac{2\pi}{\lambda}\) is the wave number,
- \(\omega = 2\pi f\) is the angular frequency,
- \(r_i\) is the distance from the \(i\)-th source to point \(\mathbf{r}\),
- \(\phi_i\) is the initial phase,
- \(t\) is time.

The total displacement at point \(\mathbf{r}\) and time \(t\) is the sum of displacements from all sources:

\[
\eta(\mathbf{r}, t) = \sum_{i=1}^N \eta_i(\mathbf{r}, t)
\]

---

## Task

- Place \(N\) point wave sources at the vertices of a regular \(N\)-sided polygon.
- Calculate the interference pattern \(\eta(\mathbf{r}, t)\) over a grid.
- Visualize constructive and destructive interference zones.

---

## Python Implementation

```python
import numpy as np
import matplotlib.pyplot as plt

# Wave parameters
N = 5                      # Number of sources (vertices of the polygon)
R = 5.0                    # Radius of the circumscribed circle
A = 1.0                    # Wave amplitude
wavelength = 2.0           # Wavelength
k = 2 * np.pi / wavelength # Wave number
frequency = 1.0            # Frequency
omega = 2 * np.pi * frequency
phi = 0                    # Initial phase (same for all sources)
t = 0                      # Time (static snapshot)

# Calculate source positions (regular polygon vertices)
angles = np.linspace(0, 2 * np.pi, N, endpoint=False)
sources_x = R * np.cos(angles)
sources_y = R * np.sin(angles)

# Create a grid of points to compute the wave displacement
grid_size = 300
x = np.linspace(-10, 10, grid_size)
y = np.linspace(-10, 10, grid_size)
X, Y = np.meshgrid(x, y)

# Initialize total displacement array
eta_total = np.zeros_like(X)

# Sum wave contributions from each source
for (x_s, y_s) in zip(sources_x, sources_y):
    r = np.sqrt((X - x_s)**2 + (Y - y_s)**2) + 1e-6  # Distance (avoid division by zero)
    eta = A * np.cos(k * r - omega * t + phi)
    eta_total += eta

# Plotting the interference pattern
plt.figure(figsize=(10, 8))
plt.title(f'Interference Pattern from {N}-sided Regular Polygon Sources', fontsize=16)
plt.xlabel('x', fontsize=14)
plt.ylabel('y', fontsize=14)
plt.pcolormesh(X, Y, eta_total, shading='auto', cmap='RdBu')
plt.colorbar(label='Wave Displacement', fontsize=12)
plt.scatter(sources_x, sources_y, color='black', marker='o', s=100, label='Sources')
plt.legend(fontsize=12)
plt.axis('equal')
plt.tight_layout()
plt.show()
