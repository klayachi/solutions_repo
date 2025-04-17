
# Problem 2  
# Investigating the Dynamics of a Forced Damped Pendulum

## Motivation

The forced damped pendulum is a captivating and powerful model in nonlinear dynamics. It exemplifies how the addition of damping and periodic driving can transform a system from simple harmonic motion into exhibiting rich and sometimes chaotic behavior. These dynamics are not only fascinating from a theoretical perspective but also deeply relevant in engineering, environmental science, and even biology.

By varying the amplitude and frequency of the external force, one can observe synchronized motion, bifurcations, chaos, and resonance. These transitions give rise to a wide array of applications, such as energy harvesting, vibration isolation systems, and structural engineering solutions.

---

## Solution

### 1. Theoretical Foundation

#### Governing Equation

The motion of a forced damped pendulum is governed by:

$$
\frac{d^2\theta}{dt^2} + \gamma \frac{d\theta}{dt} + \frac{g}{L} \sin(\theta) = A \cos(\omega t)
$$

Where:

Where:

| Symbol        | Description                         |
|---------------|-------------------------------------|
| $$\\theta(t)$$ | Angular displacement                |
| $$\\gamma$$    | Damping coefficient                 |
| $$g$$          | Gravitational acceleration          |
| $$L$$          | Length of the pendulum              |
| $$A$$          | Amplitude of the driving force      |
| $$\\omega$$    | Frequency of the driving force      | 

#### Small-Angle Approximation

When $$ \theta \ll 1 $$, we approximate $$ \sin(\theta) \approx \theta $$, leading to:

$$
\frac{d^2\theta}{dt^2} + \gamma \frac{d\theta}{dt} + \frac{g}{L} \theta = A \cos(\omega t)
$$

This linear non-homogeneous equation allows a solution composed of two parts:  
- **Transient**: Decaying oscillations due to damping  
- **Steady-state**: Driven oscillations at the frequency $$ \omega $$  

#### Resonance Condition

Resonance occurs when the driving frequency $$ \omega $$ approaches the system's natural frequency:

$$
\omega_0 = \sqrt{\frac{g}{L}}
$$

At resonance, the pendulum experiences the maximum energy transfer from the driving force.

---

### 2. Analysis of Dynamics

We examine the effect of three primary parameters:

- **Damping ($$\gamma$$)**  
  - Low: Sustained oscillations  
  - High: Rapid energy dissipation  

- **Driving Amplitude ($$A$$)**  
  - Low: Regular motion  
  - High: Chaotic transitions  

- **Driving Frequency ($$\omega$$)**  
  - $$ \omega \approx \omega_0 $$: Resonance  
  - $$ \omega \neq \omega_0 $$: Sub-harmonic, quasiperiodic, or chaotic motion  

At certain parameter combinations, the pendulum displays **chaotic motion**—highly sensitive to initial conditions and unpredictable over long time intervals.

---

### 3. Practical Applications

- **Energy Harvesting**: Vibrational energy can be converted into electrical energy using piezoelectric materials and pendulum dynamics.
- **Suspension Bridges**: Proper damping prevents failures like the Tacoma Narrows Bridge collapse.
- **RLC Circuits**: These circuits behave analogously to mechanical pendula and are essential in electronics.

---

### 4. Implementation: Python Simulation

Below are Python simulations exploring pendulum dynamics under various settings. You can run the full simulation set on Google Colab.

#### Basic Setup

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import solve_ivp

def forced_damped_pendulum(t, y, gamma, omega0, A, omega):
    theta, omega1 = y
    dtheta_dt = omega1
    domega_dt = -gamma * omega1 - omega0**2 * np.sin(theta) + A * np.cos(omega * t)
    return [dtheta_dt, domega_dt]
```

#### Case 1: No damping, no forcing

```python
sol = solve_ivp(forced_damped_pendulum, [0, 50], [0.1, 0], args=(0, 1.5, 0, 0), t_eval=np.linspace(0, 50, 1000))
plt.plot(sol.t, sol.y[0])
plt.title("Pendulum without damping or forcing")
plt.xlabel("Time (s)")
plt.ylabel("Angle (rad)")
plt.grid()
plt.show()
```

#### Case 2: Damped, no forcing

```python
sol = solve_ivp(forced_damped_pendulum, [0, 50], [0.1, 0], args=(0.5, 1.5, 0, 0), t_eval=np.linspace(0, 50, 1000))
plt.plot(sol.t, sol.y[0])
plt.title("Damped Pendulum")
plt.xlabel("Time (s)")
plt.ylabel("Angle (rad)")
plt.grid()
plt.show()
```

#### Case 3: Damped with periodic forcing

```python
sol = solve_ivp(forced_damped_pendulum, [0, 50], [0.1, 0], args=(0.5, 1.5, 1.2, 1.5), t_eval=np.linspace(0, 50, 1000))
plt.plot(sol.t, sol.y[0])
plt.title("Forced Damped Pendulum")
plt.xlabel("Time (s)")
plt.ylabel("Angle (rad)")
plt.grid()
plt.show()
```

#### Case 4: Resonance Case

```python
sol = solve_ivp(forced_damped_pendulum, [0, 50], [0.1, 0], args=(0.1, 1.5, 1.5, 1.5), t_eval=np.linspace(0, 50, 1000))
plt.plot(sol.t, sol.y[0])
plt.title("Resonance in Forced Damped Pendulum")
plt.xlabel("Time (s)")
plt.ylabel("Angle (rad)")
plt.grid()
plt.show()
```

---

## Graphical Analysis

### Phase Portrait

```python
plt.plot(sol.y[0], sol.y[1])
plt.title("Phase Portrait")
plt.xlabel("Angle (rad)")
plt.ylabel("Angular Velocity (rad/s)")
plt.grid()
plt.show()
```

### Poincaré Section

```python
omega_drive = 1.5
T_drive = 2 * np.pi / omega_drive
t_points = np.arange(0, 50, T_drive)
theta_values = []
omega_values = []

for t_eval in t_points:
    sol = solve_ivp(forced_damped_pendulum, [0, t_eval], [0.1, 0], args=(0.5, 1.5, 1.2, omega_drive))
    theta_values.append(sol.y[0][-1])
    omega_values.append(sol.y[1][-1])

plt.scatter(theta_values, omega_values, s=10)
plt.title("Poincaré Section")
plt.xlabel("Angle (rad)")
plt.ylabel("Angular Velocity (rad/s)")
plt.grid()
plt.show()
```

### Bifurcation Diagram (Driving Amplitude)

```python
A_values = np.linspace(0, 2, 200)
final_angles = []

for A in A_values:
    sol = solve_ivp(forced_damped_pendulum, [0, 200], [0.1, 0], args=(0.5, 1.5, A, 1.5), t_eval=np.linspace(190, 200, 100))
    final_angles.extend(sol.y[0][-10:])  # sample from last few cycles

plt.plot(np.repeat(A_values, 10), final_angles, ',', alpha=0.5)
plt.title("Bifurcation Diagram: Driving Amplitude")
plt.xlabel("A (Driving Amplitude)")
plt.ylabel("Final Angle (rad)")
plt.grid()
plt.show()
```

---

## Google Colab

You can run this simulation interactively here:  
[▶ Launch Google Colab Simulation](https://colab.research.google.com)

---

## Conclusion

The forced damped pendulum illustrates how simple mechanical systems can transition from order to chaos. Through theoretical models and numerical experiments, we gain deep insight into resonance, energy transfer, and complex behavior—insights that impact real systems in engineering, electronics, and the natural world.