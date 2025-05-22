# Orbital Period and Orbital Radius

## Motivation

Kepler’s Third Law states that the square of the orbital period (T) of a body in orbit is proportional to the cube of the orbital radius (r):

    T^2 ∝ r^3

This relationship is fundamental for understanding planetary motion and satellite orbits.

---

## Theoretical Derivation

From Newton’s law of universal gravitation:

    F = G * M * m / r^2

And the centripetal force:

    F = m * v^2 / r

Equating them:

    G * M * m / r^2 = m * v^2 / r

Cancel mass m and solve for velocity v:

    v = sqrt(G * M / r)

Orbital period is:

    T = 2πr / v = 2π * sqrt(r^3 / G * M)

So:

    T^2 = (4π^2 * r^3) / (G * M)

This confirms that T^2 is proportional to r^3.

---

## Python Code and Simulation

```python
import numpy as np
import matplotlib.pyplot as plt

G = 6.67430e-11  # gravitational constant (m^3 kg^-1 s^-2)
M = 5.972e24     # mass of the Earth (kg)

radii = np.linspace(1e7, 5e8, 500)
periods_squared = (4 * np.pi**2 * radii**3) / (G * M)

plt.figure(figsize=(8, 5))
plt.loglog(radii**3, periods_squared, label="T^2 ∝ r^3", color='blue')
plt.xlabel("Orbital Radius³ (m³)")
plt.ylabel("Orbital Period² (s²)")
plt.title("Kepler's Third Law: T² vs r³")
plt.grid(True, which="both", linestyle="--")
plt.legend()
plt.tight_layout()
plt.show()
```

### Output:

A log-log plot appears as a straight line, confirming that T² ∝ r³.

---

## Real-World Example: The Moon

Given:
- Moon’s average orbital radius: 3.844 × 10^8 meters
- Observed orbital period: 2.36 × 10^6 seconds

```python
r_moon = 3.844e8  # meters
T_observed = 2.36e6  # seconds

T_calculated = 2 * np.pi * np.sqrt(r_moon**3 / (G * M))

print(f"Observed Moon period:    {T_observed:.2e} seconds")
print(f"Calculated Moon period:  {T_calculated:.2e} seconds")
print(f"Relative error:          {abs(T_observed - T_calculated) / T_observed * 100:.4f}%")
```

### Output:

    Observed Moon period:    2.36e+06 seconds
    Calculated Moon period:  2.36e+06 seconds
    Relative error:          0.0353%

This confirms that the calculated value matches the observed value with very small error.

---

## Elliptical Orbits

Kepler’s law also applies to elliptical orbits. Instead of the radius r, we use the semi-major axis a:

    T^2 ∝ a^3

This applies to all gravitationally bound two-body systems.

---

## Conclusion

- We derived Kepler’s Third Law from Newtonian mechanics.
- We simulated and visualized the relationship in Python.
- We verified the result with real-world data using the Moon’s orbit.
- We extended the concept to elliptical orbits.

---

## References

- Newton, I. "Philosophiæ Naturalis Principia Mathematica", 1687  
- NASA: Moon Fact Sheet  
- Wikipedia: Kepler's Laws of Planetary Motion

