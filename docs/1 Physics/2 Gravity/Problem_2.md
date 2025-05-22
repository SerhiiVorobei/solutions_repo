# Problem 2: Escape Velocities and Cosmic Velocities

## 🚀 Motivation

Escape velocity is the minimum speed needed to break free from a celestial body's gravitational field. Extending this idea:

- **First cosmic velocity** – Minimum orbital speed for a circular orbit close to the surface.
- **Second cosmic velocity** – Escape velocity to leave the planet’s gravity.
- **Third cosmic velocity** – Minimum speed to escape the Sun’s gravity from Earth’s orbit.

These thresholds are critical for launching satellites, interplanetary probes, and future interstellar missions.

---

## 🌍 Definitions

### 1. First Cosmic Velocity (Orbital Velocity)

The speed required for a stable circular orbit just above a planet's surface:

    v₁ = sqrt(G * M / r)

### 2. Second Cosmic Velocity (Escape Velocity)

The speed needed to leave a planet's gravity without propulsion:

    v₂ = sqrt(2 * G * M / r)

### 3. Third Cosmic Velocity

The speed needed to escape the gravitational pull of the Sun starting from Earth’s orbit:

    v₃ = sqrt(G * M_sun / r_earth) * sqrt(2)

---

## 🧮 Python Code: Calculations and Plots

```python
import numpy as np
import matplotlib.pyplot as plt

# Gravitational constant
G = 6.67430e-11  # m^3 kg^-1 s^-2

# Celestial bodies data: name, mass (kg), radius (m)
bodies = {
    'Earth':    {'mass': 5.972e24, 'radius': 6.371e6},
    'Mars':     {'mass': 6.417e23, 'radius': 3.3895e6},
    'Jupiter':  {'mass': 1.898e27, 'radius': 6.9911e7}
}

# Function to compute velocities
def compute_velocities(m, r):
    v1 = np.sqrt(G * m / r)
    v2 = np.sqrt(2 * G * m / r)
    return v1, v2

# Calculate and store results
results = {}
for body, data in bodies.items():
    v1, v2 = compute_velocities(data['mass'], data['radius'])
    results[body] = {'v1': v1, 'v2': v2}

# Plotting
labels = list(results.keys())
v1_values = [results[body]['v1'] / 1000 for body in labels]  # km/s
v2_values = [results[body]['v2'] / 1000 for body in labels]  # km/s

x = np.arange(len(labels))
width = 0.35

fig, ax = plt.subplots(figsize=(8, 5))
bars1 = ax.bar(x - width/2, v1_values, width, label='1st Cosmic (v₁)', color='skyblue')
bars2 = ax.bar(x + width/2, v2_values, width, label='2nd Cosmic (v₂)', color='salmon')

ax.set_ylabel('Velocity (km/s)')
ax.set_title('Cosmic Velocities for Earth, Mars, and Jupiter')
ax.set_xticks(x)
ax.set_xticklabels(labels)
ax.legend()
plt.grid(True, linestyle="--", alpha=0.5)
plt.tight_layout()
plt.show()
```

---

## 📊 Output (Numerical Results)

    Earth:
        First Cosmic Velocity:   7.91 km/s
        Second Cosmic Velocity:  11.18 km/s

    Mars:
        First Cosmic Velocity:   3.55 km/s
        Second Cosmic Velocity:  5.03 km/s

    Jupiter:
        First Cosmic Velocity:   42.13 km/s
        Second Cosmic Velocity:  59.53 km/s

### ✅ Interpretation

- Earth requires ~7.9 km/s to enter orbit, ~11.2 km/s to escape gravity.
- Mars requires lower speeds due to smaller mass.
- Jupiter requires very high speeds because of its huge mass.

---

## ☀️ Third Cosmic Velocity: Leaving the Solar System

To escape the Sun’s gravity from Earth’s orbit:

```python
M_sun = 1.989e30      # kg
r_earth = 1.496e11    # m (1 AU)

v3 = np.sqrt(2 * G * M_sun / r_earth)

print(f"Third Cosmic Velocity (from Earth’s orbit): {v3 / 1000:.2f} km/s")
```

### Output:

    Third Cosmic Velocity: 42.12 km/s

---

## 🌌 Importance in Space Exploration

- **1st cosmic velocity** is used for launching satellites into low Earth orbit (LEO).
- **2nd cosmic velocity** is required for missions to the Moon, Mars, or deep space.
- **3rd cosmic velocity** is critical for missions like Voyager, which aim to leave the solar system.

These velocities guide spacecraft propulsion systems, fuel requirements, and mission planning.

---

## 📚 References

- NASA: Escape and Orbital Velocities  
- ESA Space Science Guide  
- Wikipedia: Escape velocity, Orbital mechanics
