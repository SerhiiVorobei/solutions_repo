<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Trajectories of a Freely Released Payload Near Earth</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 40px;
            background-color: #f8f9fa;
            color: #333;
            line-height: 1.6;
        }
        h1, h2 {
            color: #2c3e50;
        }
        code {
            background: #e9ecef;
            padding: 2px 4px;
            border-radius: 4px;
            font-size: 90%;
        }
        pre {
            background-color: #e9ecef;
            padding: 10px;
            border-radius: 6px;
            overflow-x: auto;
        }
    </style>
</head>
<body>

<h1>Trajectories of a Freely Released Payload Near Earth</h1>

<h2>1. Motivation</h2>
<p>
When a payload is released from a moving spacecraft in Earth’s vicinity, the resulting path depends on the velocity vector at the moment of release. These trajectories—elliptical, parabolic, or hyperbolic—determine whether the object enters orbit, reenters Earth’s atmosphere, or escapes Earth’s gravity.
</p>
<p>
Understanding these dynamics is crucial in mission planning for satellites, space stations, and deep-space probes.
</p>

<h2>2. Physical and Mathematical Background</h2>
<p><strong>Newton's Law of Universal Gravitation:</strong></p>
<pre>F = G * M * m / r²</pre>

<p><strong>Gravitational Acceleration:</strong></p>
<pre>⃗a = -GM * ⃗r / |r|³</pre>

<ul>
    <li>G: Gravitational constant ≈ 6.674 × 10⁻¹¹ Nm²/kg²</li>
    <li>M: Mass of Earth ≈ 5.972 × 10²⁴ kg</li>
    <li>r: Distance from Earth's center</li>
</ul>

<p><strong>Total Specific Mechanical Energy:</strong></p>
<pre>ε = v²/2 − GM/r</pre>

<ul>
    <li>ε &lt; 0: Elliptical</li>
    <li>ε = 0: Parabolic</li>
    <li>ε &gt; 0: Hyperbolic</li>
</ul>

<h2>3. Numerical Simulation of Payload Trajectories</h2>
<p>Python Simulation:</p>
<pre><code>import numpy as np
import matplotlib.pyplot as plt

# Constants
G = 6.67430e-11  # m^3/kg/s^2
M_earth = 5.972e24  # kg
R_earth = 6.371e6  # m

# Function to calculate acceleration
def acceleration(r):
    norm_r = np.linalg.norm(r)
    return -G * M_earth * r / norm_r**3

# Euler's method for orbital trajectory
def simulate_trajectory(r0, v0, dt=1, t_max=10000):
    r = r0
    v = v0
    positions = [r.copy()]
    
    for _ in range(int(t_max / dt)):
        a = acceleration(r)
        v += a * dt
        r += v * dt
        positions.append(r.copy())
        if np.linalg.norm(r) < R_earth:
            break
    
    return np.array(positions)

# Initial conditions
altitude = 400e3  # 400 km
r0 = np.array([R_earth + altitude, 0])
v_circular = np.sqrt(G * M_earth / np.linalg.norm(r0))

# Try different velocities
velocity_cases = [
    ("Suborbital", v_circular * 0.9),
    ("Circular Orbit", v_circular),
    ("Elliptical Orbit", v_circular * 1.1),
    ("Escape", np.sqrt(2) * v_circular)
]

plt.figure(figsize=(10, 10))
theta = np.linspace(0, 2*np.pi, 100)
plt.plot(R_earth * np.cos(theta), R_earth * np.sin(theta), 'k', label='Earth')

for label, v0_mag in velocity_cases:
    v0 = np.array([0, v0_mag])
    traj = simulate_trajectory(r0.copy(), v0.copy(), dt=1, t_max=10000)
    plt.plot(traj[:,0], traj[:,1], label=label)

plt.axis('equal')
plt.xlabel("x [m]")
plt.ylabel("y [m]")
plt.title("Payload Trajectories Released Near Earth")
plt.legend()
plt.grid(True)
plt.show()</code></pre>

<h2>4. Interpretation of Results</h2>
<ul>
    <li><strong>Suborbital:</strong> The payload falls back to Earth, possibly reentering.</li>
    <li><strong>Circular Orbit:</strong> The payload remains in stable orbit.</li>
    <li><strong>Elliptical Orbit:</strong> The payload enters a higher apogee orbit.</li>
    <li><strong>Escape Trajectory:</strong> The payload leaves Earth’s gravitational field.</li>
</ul>

<p><strong>Escape Velocity:</strong></p>
<pre>v_esc = sqrt(2GM / r) ≈ 11.2 km/s at surface</pre>

<h2>5. Applications in Space Missions</h2>
<ul>
    <li><strong>Orbital Insertion:</strong> Payloads must match circular/elliptical criteria.</li>
    <li><strong>Reentry Capsules:</strong> Suborbital trajectories ensure atmospheric return.</li>
    <li><strong>Interplanetary Missions:</strong> Escape trajectories enable transfers to other planets.</li>
</ul>

<h2>6. Conclusion</h2>
<p>
This analysis demonstrates how classical mechanics and numerical methods provide insights into orbital dynamics. Understanding the nature of a trajectory based on velocity and position at release is fundamental in aerospace engineering and astrodynamics.
</p>

</body>
</html>
