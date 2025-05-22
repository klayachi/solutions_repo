
# Problem 3
# Trajectories of a Freely Released Payload Near Earth

## 1. Introduction

When a payload is released from a spacecraft near Earth, its path is no longer dictated by propulsion but solely by gravitational interaction. The resulting trajectory—whether an orbital arc, escape route, or reentry—depends on the initial conditions at the moment of release. This investigation explores the governing dynamics, equations, and possible paths, providing essential context for space engineering and mission design.

---

## 2. Gravitational Dynamics and Force Model

### 2.1 Newton’s Law of Universal Gravitation

The gravitational force acting on a payload of mass $m$ near Earth is:

$$
\vec{F} = -\frac{G M m}{r^2} \hat{r}
$$

Where:
- $G = 6.674 \times 10^{-11} \, \text{m}^3/\text{kg} \cdot \text{s}^2$ — gravitational constant  
- $M$ — mass of the Earth ($5.972 \times 10^{24} \text{ kg}$)  
- $r$ — distance from Earth’s center  
- $\hat{r}$ — unit vector directed radially from Earth

### 2.2 Equations of Motion

Using Newton’s second law:

$$
m \vec{a} = -\frac{G M m}{r^2} \hat{r} \Rightarrow \vec{a} = -\frac{G M}{r^2} \hat{r}
$$

In Cartesian coordinates:

$$
\vec{a} = -\frac{G M}{(x^2 + y^2)^{3/2}} \begin{bmatrix} x \\ y \end{bmatrix}
$$

---

## 3. Energy-Based Trajectory Classification

The type of path followed by the object is determined by its total mechanical energy:

$$
E = \frac{1}{2} m v^2 - \frac{G M m}{r}
$$

### 3.1 Parabolic (E = 0)

The velocity equals the escape velocity:

$$
v = v_{\text{esc}} = \sqrt{\frac{2 G M}{r}}
$$

### 3.2 Elliptical (E < 0)

Bound orbit (closed), energy negative:

$$
v = \sqrt{ G M \left( \frac{2}{r} - \frac{1}{a} \right) }
$$

Where $a$ is the semi-major axis of the ellipse.

### 3.3 Hyperbolic (E > 0)

Escape trajectory, object never returns:

$$
v = \sqrt{ G M \left( \frac{2}{r} + \frac{1}{|a|} \right) }
$$

Where $a$ is negative for hyperbolic trajectories.

---

## 4. Numerical Method – Runge-Kutta 4th Order

The 4th-order Runge-Kutta (RK4) method is used to solve the system:

\[
\frac{d^2\vec{r}}{dt^2} = -\frac{GM}{||\vec{r}||^3} \vec{r}
\]

Simulating trajectories involves computing the object's position at each time step based on its gravitational acceleration and velocity using RK4.

---

## 5. Python Simulation of Parabolic, Elliptical, and Hyperbolic Paths

```python
import numpy as np
import matplotlib.pyplot as plt

G = 6.674e-11
M = 5.972e24
R_earth = 6.371e6

def acceleration(r):
    norm = np.linalg.norm(r)
    return -G * M * r / norm**3

def rk4_step(r, v, dt):
    k1v = acceleration(r)
    k1r = v
    k2v = acceleration(r + 0.5 * dt * k1r)
    k2r = v + 0.5 * dt * k1v
    k3v = acceleration(r + 0.5 * dt * k2r)
    k3r = v + 0.5 * dt * k2v
    k4v = acceleration(r + dt * k3r)
    k4r = v + dt * k3v
    r_next = r + dt/6 * (k1r + 2*k2r + 2*k3r + k4r)
    v_next = v + dt/6 * (k1v + 2*k2v + 2*k3v + k4v)
    return r_next, v_next

# Initial setup
r0 = np.array([R_earth + 300e3, 0])
v_escape = np.sqrt(2 * G * M / np.linalg.norm(r0))
v_orbit = np.sqrt(G * M / np.linalg.norm(r0))
v_hyper = v_escape * 1.2

initials = {
    "Elliptical": np.array([0, v_orbit * 0.8]),
    "Parabolic": np.array([0, v_escape]),
    "Hyperbolic": np.array([0, v_hyper])
}

dt = 1
steps = 10000

plt.figure(figsize=(8, 8))
for label, v0 in initials.items():
    r = r0.copy()
    v = v0.copy()
    traj = [r.copy()]
    for _ in range(steps):
        r, v = rk4_step(r, v, dt)
        if np.linalg.norm(r) > 20 * R_earth:
            break
        traj.append(r.copy())
    traj = np.array(traj)
    plt.plot(traj[:,0]/1e6, traj[:,1]/1e6, label=label)

# Draw Earth
earth = plt.Circle((0, 0), R_earth/1e6, color='blue', alpha=0.3)
plt.gca().add_patch(earth)
plt.xlabel("x (Mm)")
plt.ylabel("y (Mm)")
plt.title("Simulated Payload Trajectories Near Earth")
plt.legend()
plt.axis('equal')
plt.grid()
plt.tight_layout()
plt.show()
```

---

## 6. Practical Applications

- **Satellite Launch Windows**: Ensure payload enters desired orbital path
- **Reentry Dynamics**: Calculate trajectories for safe descent and recovery
- **Mission Planning**: High-velocity releases determine escape paths for interplanetary transfer

---

## 7. Conclusion

By integrating Newtonian gravity with energy and velocity constraints, this study provides a complete view of gravitational trajectories. Through numerical simulation, parabolic, elliptical, and hyperbolic dynamics are modeled, showing how initial velocity alone determines the mission outcome.