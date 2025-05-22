{
 "cells": [
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# 🌌 Orbital Period and Orbital Radius\n",
    "\n",
    "## 🎯 Motivation\n",
    "Kepler’s Third Law states that the square of the orbital period $T$ of a planet is directly proportional to the cube of the semi-major axis $r$ of its orbit:\n",
    "\n",
    "$$T^2 \\propto r^3$$\n",
    "\n",
    "This relationship is instrumental in understanding planetary motion, calculating satellite trajectories, and measuring celestial distances."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## 🧠 Theoretical Derivation\n",
    "\n",
    "Starting from Newton's law of gravitation and the centripetal force:\n",
    "\n",
    "$$\\frac{G M m}{r^2} = \\frac{m v^2}{r}$$\n",
    "\n",
    "Solving for $v$ and expressing the orbital period $T = \\frac{2\\pi r}{v}$, we derive:\n",
    "\n",
    "$$T^2 = \\frac{4 \\pi^2 r^3}{G M}$$\n",
    "\n",
    "✅ Therefore, $T^2 \\propto r^3$"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": [
    "# Import libraries\n",
    "import numpy as np\n",
    "import matplotlib.pyplot as plt\n",
    "\n",
    "# Constants\n",
    "G = 6.67430e-11  # gravitational constant (m^3 kg^-1 s^-2)\n",
    "M = 5.972e24     # mass of Earth (kg)\n",
    "\n",
    "# Orbital radii (in meters)\n",
    "radii = np.linspace(1e7, 5e8, 500)\n",
    "periods_squared = (4 * np.pi**2 * radii**3) / (G * M)\n",
    "\n",
    "# Plot T^2 vs r^3\n",
    "plt.figure(figsize=(8, 5))\n",
    "plt.loglog(radii**3, periods_squared, label=r\"$T^2 \\propto r^3$\", color='royalblue')\n",
    "plt.xlabel(\"Orbital Radius$^3$ (m$^3$)\")\n",
    "plt.ylabel(\"Orbital Period$^2$ (s$^2$)\")\n",
    "plt.title(\"Kepler's Third Law Verification\")\n",
    "plt.grid(True, which='both', ls='--')\n",
    "plt.legend()\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## 🌍 Real-World Example: Moon’s Orbit Around Earth\n",
    "\n",
    "Known values:\n",
    "- Orbital radius: $r = 3.844 \\times 10^8$ m\n",
    "- Observed orbital period: $T = 2.36 \\times 10^6$ s (27.3 days)\n",
    "\n",
    "Let's verify this using the formula."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": [
    "# Moon's orbital check\n",
    "r_moon = 3.844e8  # meters\n",
    "T_observed = 2.36e6  # seconds\n",
    "T_calculated = 2 * np.pi * np.sqrt(r_moon**3 / (G * M))\n",
    "\n",
    "print(f\"Observed Moon period: {T_observed:.2e} seconds\")\n",
    "print(f\"Calculated Moon period: {T_calculated:.2e} seconds\")\n",
    "print(f\"Relative error: {abs(T_observed - T_calculated) / T_observed * 100:.4f}%\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### ✅ Conclusion\n",
    "\n",
    "- The calculated orbital period is very close to the observed value.\n",
    "- This confirms the validity of Kepler’s Third Law in real-world scenarios.\n",
    "\n",
    "$$T_{calculated} \\approx T_{observed}$$"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## 📈 Extension to Elliptical Orbits\n",
    "\n",
    "Kepler’s Third Law also applies to elliptical orbits when replacing radius $r$ with the **semi-major axis** $a$:\n",
    "\n",
    "$$T^2 \\propto a^3$$\n",
    "\n",
    "This is used for calculating the motion of planets, moons, artificial satellites, and even exoplanets."
   ]
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "name": "python"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 5
}
