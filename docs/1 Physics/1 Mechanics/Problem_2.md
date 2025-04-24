# Problem 2
# 🌀 Investigation of the Dynamics of a Forced Damped Pendulum

## 📚 Theoretical Foundation

The equation of motion for a pendulum with damping and an external force is given by:

\[
\frac{d^2\theta}{dt^2} + \gamma \frac{d\theta}{dt} + \omega_0^2 \sin(\theta) = A \cos(\omega t)
\]

For small angles:  
\[
\sin(\theta) \approx \theta
\]

This allows the analysis of **damped harmonic oscillations**, **resonance**, and even **chaos** by varying parameters.

---

## 🧪 Python Model of the Pendulum

A numerical solution is obtained using the Runge-Kutta method (4th order) from the `scipy.integrate.solve_ivp` package.

Model parameters:
- γ (damping): `0.1`
- ω₀ (natural frequency): `1.5`
- A (amplitude of the external force): `1.2`
- ω (driving frequency): `2.0`

> **Code can be found in the repository or below upon request.**

---

## 📊 Visualization of Results

### 1️⃣ Angle vs Time  
![Angle vs Time](time_series_theta.png)
---

### 2️⃣ Phase Portrait  
(θ vs ω — shows the system's behavior in the state space)  
![Phase Portrait](phase_portrait.png)
---

### 3️⃣ Poincaré Section  
(Sampling the position and velocity of the pendulum at certain moments — a fractal structure appears when chaos emerges)  
![Poincaré Section](poincare_section.png)

---

## 📌 Conclusions

- The system demonstrates **various motion regimes**: regular, quasiperiodic, and chaotic.
- Under certain conditions, **resonance** occurs, increasing the amplitude.
- When changing parameters, **chaos** appears — an example of complex nonlinear dynamics.

---

## ⚙️ Applications

This model can be applied in:
- engineering (vibrations, damping),
- electronics (RLC circuits),
- biomechanics (modeling rhythmic patterns),
- energy harvesting (smoothing oscillations).

---

## 🛠 Tools

- **Python 3**
- `NumPy`, `SciPy`, `Matplotlib`
- Visual Studio Code
- Git, GitHub Pages
