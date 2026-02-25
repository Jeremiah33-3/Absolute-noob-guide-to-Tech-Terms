# Lecture Summary: Lines & Hough Transform

## 1. Motivation for Line Fitting
While edge detectors (like Canny) identify edge pixels, they do not inherently understand the structure of the objects. Line fitting is necessary to:
* Identify which points belong to which specific lines.
* Handle noise, missing edge points, and occlusion.
* Recognize multiple instances of a shape in a single pass.

---

## 2. Mathematics of Lines
The lecture discusses three primary ways to parameterize a line:

### A. Slope-Intercept Form
$$y = mx + b$$
* **$m$**: Slope.
* **$b$**: y-intercept.
* **Limitation**: Cannot represent vertical lines ($m = \infty$).

### B. Double Intercept Form
$$\frac{x}{a} + \frac{y}{b} = 1$$
* **$a$**: x-intercept; **$b$**: y-intercept.

### C. Normal Form (Hessian Normal Form)
This is the preferred form for Hough Transforms because it uses a finite parameter space.

$$x \cos \theta + y \sin \theta = \rho$$
* **$\rho$ (rho)**: The perpendicular distance from the origin to the line.
* **$\theta$ (theta)**: The angle of the normal vector to the line.
* **Range**: $0 \le \theta \le 2\pi$ and $0 \le \rho \le \rho_{max}$.

---

## 3. The Hough Transform Algorithm
The Hough Transform is a **voting technique** where image points "vote" for the parameters of the shapes they could potentially form.

### Algorithm Steps:
1.  **Quantize Parameter Space**: Create a 2D accumulator array $A(\theta, \rho)$.
2.  **Initialize**: Set all values in the accumulator to zero.
3.  **Vote**: For every edge point $(x_i, y_i)$ in the image (from canny edge detector), calculate all possible $(\theta, \rho)$ pairs that satisfy the line equation and increment those "bins" in the accumulator.
    * *Note: A point in image space becomes a **sinusoid** in $(\theta, \rho)$ parameter space*.
4.  **Detect**: Find local maxima in the accumulator that exceed a certain threshold.

---

## 4. Extensions of the Hough Transform

### Circle Detection
Circles are parameterized as $(x-a)^2 + (y-b)^2 = r^2$.
* **Known Radius**: Requires a 2D parameter space $(a, b)$ for the center.
* **Unknown Radius**: Requires a 3D parameter space $(a, b, r)$, which increases computational complexity

### Leveraging Gradients
To improve efficiency, one can use the **edge orientation ($\phi$)**.
* Instead of voting for all possible parameters, a point only votes for shapes consistent with its local gradient.

### Generalized Hough Transform (GHT)
Used for arbitrary shapes that lack a simple equation.
* **Model**: Defined by displacement vectors from boundary points to a reference point.
* **Table**: Displacement vectors are stored in a table indexed by gradient orientation.
* **Modern Use**: Can be generalized using "visual codewords" for object detection and tracking.

---

## 5. Pros and Cons

| **Pros** | **Cons** |
| :--- | :--- |
| Robust to gaps and occlusion. | Computational complexity grows exponentially with parameters. |
| Robust to noise. | Tricky to pick the right quantization/grid size. |
| Can detect multiple instances at once. | Can produce spurious peaks from non-target shapes. |
