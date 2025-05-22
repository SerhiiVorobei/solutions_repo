# Problem 3: Trajectories of a Freely Released Payload Near Earth

## 🎯 Motivation

When a payload is released from a spacecraft near Earth, it may:
- Reenter the atmosphere and crash (suborbital)
- Go into stable orbit (elliptical or circular)
- Escape Earth’s gravity (hyperbolic trajectory)

The path depends on its velocity and direction at release. Understanding this is crucial for:
- Deploying satellites
- Deorbiting spacecraft
- Planning interplanetary missions

---

## 🌍 Physical Background

The payload is affected only by Earth's gravity (ignoring air resistance):

Newton’s law:

    F = G * M * m / r²

This results in an acceleration toward Earth:

    a = -G * M / r²

The trajectory depends on initial velocity vector **v₀** and position **r₀**.

---

## 🔢 Numerical Simulation (Python)

We'll simulate the motion using Euler integration.

```python
import numpy as np
import matplotlib.pyplot as plt

# Constants
G = 6.67430e-11  # m^3 kg^-1 s^-2
M = 5.972e24     # kg
R_earth = 6.371e6  # m

# Initial conditions
altitude = 400e3  # 400 km above surface (LEO)
r0 = np.array([R_earth + altitude, 0])  # initial position
v_escape = np.sqrt(2 * G * M / np.linalg.norm(r0))
v_circular = np.sqrt(G * M / np.linalg.norm(r0))

# Try different velocities
initial_velocities = {
    "Suborbital (5 km/s)": np.array([0, 5e3]),
    "Circular Orbit (~7.67 km/s)": np.array([0, v_circular]),
    "Escape (>11 km/s)": np.array([0, 11.2e3])
}

# Simulation parameters
dt = 1  # second
t_max = 6000  # simulate up to 6000 s

# Simulation loop
def simulate_trajectory(r0, v0):
    r = r0.copy()
    v = v0.copy()
    positions = []

    for _ in range(int(t_max / dt)):
        r_norm = np.linalg.norm(r)
        if r_norm <= R_earth:
            break  # hit Earth
        a = -G * M * r / r_norm**3
        v += a * dt
        r += v * dt
        positions.append(r.copy())
    return np.array(positions)

# Plotting all scenarios
plt.figure(figsize=(8, 8))
theta = np.linspace(0, 2 * np.pi, 500)
plt.plot(R_earth * np.cos(theta), R_earth * np.sin(theta), 'k', label="Earth")

for label, v0 in initial_velocities.items():
    traj = simulate_trajectory(r0, v0)
    plt.plot(traj[:, 0], traj[:, 1], label=label)

plt.gca().set_aspect('equal')
plt.title("Trajectories of Payloads Released Near Earth")
plt.xlabel("x [m]")
plt.ylabel("y [m]")
plt.legend()
plt.grid(True)
plt.tight_layout()
plt.show()
```

---

## 📊 Results and Interpretation

### 1. Suborbital (5 km/s)
- Trajectory returns to Earth.
- This is not enough for a stable orbit.
- Used in missile launches or capsule reentry.

### 2. Circular Orbit (~7.67 km/s)
- Payload maintains a stable circular orbit.
- Used for ISS and most satellites.

### 3. Escape Velocity (11.2 km/s)
- Payload follows a hyperbolic path and escapes Earth's gravity.
- Used for missions to the Moon, Mars, or beyond.

---

## 💡 Real Applications

- **Satellite Deployment:** Requires precise orbital speed for mission type.
- **Deorbit Maneuvers:** Reduce speed → payload falls to Earth.
- **Escape Missions:** Speed up to reach Moon, Mars, or leave Solar System.

---

## 🔍 Observations

- Changing only the initial speed (not direction) dramatically alters trajectory type.
- All orbits are conic sections: circle, ellipse, parabola, or hyperbola.
- Simulating numerically helps visualize real mission scenarios.

---

## 📚 References

- NASA: Basic orbital mechanics
- "Fundamentals of Astrodynamics" – Bate, Mueller, White
- Wikipedia: Trajectory (physics), Orbital mechanics

