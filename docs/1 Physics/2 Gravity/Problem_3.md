# 🚀 Problem 3: Trajectories of a Freely Released Payload Near Earth

## 🎯 Motivation

When an object is released from a moving rocket near Earth, its trajectory depends on initial conditions and gravitational forces. This is essential for understanding reentry, orbital insertion, or escape during space missions.

## 📚 Theoretical Background

We analyze the motion using Newton's Law of Gravitation:

F = GMm / r²


And the resulting acceleration in 2D space:

aₓ = -GMx / r³, aᵧ = -GMy / r³


Different initial velocities lead to various types of trajectories:

- **Suborbital (Reentry)** – The object falls back to Earth.
- **Elliptical Orbit** – A stable, closed orbital path.
- **Circular Orbit** – A special case of elliptical with constant radius.
- **Escape Trajectory** – The object leaves Earth's gravity field.
- **Hyperbolic Path** – A faster-than-escape velocity trajectory.

## 🧮 Python Simulation

Below is a Python script that simulates the motion using numerical integration:

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import solve_ivp

# Constants
G = 6.67430e-11
M = 5.972e24
R_earth = 6.371e6
mu = G * M

def equations(t, y):
    x, vx, y_pos, vy = y
    r = np.sqrt(x**2 + y_pos**2)
    ax = -mu * x / r**3
    ay = -mu * y_pos / r**3
    return [vx, ax, vy, ay]

def simulate_trajectory(r0, v0, t_max=20000, dt=10):
    y0 = [r0[0], v0[0], r0[1], v0[1]]
    t_span = (0, t_max)
    t_eval = np.arange(0, t_max, dt)
    sol = solve_ivp(equations, t_span, y0, t_eval=t_eval, rtol=1e-8)
    return sol

# Initial position (300 km above Earth)
altitude = 300e3
r0 = [R_earth + altitude, 0]

# Velocities
v_circular = np.sqrt(mu / np.linalg.norm(r0))
v_escape = np.sqrt(2) * v_circular

velocities = {
    "Suborbital (Reentry)": [0.7 * v_circular, 0],
    "Circular Orbit": [0, v_circular],
    "Escape Trajectory": [0, v_escape],
    "Elliptical Orbit": [0, 0.9 * v_circular],
    "Hyperbolic Path": [0, 1.5 * v_circular]
}

plt.figure(figsize=(10, 10))

for label, v0 in velocities.items():
    sol = simulate_trajectory(r0, v0)
    x, y = sol.y[0], sol.y[2]
    plt.plot(x / 1000, y / 1000, label=label)

# Draw Earth
theta = np.linspace(0, 2 * np.pi, 1000)
earth_x = R_earth * np.cos(theta) / 1000
earth_y = R_earth * np.sin(theta) / 1000
plt.plot(earth_x, earth_y, 'k', linewidth=2)
plt.fill(earth_x, earth_y, 'lightblue', label="Earth")

plt.xlabel("x (km)")
plt.ylabel("y (km)")
plt.title("Payload Trajectories Near Earth")
plt.axis("equal")
plt.grid(True)
plt.legend()
plt.tight_layout()
plt.savefig("trajectory.png")
plt.show()

🖼️ Resulting Trajectories

The graph below shows the various paths the payload can follow depending on its initial velocity and direction:

📊 Interpretation of Results

    Reentry: Below orbital speed – crashes back to Earth.

    Stable Orbit: At circular or elliptical speeds.

    Escape: Above escape velocity – leaves Earth's gravity.

    Hyperbolic: A steep trajectory, fast exit.

🛰️ Applications

    Space capsule reentry and safety

    Satellite deployment strategies

    Designing interplanetary missions

    Avoiding orbital debris