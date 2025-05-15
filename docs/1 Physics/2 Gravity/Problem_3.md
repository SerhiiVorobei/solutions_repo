# Trajectories of a Freely Released Payload Near Earth

## 🚀 Motivation

When an object is released from a moving rocket near Earth, its trajectory depends critically on the initial conditions (position, velocity, altitude) and Earth's gravity. The resulting motion can be elliptical (orbit), parabolic (escape trajectory), or hyperbolic (escape with excess velocity). Understanding these trajectories is essential for space missions, including satellite deployment, orbital insertion, and reentry planning.

---

## 1. Theoretical Background

### Newton’s Law of Universal Gravitation

The gravitational force acting on the payload of mass \(m\) at position vector \(\mathbf{r}\) relative to Earth's center is:

\[
\mathbf{F} = -\frac{G M_e m}{r^3} \mathbf{r}
\]

Where:

- \(G = 6.67430 \times 10^{-11} \, \text{m}^3\text{kg}^{-1}\text{s}^{-2}\) — gravitational constant,
- \(M_e = 5.972 \times 10^{24} \, \text{kg}\) — Earth's mass,
- \(r = |\mathbf{r}|\) — distance from Earth's center.

### Equation of Motion

Using Newton's second law:

\[
m \mathbf{\ddot{r}} = \mathbf{F} \implies \mathbf{\ddot{r}} = -\frac{G M_e}{r^3} \mathbf{r}
\]

This second-order vector differential equation governs the motion of the payload.

---

## 2. Types of Trajectories

The nature of the orbit depends on the total mechanical energy \(E\):

\[
E = \frac{1}{2} m v^2 - \frac{G M_e m}{r}
\]

- **Elliptical Orbit:** \(E < 0\) — payload is gravitationally bound.
- **Parabolic Trajectory:** \(E = 0\) — payload reaches escape velocity.
- **Hyperbolic Trajectory:** \(E > 0\) — payload escapes with excess kinetic energy.

---

## 3. Numerical Simulation Approach

We will:

- Use the initial position and velocity of the payload relative to Earth's center.
- Numerically integrate the equations of motion using the 4th order Runge-Kutta method via `scipy.integrate.solve_ivp`.
- Simulate the trajectory over a given time span.
- Visualize trajectories in 2D for clarity.

---

## 4. Python Implementation

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import solve_ivp

# Constants
G = 6.67430e-11          # gravitational constant, m^3/kg/s^2
M_e = 5.972e24           # Earth mass, kg
R_e = 6.371e6            # Earth radius, m

def equations(t, y):
    # y = [x, y, vx, vy]
    rx, ry, vx, vy = y
    r = np.sqrt(rx**2 + ry**2)
    
    ax = -G * M_e * rx / r**3
    ay = -G * M_e * ry / r**3
    
    return [vx, vy, ax, ay]

# Initial conditions
# Example: Payload released from 400 km altitude with initial velocity
altitude = 400e3  # 400 km above Earth's surface
initial_speed = 7800  # approx low Earth orbit speed in m/s

# Initial position (x, y)
x0 = R_e + altitude
y0 = 0.0

# Initial velocity (vx, vy)
vx0 = 0.0
vy0 = initial_speed

# Initial state vector
y0_vec = [x0, y0, vx0, vy0]

# Time span for simulation (seconds)
t_span = (0, 6000)  # simulate for 6000 seconds (~1.67 hours)
t_eval = np.linspace(*t_span, 5000)

# Solve ODE using Runge-Kutta method
sol = solve_ivp(equations, t_span, y0_vec, t_eval=t_eval, rtol=1e-9, atol=1e-9)

# Extract solution
x = sol.y[0]
y = sol.y[1]

# Earth outline for reference
theta = np.linspace(0, 2*np.pi, 100)
earth_x = R_e * np.cos(theta)
earth_y = R_e * np.sin(theta)

# Plot trajectory and Earth
plt.figure(figsize=(8,8))
plt.plot(earth_x, earth_y, 'b', label='Earth')
plt.plot(x, y, 'r', label='Payload trajectory')
plt.xlabel('x (m)')
plt.ylabel('y (m)')
plt.title('Trajectory of Payload Released Near Earth')
plt.axis('equal')
plt.grid(True)
plt.legend()
plt.show()
