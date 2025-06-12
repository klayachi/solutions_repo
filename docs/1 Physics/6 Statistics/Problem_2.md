
# Problem 2

# Estimating $\pi$ using Monte Carlo Methods

### 1. Theoretical Foundation

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
\pi \approx 4 \cdot \frac{N_{\text{inside}}}{N_{\text{total}}}
$$

### 2. Simulation

1. Generate $N$ random points $(x, y)$ in the square $[-1, 1] \times [-1, 1]$.
2. Count how many fall inside the unit circle (i.e., those satisfying $x^2 + y^2 \leq 1$).
3. Estimate $\pi$ using:

$$
\pi \approx 4 \cdot \frac{N_{\text{inside}}}{N_{\text{total}}}
$$

### 3. Visualization

A plot can show:

- Points **inside** the circle in **blue**
- Points **outside** the circle in **red**
- The **unit circle** boundary

This visually demonstrates how random sampling approximates the circle's area.

### 4. Analysis

- As $N \rightarrow \infty$, the estimate of $\pi$ converges to the true value.
- The convergence rate is $O(1/\sqrt{N})$, typical for Monte Carlo methods.
- Accuracy increases slowly, so large numbers of samples are needed for high precision.
- Monte Carlo integration is simple but computationally inefficient compared to analytical methods.

---

## Part 2: Estimating $\pi$ Using Buffon’s Needle

### 1. Theoretical Foundation

Buffon's Needle is a probability problem: Drop a needle of length $L$ onto a plane with parallel lines spaced a distance $d$ apart ($L \leq d$). The probability that the needle crosses a line is:

$$
P = \frac{2L}{\pi d}
$$

Rearranging to estimate $\pi$:

$$
\pi \approx \frac{2L \cdot N_{\text{total}}}{d \cdot N_{\text{cross}}}
$$

Where:
- $N_{\text{total}}$ = total number of needle drops
- $N_{\text{cross}}$ = number of times the needle crosses a line

### 2. Simulation

1. Randomly simulate dropping a needle:
   - Random angle $\theta \in [0, \pi]$
   - Random distance from center to nearest line $x \in [0, d/2]$
2. The needle crosses a line if:

$$
x \leq \frac{L}{2} \sin(\theta)
$$

3. Count the number of crossings and estimate $\pi$:

$$
\pi \approx \frac{2L \cdot N_{\text{total}}}{d \cdot N_{\text{cross}}}
$$

### 3. Visualization

A diagram should show:

- Horizontal parallel lines spaced at distance $d$
- Needles randomly placed, with crossing ones in a distinct color
- This illustrates the relationship between geometry and probability

### 4. Analysis

- Like the circle method, this converges slowly: $O(1/\sqrt{N})$
- More complex to implement due to trigonometric calculations
- It offers historical and theoretical interest but is less practical for accurate estimation of $\pi$
- For small numbers of trials, the result is very noisy

---

## Comparison of Methods

| Method              | Convergence Rate | Complexity | Practicality |
|---------------------|------------------|------------|--------------|
| Monte Carlo Circle  | $O(1/\sqrt{N})$  | Easy       | High         |
| Buffon’s Needle     | $O(1/\sqrt{N})$  | Moderate   | Moderate     |

---

## Animation 1

![alt text](download2-ezgif.com-video-to-gif-converter.gif)

## Animation 2

![alt text](ScreenRecording2025-05-22095607-ezgif.com-video-to-gif-converter.gif)

## Using Buffon’s Needle

![alt text](ScreenRecording2025-05-22162411-ezgif.com-video-to-gif-converter.gif)

![alt text](image-15.png)
