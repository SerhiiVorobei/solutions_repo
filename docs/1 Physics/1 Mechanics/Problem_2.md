🎓 Investigating the Dynamics of a Forced Damped Pendulum
🔍 Motivation
The forced damped pendulum is a classic example of a nonlinear dynamical system. Due to the interplay between restoring forces, damping, and external periodic driving, it exhibits a wide range of behaviors—from simple harmonic motion to rich, chaotic dynamics.

This system models real-world phenomena such as:

Vibrating mechanical systems (e.g., bridges),

Driven electrical circuits (RLC circuits),

Human gait modeling,

Energy harvesting mechanisms.

1. 🧠 Theoretical Foundation
General Equation of Motion:
𝑓
𝑟
𝑎
𝑐
𝑑
2
𝑡
ℎ
𝑒
𝑡
𝑎
𝑑
𝑡
2
+
𝑏
𝑒
𝑡
𝑎
𝑓
𝑟
𝑎
𝑐
𝑑
𝑡
ℎ
𝑒
𝑡
𝑎
𝑑
𝑡
+
𝑜
𝑚
𝑒
𝑔
𝑎
0
2
𝑠
𝑖
𝑛
(
𝑡
ℎ
𝑒
𝑡
𝑎
)
=
𝐴
𝑐
𝑜
𝑠
(
𝑜
𝑚
𝑒
𝑔
𝑎
𝑡
)
fracd 
2
 thetadt 
2
 +
beta
fracdthetadt+
omega 
0
2
​
 
sin(
theta)=A
cos(
omegat)
Where:

𝜃
(
𝑡
)
θ(t) — angular displacement,

𝛽
β — damping coefficient,

𝜔
0
ω 
0
​
  — natural frequency of the pendulum,

𝐴
cos
⁡
(
𝜔
𝑡
)
Acos(ωt) — periodic driving force.

Small Angle Approximation:
When 
𝜃
≪
1
θ≪1, we can approximate 
sin
⁡
(
𝜃
)
≈
𝜃
sin(θ)≈θ, giving us a linear equation:

𝑓
𝑟
𝑎
𝑐
𝑑
2
𝑡
ℎ
𝑒
𝑡
𝑎
𝑑
𝑡
2
+
𝑏
𝑒
𝑡
𝑎
𝑓
𝑟
𝑎
𝑐
𝑑
𝑡
ℎ
𝑒
𝑡
𝑎
𝑑
𝑡
+
𝑜
𝑚
𝑒
𝑔
𝑎
0
2
𝑡
ℎ
𝑒
𝑡
𝑎
=
𝐴
𝑐
𝑜
𝑠
(
𝑜
𝑚
𝑒
𝑔
𝑎
𝑡
)
fracd 
2
 thetadt 
2
 +
beta
fracdthetadt+
omega 
0
2
​
 
theta=A
cos(
omegat)
The general solution includes:

A transient part (decaying oscillations),

A steady-state part (driven response).

𝜃
(
𝑡
)
=
𝑒
−
𝑓
𝑟
𝑎
𝑐
𝑏
𝑒
𝑡
𝑎
2
𝑡
𝐶
cos
⁡
(
𝑜
𝑚
𝑒
𝑔
𝑎
𝑑
𝑡
+
𝜙
)
+
𝑓
𝑟
𝑎
𝑐
𝐴
𝑠
𝑞
𝑟
𝑡
(
𝑜
𝑚
𝑒
𝑔
𝑎
0
2
−
𝑜
𝑚
𝑒
𝑔
𝑎
2
)
2
+
(
𝑏
𝑒
𝑡
𝑎
𝑜
𝑚
𝑒
𝑔
𝑎
)
2
cos
⁡
(
𝑜
𝑚
𝑒
𝑔
𝑎
𝑡
−
𝑑
𝑒
𝑙
𝑡
𝑎
)
θ(t)=e 
−fracbeta2t
 Ccos(
omega 
d
​
 t+ϕ)+
fracAsqrt(omega 
0
2
​
 −omega 
2
 ) 
2
 +(betaomega) 
2
 cos(
omegat−
delta)
2. ⚙️ Analysis of Dynamics
Parameter Effects:
Damping 
𝛽
β — suppresses motion, affects decay rate.

Driving Amplitude 
𝐴
A — larger energy input, can induce chaos.

Driving Frequency 
𝜔
ω — resonance occurs when 
𝜔
≈
𝜔
0
ω≈ω 
0
​
 .

Transition to Chaos:
At low forcing: regular oscillations,

Increasing 
𝐴
A and/or changing 
𝜔
ω: quasiperiodic or chaotic behavior.

Chaos: extreme sensitivity to initial conditions, non-repeating patterns.

3. 🛠️ Real-World Applications
This model applies to:

Suspension bridges — risk of collapse from resonance (e.g., Tacoma Narrows Bridge),

Driven RLC circuits — electrical analogs,

Energy harvesting — from ambient vibration,

Biomechanics — modeling walking or limb oscillations.

4. 💻 Python Implementation: Simulation & Visualization
Code:
python
Copy
Edit
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import solve_ivp

# Parameters
beta = 0.5       # Damping coefficient
A = 1.2          # Driving force amplitude
omega = 2/3      # Driving frequency
omega0 = 1.5     # Natural frequency

# ODE System
def pendulum(t, y):
    theta, omega_theta = y
    dydt = [omega_theta, -beta * omega_theta - omega0**2 * np.sin(theta) + A * np.cos(omega * t)]
    return dydt

# Initial conditions
y0 = [0.2, 0.0]
t_eval = np.linspace(0, 100, 5000)

# Solve ODE
sol = solve_ivp(pendulum, [0, 100], y0, t_eval=t_eval, method='RK45')

# Angular displacement over time
plt.figure(figsize=(10, 4))
plt.plot(sol.t, sol.y[0])
plt.xlabel('Time')
plt.ylabel('Angle θ (rad)')
plt.title('Forced Damped Pendulum Motion')
plt.grid(True)
plt.show()
Phase Portrait:
python
Copy
Edit
plt.figure(figsize=(6, 6))
plt.plot(sol.y[0], sol.y[1], lw=0.5)
plt.xlabel('Angle θ (rad)')
plt.ylabel('Angular Velocity')
plt.title('Phase Portrait')
plt.grid(True)
plt.show()
Poincaré Section:
python
Copy
Edit
T_drive = 2 * np.pi / omega
sampled_times = np.arange(0, 100, T_drive)
sampled_theta = np.interp(sampled_times, sol.t, sol.y[0])
sampled_omega = np.interp(sampled_times, sol.t, sol.y[1])

plt.figure(figsize=(6, 6))
plt.scatter(sampled_theta, sampled_omega, s=2)
plt.xlabel('Angle θ (rad)')
plt.ylabel('Angular Velocity')
plt.title('Poincaré Section')
plt.grid(True)
plt.show()
📈 Interpretation of Results
Regular oscillations show as smooth curves and discrete dots in Poincaré sections.

Chaotic behavior appears as scattered, unpredictable points—sign of a sensitive, nonlinear system.

The phase portrait reveals the structure of the motion (limit cycles, attractors, chaos).

Poincaré maps reduce continuous-time dynamics to a discrete map, useful for visualizing periodicity or chaos.

📌 Limitations & Extensions
Limitations:
Assumes idealized physical model (no frictional torque variations).

Sinusoidal driving force only.

Possible Extensions:
Introduce nonlinear damping (e.g., quadratic damping),

Replace cosine forcing with non-periodic or stochastic inputs,

Explore bifurcation diagrams for system behavior vs. parameter changes,

Add 3D visualizations (e.g., 
𝜃
,
𝜃
˙
,
𝑡
θ, 
θ
˙
 ,t).