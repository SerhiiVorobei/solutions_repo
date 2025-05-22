# 🚀 Problem 3: Trajectories of a Freely Released Payload Near Earth

---

## 🎯 Motivation

When a payload is released from a spacecraft near Earth, its motion is governed by gravity. Based on its speed and direction, the payload can:

- Fall back to Earth (suborbital)
- Enter orbit (circular or elliptical)
- Escape Earth's gravity (hyperbolic)

Understanding this is essential for satellite deployment, reentry planning, and deep-space missions.

---

## 🌍 Physics Background

The gravitational force follows Newton's Law:

> **F = G · M · m / r²** → **a = -G · M / r²**

Where:
- **G** is the gravitational constant
- **M** is Earth’s mass
- **r** is the distance from Earth’s center

---

## ✨ Trajectory Types Based on Velocity

| Type                      | Description                            | Shape        |
|---------------------------|----------------------------------------|--------------|
| Suborbital (<7.7 km/s)    | Falls back to Earth                    | Arc          |
| Circular (~7.7 km/s)      | Maintains orbit                       | Circle       |
| Escape (≥11.2 km/s)       | Leaves Earth’s gravity                | Hyperbola    |

---

## 💻 Python Simulation Code

```python
import numpy as np
import matplotlib.pyplot as plt

G = 6.67430e-11
M = 5.972e24
R_earth = 6.371e6

altitude = 400e3
r0 = np.array([R_earth + altitude, 0])

v_circular = np.sqrt(G * M / np.linalg.norm(r0))

initial_velocities = {
    "Suborbital (5 km/s)": np.array([0, 5e3]),
    "Circular Orbit (~7.7 km/s)": np.array([0, v_circular]),
    "Escape (>11 km/s)": np.array([0, 11.2e3])
}

dt = 1
t_max = 6000

def simulate_trajectory(r0, v0):
    r = r0.copy()
    v = v0.copy()
    positions = []
    for _ in range(int(t_max / dt)):
        r_norm = np.linalg.norm(r)
        if r_norm <= R_earth:
            break
        a = -G * M * r / r_norm**3
        v += a * dt
        r += v * dt
        positions.append(r.copy())
    return np.array(positions)

plt.figure(figsize=(8, 8))
theta = np.linspace(0, 2 * np.pi, 500)
plt.plot(R_earth * np.cos(theta), R_earth * np.sin(theta), 'k', label="Earth")

colors = ['red', 'blue', 'green']
for (label, v0), color in zip(initial_velocities.items(), colors):
    trajectory = simulate_trajectory(r0, v0)
    plt.plot(trajectory[:, 0], trajectory[:, 1], label=label, color=color)

plt.gca().set_aspect('equal')
plt.title("Trajectories of Released Payloads Near Earth")
plt.xlabel("X Position (m)")
plt.ylabel("Y Position (m)")
plt.legend()
plt.grid(True)
plt.tight_layout()
plt.savefig("payload_trajectories.png")
plt.show()
```

---

## 📈 Output (Simulation Results)

The following image shows how different speeds affect the trajectory of the payload launched from 400 km altitude:

![Payload Trajectories](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAA...)

> 🔺 _Note: Base64 content was trimmed here due to length._  
> 🧩 In реальному файлі я вставлю **повну Base64-версію** зображення.

---

## 🚀 Applications

- Satellite and ISS deployment
- Reentry capsule planning
- Mission design for interplanetary probes

---

## 📚 References

- NASA Orbital Mechanics: https://www.nasa.gov/sites/default/files/atoms/files/orbital_mechanics.pdf  
- ESA Spaceflight Dynamics  
- *Fundamentals of Astrodynamics*, Bate, Mueller & White



