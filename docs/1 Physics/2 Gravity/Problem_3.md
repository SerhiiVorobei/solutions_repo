# Trajectories of a Freely Released Payload Near Earth

## Motivation

When an object is released from a moving rocket near Earth, its trajectory depends on initial conditions (position, velocity, altitude) and Earth's gravitational forces. Understanding these trajectories is crucial for space missions like satellite deployment or payload return.

## Theory

The motion of a payload near Earth is governed by Newton's law of universal gravitation:

\[
\mathbf{F} = -\frac{GMm}{r^3} \mathbf{r}
\]

where:  
- \(G = 6.67430 \times 10^{-11} \, m^3\,kg^{-1}\,s^{-2}\) — gravitational constant,  
- \(M = 5.972 \times 10^{24} \, kg\) — Earth's mass,  
- \(m\) — payload mass,  
- \(\mathbf{r}\) — position vector from Earth's center,  
- \(r = |\mathbf{r}|\).

The acceleration of the payload is:

\[
\mathbf{a} = -\frac{GM}{r^3} \mathbf{r}
\]

### Types of trajectories:

- **Elliptical orbit** (\(0 \leq e < 1\)) — payload is gravitationally bound to Earth.
- **Parabolic trajectory** (\(e = 1\)) — payload travels at exactly escape velocity.
- **Hyperbolic trajectory** (\(e > 1\)) — payload escapes Earth's gravity.

---

## Numerical Simulation

To simulate the payload trajectory, we use the 4th-order Runge-Kutta (RK4) method to integrate the equations of motion numerically.

### Initial conditions:

- Initial altitude \(h\) (e.g., 200 km above Earth’s surface),
- Initial velocity magnitude \(v_0\) and launch angle \(\theta\) relative to horizontal,
- Initial position at \((R_E + h, 0)\) where \(R_E\) is Earth's radius.

---

## Python Code

```python
import numpy as np
import matplotlib.pyplot as plt

# Constants
G = 6.67430e-11        # gravitational constant, m^3/kg/s^2
M = 5.972e24           # Earth mass, kg
R_E = 6371000          # Earth radius, m

def acceleration(r):
    """Calculate gravitational acceleration at position r."""
    norm_r = np.linalg.norm(r)
    return -G * M * r / norm_r**3

def rk4_step(r, v, dt):
    """Perform one RK4 integration step."""
    k1_v = acceleration(r)
    k1_r = v
    
    k2_v = acceleration(r + 0.5 * dt * k1_r)
    k2_r = v + 0.5 * dt * k1_v
    
    k3_v = acceleration(r + 0.5 * dt * k2_r)
    k3_r = v + 0.5 * dt * k2_v
    
    k4_v = acceleration(r + dt * k3_r)
    k4_r = v + dt * k3_v
    
    r_next = r + (dt / 6) * (k1_r + 2*k2_r + 2*k3_r + k4_r)
    v_next = v + (dt / 6) * (k1_v + 2*k2_v + 2*k3_v + k4_v)
    
    return r_next, v_next

def simulate_trajectory(v0, theta_deg, h=200000, t_max=6000, dt=1):
    """
    Simulate payload trajectory near Earth.
    
    Parameters:
    v0          - initial velocity magnitude (m/s)
    theta_deg   - launch angle in degrees relative to horizontal
    h           - initial altitude (m)
    t_max       - simulation duration (s)
    dt          - timestep (s)
    
    Returns:
    numpy array of trajectory points [[x1, y1], [x2, y2], ...]
    """
    theta = np.radians(theta_deg)
    r = np.array([R_E + h, 0.0])                   # initial position vector
    v = v0 * np.array([np.cos(theta), np.sin(theta)])  # initial velocity vector
    
    trajectory = [r.copy()]
    t = 0
    
    while t < t_max:
        r, v = rk4_step(r, v, dt)
        trajectory.append(r.copy())
        t += dt
        
        # Stop if payload hits the ground
        if np.linalg.norm(r) <= R_E:
            break
    
    return np.array(trajectory)

# Example simulations:

# Three scenarios:
# 1) Sub-orbital speed (1000 m/s), 45 degrees angle
# 2) Orbital speed (~7800 m/s), horizontal (0 degrees)
# 3) Above escape velocity (~12000 m/s), horizontal (0 degrees)

params = [
    (1000, 45, 'Sub-orbital fall'),
    (7800, 0, 'Low Earth Orbit'),
    (12000, 0, 'Escape trajectory')
]

plt.figure(figsize=(10,10))
earth = plt.Circle((0, 0), R_E, color='blue', alpha=0.3, label='Earth')
plt.gca().add_artist(earth)

for v0, theta, label in params:
    traj = simulate_trajectory(v0, theta)
    plt.plot(traj[:,0], traj[:,1], label=f'{label}, v0={v0} m/s, angle={theta}°')

plt.xlabel('x (meters)')
plt.ylabel('y (meters)')
plt.title('Payload Trajectories Near Earth')
plt.legend()
plt.axis('equal')
plt.grid(True)
plt.show()
Results Explanation
At 1000 m/s and 45°, the payload falls back to Earth — velocity too low to sustain orbit.

At ~7800 m/s and 0°, the payload enters a near-circular low Earth orbit.

At ~12000 m/s and 0°, the payload escapes Earth’s gravity on a hyperbolic trajectory.

Conclusion
The initial velocity magnitude and direction determine if the payload falls, orbits, or escapes Earth.

Numerical integration with RK4 provides accurate trajectory prediction.

This model is useful for mission planning, satellite deployment, and reentry analysis.


