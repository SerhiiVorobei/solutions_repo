# Investigating the Dynamics of a Forced Damped Pendulum

## 🎯 Motivation

The forced damped pendulum is a classic nonlinear system exhibiting rich behavior—from simple oscillations to chaos. Understanding this system allows us to explore mechanical resonance, nonlinear dynamics, and real-world systems like suspension bridges and electrical circuits.

---

## 📘 1. Theoretical Background

### Equation of Motion

\[
\frac{d^2\theta}{dt^2} + \beta \frac{d\theta}{dt} + \omega_0^2 \sin(\theta) = A \cos(\omega t)
\]

Where:

- \( \theta(t) \): angle,
- \( \beta \): damping coefficient,
- \( \omega_0 \): natural frequency,
- \( A \): driving amplitude,
- \( \omega \): driving frequency.

---

### Small-Angle Approximation

For small \( \theta \), we use \( \sin(\theta) \approx \theta \):

\[
\frac{d^2\theta}{dt^2} + \beta \frac{d\theta}{dt} + \omega_0^2 \theta = A \cos(\omega t)
\]

General solution:

\[
\theta(t) = e^{-\frac{\beta}{2}t}C \cos(\omega_d t + \phi) + \frac{A}{\sqrt{(\omega_0^2 - \omega^2)^2 + (\beta \omega)^2}} \cos(\omega t - \delta)
\]

---

## 🔍 2. Dynamics Analysis

- **Damping \( \beta \)**: reduces amplitude over time.
- **Driving amplitude \( A \)**: larger amplitude increases energy.
- **Driving frequency \( \omega \)**: resonance occurs near \( \omega_0 \).

**At high amplitudes or specific frequencies, chaos can emerge.**

---

## 🏗️ 3. Real-World Applications

- **Suspension bridges** — avoid resonance (e.g., Tacoma Narrows Bridge).
- **Oscillating RLC circuits** — exact analogs of this system.
- **Human biomechanics** — models for walking and limb movement.
- **Energy harvesting** — from vibrations using piezoelectric materials.

---

## 💻 4. Python Simulation

### Parameters:

```python
beta = 0.5       # damping
A = 1.2          # driving amplitude
omega = 2/3      # driving frequency
omega0 = 1.5     # natural frequency
ODE Definition & Solver:
python
Copy
Edit
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import solve_ivp

def pendulum(t, y):
    theta, omega_theta = y
    return [omega_theta, -beta * omega_theta - omega0**2 * np.sin(theta) + A * np.cos(omega * t)]

y0 = [0.2, 0.0]
t_eval = np.linspace(0, 100, 5000)

sol = solve_ivp(pendulum, [0, 100], y0, t_eval=t_eval)
Plotting Motion:
python
Copy
Edit
plt.plot(sol.t, sol.y[0])
plt.title('Angle θ vs Time')
plt.xlabel('Time')
plt.ylabel('θ (rad)')
plt.grid(True)
plt.show()
Phase Portrait:
python
Copy
Edit
plt.plot(sol.y[0], sol.y[1])
plt.title('Phase Portrait')
plt.xlabel('θ')
plt.ylabel('dθ/dt')
plt.grid(True)
plt.show()
Poincaré Section:
python
Copy
Edit
T_drive = 2 * np.pi / omega
sample_times = np.arange(0, 100, T_drive)
theta_samples = np.interp(sample_times, sol.t, sol.y[0])
omega_samples = np.interp(sample_times, sol.t, sol.y[1])

plt.scatter(theta_samples, omega_samples, s=2)
plt.title('Poincaré Section')
plt.xlabel('θ')
plt.ylabel('dθ/dt')
plt.grid(True)
plt.show()
📊 5. Interpretation
Low amplitude: periodic oscillations.

Medium: possible resonance.

High: chaotic, unpredictable motion.

Poincaré sections and phase diagrams visually confirm this.

🧪 6. Limitations & Extensions
Limitations:

Assumes perfect damping and sinusoidal force.

Real systems have friction and complex boundaries.

Extensions:

Add nonlinear damping (e.g., air drag).

Use random or aperiodic driving.

Plot bifurcation diagrams with changing 
𝐴
A.

✅ Conclusion
The forced damped pendulum is a rich, educational system for exploring regular and chaotic motion. This project bridges theory and simulation, providing both conceptual and practical understanding of nonlinear dynamics.