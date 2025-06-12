# Problem 2

# Estimating $\pi$ using Monte Carlo Methods

## 1. Theoretical Foundation

To estimate $\pi$ using random points, consider a unit circle inscribed in a square. The circle has a radius $r = 1$, and the square spans from $-1$ to $1$ in both $x$ and $y$ directions.

The area of the unit circle is:

$$
A_{\text{circle}} = \pi r^2 = \pi
$$

The area of the square is:

$$
A_{\text{square}} = (2r)^2 = 4
$$

If we randomly generate points uniformly within the square, the probability that a point lies inside the circle is:

$$
P = \frac{A_{\text{circle}}}{A_{\text{square}}} = \frac{\pi}{4}
$$

Solving for $\pi$ gives:

$$
\pi \approx 4 \cdot \frac{\text{Number of points inside the circle}}{\text{Total number of points}}
$$

---

## 2. Simulation

1. Generate $N$ random points $(x, y)$ in the square $[-1, 1] \times [-1, 1]$.
2. Count how many fall inside the unit circle (i.e., those satisfying $x^2 + y^2 \leq 1$).
3. Estimate $\pi$ using:

$$
\pi \approx 4 \cdot \frac{N_{\text{inside}}}{N_{\text{total}}}
$$

---

## 3. Visualization

A plot can show:

- Points **inside** the circle in **blue**
- Points **outside** the circle in **red**
- The **unit circle** boundary

This visually demonstrates how random sampling approximates the circle's area.

![alt text](pi_convergence_plot.png)

---

## 4. Analysis

- As $N \rightarrow \infty$, the estimate of $\pi$ converges to the true value.
- The convergence rate is $O(1/\sqrt{N})$, typical for Monte Carlo methods.
- Accuracy increases slowly, so large numbers of samples are needed for high precision.
- Monte Carlo integration is simple but computationally inefficient compared to analytical methods.

---

## Summary

This method:
- Is easy to implement.
- Demonstrates probabilistic estimation.
- Converges slowly (requires a lot of points for high precision).
- Visualizes the randomness and convergence beautifully.

---

## Formula Recap

$$
\pi \approx 4 \cdot \frac{N_{\text{in}}}{N_{\text{total}}}
$$

Where:
- $N_{\text{in}}$ = number of points inside the circle
- $N_{\text{total}}$ = total number of points sampled
