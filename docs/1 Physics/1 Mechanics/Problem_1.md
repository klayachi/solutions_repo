# Problem 1

# Investigating the Range as a Function of the Angle of Projection

![alt text](projectile_all_angles_slow.gif)


## 1. Theoretical Foundation
Projectile motion is governed by Newton's laws. The equations of motion for a projectile launched at an angle \( \theta \) with initial velocity \( v_0 \) are derived from kinematic equations:

### Differential Equation of Motion
The motion of a projectile is governed by the second-order differential equations:
  $$
  \frac{d^2x}{dt^2} = 0, \quad \frac{d^2y}{dt^2} = -g
  $$
Integrating once:
  $$
  \frac{dx}{dt} = v_0 \cos(\theta), \quad \frac{dy}{dt} = v_0 \sin(\theta) - g t
  $$
Integrating again:
  $$
  x(t) = v_0 \cos(\theta) t, \quad y(t) = v_0 \sin(\theta) t - \frac{1}{2} g t^2
  $$


### Equations of Motion
    
- **Horizontal displacement:**
  $$
  x(t) = v_0 \cos(\theta) t
  $$
- **Vertical displacement:**
  $$
  y(t) = v_0 \sin(\theta) t - \frac{1}{2} g t^2
  $$


To find the range \( R \), we determine the time of flight \( T_f \):
  $$
  T_f = \frac{2 v_0 \sin(\theta)}{g}
  $$

Substituting into the horizontal displacement:
  $$
  R = \frac{v_0^2 \sin(2\theta)}{g}
  $$

## 2. Analysis of the Range

- The maximum range occurs at \( \theta = 45^\circ \), yielding:  
  $$
  R_{\max} = \frac{v_0^2}{g}
  $$  
- **Why is \( 45^\circ \) the optimal angle?**  

  The range formula for projectile motion (neglecting air resistance) is:  

  $$
  R = \frac{v_0^2 \sin(2\theta)}{g}
  $$  

  The **sine function** reaches its maximum value when **\( 2\theta = 90^\circ \)**, meaning:  

  $$
  \theta = 45^\circ
  $$  

  At this angle, the **horizontal velocity** and **vertical velocity** are balanced, maximizing the distance traveled.  

  **Visual Representation:**  

  Below is a diagram illustrating projectile motion at different angles. Notice how the range is maximized at **\( 45^\circ \)**:  


- **Gravity Influence:** Lower gravity increases range (e.g., Moon vs. Earth).  
- **Velocity Impact:** Higher velocity increases range quadratically.  


## 3. Practical Applications

Projectile motion has a wide range of practical applications across various fields. Understanding the principles behind projectile trajectories allows for better planning, optimization, and decision-making. Here are some key areas where these concepts are applied:

### 3.1 Sports
In sports such as football, basketball, and golf, the trajectory of balls is often analyzed to improve player performance and strategy. Understanding how different angles and speeds affect the distance and trajectory of a ball can help athletes optimize their throws, kicks, and swings. Coaches and players can use this information to improve accuracy and maximize the effectiveness of their plays.

- **Football**: The trajectory of a football when kicked for a field goal or a punt is a classic example of projectile motion. The optimal launch angle and velocity for achieving maximum distance and accuracy are essential.
- **Golf**: In golf, golfers use their knowledge of projectile motion to determine the ideal angle for hitting the ball to achieve maximum distance and ensure it lands where they want.
- **Basketball**: The angle at which a basketball is thrown affects the likelihood of it going through the hoop. Understanding projectile motion helps players optimize their shooting angles and force for better accuracy.

### 3.2 Engineering
Projectile motion principles are also applied in engineering, especially in the design and optimization of systems involving the launch or movement of objects. Engineers working in fields like aerospace, mechanical, and civil engineering must understand how objects travel through air or space.

- **Ballistics Engineering**: Ballistics engineers use these principles to design and test the trajectories of projectiles such as missiles and bombs. Understanding the physics behind projectile motion ensures the effectiveness and precision of weapons.
- **Aerospace Engineering**: The principles of projectile motion are also fundamental in the design of spacecraft and satellites, particularly when launching probes into orbit. These calculations help engineers predict the trajectory of a spacecraft during its journey, ensuring accurate positioning and minimizing fuel consumption.

### 3.3 Astrophysics
In astrophysics, the study of projectile motion is crucial for calculating the orbits of planets, moons, satellites, and other celestial bodies. Understanding the motion of objects in space allows scientists to predict their movements and plan missions to explore distant regions.

- **Satellite Orbits**: The trajectories of satellites around Earth or other planets are determined by applying the principles of projectile motion. Engineers and astrophysicists use these principles to ensure satellites stay in orbit and fulfill their intended functions.
- **Space Probes**: Space agencies like NASA rely on precise projectile motion calculations when launching probes to explore planets, moons, and asteroids. Accurate predictions of trajectory and range are essential to ensure that these probes reach their targets, such as Mars or Jupiter's moons, without missing their mark.

### 3.4 Environmental Science
Projectile motion principles are also relevant in environmental science, particularly in the study of pollution and the movement of particles in the atmosphere. For instance, understanding the motion of pollutants released into the atmosphere can help predict how far and in what direction these pollutants will travel.

- **Pollutant Dispersion**: The dispersion of pollutants in the atmosphere or water bodies can be modeled using the principles of projectile motion. By calculating the optimal angles and velocities of the particles, environmental scientists can predict the spread of pollutants over time and space.
- **Wildfire Smoke Trajectory**: In wildfire management, predicting the movement of smoke and ash can help emergency services plan evacuations and predict air quality conditions in affected areas.

## 4. Implementation
The following Python script implements additional simulations based on professor's notes:
You can run the simulation in Google Colab by clicking the link below:

[▶ Run in Google Colab](https://colab.research.google.com/drive/1vAG0r9HznXhCcpJ7Q-qQ4i_W0lf_yCkD?usp=sharing)

```
import numpy as np
import matplotlib.pyplot as plt
from matplotlib.animation import FuncAnimation
from IPython.display import HTML

def projectile_trajectory(v0, angle, g=9.81, h=0, dt=0.05):
    angle_rad = np.radians(angle)
    vx = v0 * np.cos(angle_rad)
    vy = v0 * np.sin(angle_rad)
    x, y = [0], [h]
    t = 0
    while y[-1] >= 0:
        t += dt
        x.append(vx * t)
        y.append(h + vy * t - 0.5 * g * t**2)
    return np.array(x), np.array(y)

# 1. Three different velocities on the same plot
plt.figure(figsize=(8,5))
plt.ylim(0, 60)
for v0 in [10, 20, 30]:
    x, y = projectile_trajectory(v0, 45)
    plt.plot(x, y, label=f'v0 = {v0} m/s')
plt.xlabel("Horizontal Distance (m)")
plt.ylabel("Vertical Distance (m)")
plt.title("Projectile Motion with Different Velocities")
plt.legend()
plt.grid()
plt.show()

# 2. Same initial conditions on three different planets
plt.figure(figsize=(8,5))
plt.ylim(0, 60)
planets = {"Earth": 9.81, "Moon": 1.62, "Jupiter": 24.79}
for planet, g in planets.items():
    x, y = projectile_trajectory(20, 45, g)
    plt.plot(x, y, label=planet)
plt.xlabel("Horizontal Distance (m)")
plt.ylabel("Vertical Distance (m)")
plt.title("Projectile Motion on Different Planets")
plt.legend()
plt.grid()
plt.show()

# 3. Different heights
plt.figure(figsize=(8,5))
plt.ylim(0, 60)
for h in [0, 10, 20]:
    x, y = projectile_trajectory(20, 45, 9.81, h)
    plt.plot(x, y, label=f'Height = {h}m')
plt.xlabel("Horizontal Distance (m)")
plt.ylabel("Vertical Distance (m)")
plt.title("Projectile Motion with Different Initial Heights")
plt.legend()
plt.grid()
plt.show()

# 4. Air resistance vs. no air resistance
plt.figure(figsize=(8,5))
plt.ylim(0, 60)
def projectile_with_drag(v0, angle, g=9.81, h=0, dt=0.05, drag_coeff=0.1):
    angle_rad = np.radians(angle)
    vx, vy = v0 * np.cos(angle_rad), v0 * np.sin(angle_rad)
    x, y = [0], [h]
    t = 0
    while y[-1] >= 0:
        t += dt
        vx -= drag_coeff * vx * dt
        vy -= (g + drag_coeff * vy) * dt
        x.append(x[-1] + vx * dt)
        y.append(y[-1] + vy * dt)
    return np.array(x), np.array(y)

x_no_drag, y_no_drag = projectile_trajectory(20, 45)
x_drag, y_drag = projectile_with_drag(20, 45)
plt.plot(x_no_drag, y_no_drag, label="No Air Resistance")
plt.plot(x_drag, y_drag, linestyle='dashed', label="With Air Resistance")
plt.xlabel("Horizontal Distance (m)")
plt.ylabel("Vertical Distance (m)")
plt.title("Projectile Motion With and Without Air Resistance")
plt.legend()
plt.grid()
plt.show()
```

## 5. Limitations and Future Work

While the basic model of projectile motion provides valuable insights, there are several limitations that need to be addressed in future studies. Expanding the model to incorporate more factors will improve its accuracy and applicability across various domains. Below are some key limitations and potential areas for future research:

### 5.1 Simplified Assumptions in the Basic Model
The standard projectile motion model neglects several real-world factors, such as air resistance, wind, and the Earth's curvature, which can all significantly affect the trajectory of a projectile. The basic model assumes:
- **No Air Resistance**: This simplification assumes a frictionless environment, which is unrealistic, especially for objects moving at high speeds or over long distances.
- **Flat Terrain**: The basic model assumes the projectile is launched from a flat surface, ignoring the effects of uneven terrain or changes in altitude.
- **Constant Gravity**: The model assumes gravity is constant, but in reality, it varies slightly depending on the location on Earth and other factors, such as altitude.

### 5.2 Air Resistance and Drag
One of the most significant limitations of the basic model is its neglect of air resistance, which plays a critical role in real-world projectile motion. In the presence of air resistance, the projectile’s trajectory is altered, resulting in a shorter range and a more complex path. Future work could focus on including drag forces in the equations, which would require more sophisticated models, such as the **drag equation** that accounts for factors like velocity, projectile shape, and air density.

- **Drag Effects**: The effect of air resistance can be modeled using the drag coefficient, which depends on the object's shape, surface roughness, and velocity. Implementing air resistance would allow more accurate simulations of projectile motion in real-world scenarios.
- **Wind Effects**: Wind can significantly influence the motion of a projectile, especially over long distances. Future studies could include wind simulations to account for changes in direction and speed, further enhancing the accuracy of the model.

### 5.3 Uneven Terrain and Variable Gravitational Fields
The basic model assumes a flat, uniform surface for the projectile to land on, which is not always the case in real-world scenarios. For example, when launching projectiles on uneven terrain or at varying altitudes, the motion is influenced by changes in gravitational force and the angle of the launch.

- **Uneven Terrain**: In future models, terrain variations could be included to simulate the projectile’s behavior when launched from hills, mountains, or other irregular surfaces.
- **Variable Gravity**: Gravity decreases with altitude, and in certain locations, it may vary slightly. Incorporating this variable gravity into the equations could lead to more precise predictions for long-range projectiles, especially in space exploration.

### 5.4 Impact of External Factors
Other environmental factors, such as temperature, humidity, and air pressure, can also affect projectile motion. Future work could consider these factors, particularly in applications like military ballistics or sports, where precision is critical.

- **Temperature and Humidity**: These factors can change the density of the air, which in turn affects air resistance. Future models could incorporate atmospheric conditions to refine the trajectory predictions.
- **Coriolis Effect**: On Earth, the rotation of the planet affects long-range projectiles, particularly over large distances, such as when launching missiles or projectiles on a global scale. The **Coriolis effect** should be included in future models to account for the Earth's rotation.

### 5.5 Advanced Computational Models
While the current simulations provide valuable insights, more advanced computational models could allow for more complex analyses. These models could use higher-order differential equations to account for additional forces and interactions, such as:
- **Turbulent Flow**: Simulating the effects of turbulent air around the projectile could provide a more accurate representation of real-world conditions.
- **Multi-Stage Trajectories**: For multi-stage projectiles, such as rockets or missiles, the trajectory could be modeled as a series of stages, each with different velocity, gravity, and drag conditions.

In conclusion, while the basic model offers a solid foundation for understanding projectile motion, future work should expand the model to account for a broader range of real-world factors. By incorporating air resistance, varying terrain, and other external forces, we can achieve more accurate simulations and predictions, ultimately enhancing applications in fields like aerospace, sports, and environmental science.