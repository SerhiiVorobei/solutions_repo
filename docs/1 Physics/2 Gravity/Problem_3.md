# 🚀 Problem 3: Trajectories of a Freely Released Payload Near Earth

---

## 🎯 Motivation

When a payload is released from a spacecraft near Earth, its motion is governed by gravity. Based on its speed and direction, the payload can:

- Fall back to Earth (suborbital)
- Enter orbit (circular or elliptical)
- Escape Earth's gravity (hyperbolic)

This is crucial for satellite deployment, reentry planning, and deep-space missions.

---

## 🌍 Physics Background

The force acting on the payload is Newton's law of gravitation:

> **F = G · M · m / r²**

Leading to the acceleration:

> **a = -G · M / r²** (toward Earth)

Where:

- G = gravitational constant
- M = Earth's mass
- r = distance from Earth’s center

The resulting **trajectory** is determined by:
- Initial position
- Initial velocity vector

---

## ✨ Types of Trajectories

| Trajectory Type   | Velocity Range                     | Shape         |
|-------------------|------------------------------------|---------------|
| Suborbital        | < Circular orbit speed (~7.7 km/s) | Arc           |
| Circular orbit    | ~7.7 km/s                          | Circle        |
| Elliptical orbit  | 7.7 – 11.2 km/s                    | Ellipse       |
| Escape trajectory | ≥ 11.2 km/s                        | Parabola / Hyperbola |

---

## 🧮 Python Code: Simulating Trajectories

```python
import numpy as np
import matplotlib.pyplot as plt

# Constants
G = 6.67430e-11         # Gravitational constant (m³/kg/s²)
M = 5.972e24            # Mass of Earth (kg)
R_earth = 6.371e6       # Radius of Earth (m)

# Initial position: 400 km above Earth
altitude = 400e3
r0 = np.array([R_earth + altitude, 0])

# Velocity options
v_circular = np.sqrt(G * M / np.linalg.norm(r0))
v_escape = np.sqrt(2 * G * M / np.linalg.norm(r0))

initial_velocities = {
    "Suborbital (5 km/s)": np.array([0, 5e3]),
    "Circular Orbit (~7.7 km/s)": np.array([0, v_circular]),
    "Escape (>11 km/s)": np.array([0, 11.2e3])
}

# Simulation parameters
dt = 1         # time step (s)
t_max = 6000   # total time (s)

def simulate_trajectory(r0, v0):
    r = r0.copy()
    v = v0.copy()
    positions = []

    for _ in range(int(t_max / dt)):
        r_norm = np.linalg.norm(r)
        if r_norm <= R_earth:
            break  # impact with Earth
        a = -G * M * r / r_norm**3
        v += a * dt
        r += v * dt
        positions.append(r.copy())
    return np.array(positions)

# Plotting
plt.figure(figsize=(8, 8))
theta = np.linspace(0, 2 * np.pi, 500)
plt.plot(R_earth * np.cos(theta), R_earth * np.sin(theta), 'k', label="Earth")

for label, v0 in initial_velocities.items():
    trajectory = simulate_trajectory(r0, v0)
    plt.plot(trajectory[:, 0], trajectory[:, 1], label=label)

plt.gca().set_aspect('equal')
plt.title("Trajectories of Released Payloads")
plt.xlabel("X Position (m)")
plt.ylabel("Y Position (m)")
plt.legend()
plt.grid(True)
plt.tight_layout()
plt.show()
```

---

## 📊 Output Summary

**Initial Altitude:** 400 km  
**Gravitational body:** Earth

### Results by Velocity:

#### 🔻 Suborbital (5 km/s)
- Result: Payload crashes into Earth.
- Application: Capsules, test flights, missiles.

#### 🛰️ Circular Orbit (~7.7 km/s)
- Result: Payload remains in a low Earth orbit.
- Application: Satellites, ISS.

#### 🛸 Escape Trajectory (11.2 km/s)
- Result: Payload escapes Earth's gravity.
- Application: Lunar missions, probes to Mars or outer planets.

---

## 🌌 Discussion

This simulation demonstrates how **small differences in initial speed** radically alter the trajectory:

- **Too slow** → crash.
- **Precise** → orbit.
- **Too fast** → escape.

These principles are used for:
- Launch window planning
- Mission trajectory design
- Ensuring spacecraft don't reenter prematurely

---

## 🔬 Further Improvements

- Add air resistance for reentry realism
- Simulate using Runge-Kutta (RK4) for higher accuracy
- Vary release angle to analyze direction effects

---

## 📚 References

- NASA Orbital Mechanics: https://www.nasa.gov/sites/default/files/atoms/files/orbital_mechanics.pdf  
- ESA Spaceflight Dynamics Guide  
- Bate, Mueller & White – *Fundamentals of Astrodynamics*

