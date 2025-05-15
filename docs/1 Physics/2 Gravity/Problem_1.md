Orbital Period and Orbital Radius: Kepler's Third Law in Practice

🌌 Motivation

Kepler's Third Law reveals the elegant relationship between a planet's orbital period and its distance from the body it orbits. This law provides critical insight into the structure and behavior of planetary systems, allowing astronomers to estimate masses, distances, and even discover exoplanets. It forms a bridge between Newtonian gravity and observed celestial motions.

🔍 1. Derivation: Kepler's Third Law for Circular Orbits

Newton's Law of Gravitation:



Centripetal Force for Circular Motion:



Equating gravitational force and centripetal force:




Orbital period :



Substitute into the velocity equation:



Rearranged:



Final Form (Kepler's Third Law):



💭 2. Implications in Astronomy

Allows calculation of planetary distances when periods are known.

Estimating masses of stars or planets from satellite motion.

Used in orbital mechanics to plan space missions.

Example: Earth's orbit

 year,  AU

Any other body in the solar system follows: 

🌍 3. Real-World Examples

Moon Around Earth:

Orbital radius  m

Period  days

Using Kepler's law, we can estimate Earth's mass or verify the law with actual data.

Planets in the Solar System:

Planet

Radius (AU)

Period (Years)

T^2 / r^3

Mercury

0.39

0.24

1.01

Venus

0.72

0.62

1.01

Earth

1.00

1.00

1.00

Mars

1.52

1.88

1.01

Jupiter

5.20

11.86

1.00

📈 4. Python Simulation of Circular Orbits

import numpy as np
import matplotlib.pyplot as plt

G = 6.67430e-11   # gravitational constant
M = 5.972e24      # mass of Earth (kg)

radii = np.linspace(1e7, 5e8, 100)
periods = 2 * np.pi * np.sqrt(radii**3 / (G * M))

plt.plot(radii / 1e6, periods / 3600, label='T vs r (Earth orbit)')
plt.xlabel('Orbital Radius (10^6 m)')
plt.ylabel('Orbital Period (hours)')
plt.title('Orbital Period vs Radius')
plt.grid(True)
plt.legend()
plt.show()

Verification of Kepler's Law:

T2 = periods**2
r3 = radii**3

plt.plot(r3, T2)
plt.xlabel('r^3')
plt.ylabel('T^2')
plt.title("Kepler's Third Law: T^2 vs r^3")
plt.grid(True)
plt.show()

🔄 5. Extensions to Elliptical Orbits

For elliptical orbits,  is replaced by the semi-major axis .

Kepler's Law still holds: 

Applies to comets, asteroids, and binary stars.

Used to determine masses of galaxies and detect exoplanets.

✅ Conclusion

Kepler's Third Law elegantly connects time and space for orbiting bodies. From understanding planetary motion to designing satellite systems, the relationship  is fundamental. Through derivation, application, and simulation, this project confirms the law and shows its profound relevance across astronomy and physics.