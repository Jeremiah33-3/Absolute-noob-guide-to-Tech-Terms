# Lecture Summary: Image Segmentation

## 1. Overview and Goals
The primary objective of image segmentation is to separate an image into coherent regions or "objects". This process groups similar pixels together to increase the efficiency of further processing.
* **Superpixels**: Groups of pixels sharing common characteristics (e.g., intensity) that provide a compact representation with perceptual meaning.
* **Segmentation Types**: An image can have multiple segmentations (undersegmented or oversegmented) depending on the algorithm and parameters.

---

## 2. Segmentation as a Clustering Problem
Clustering involves grouping similar data points and representing them with a single token.

### Key Challenges 
1.  **Similarity Measure**: Determining what makes points similar (e.g., pixel intensity, color, or SSD).
2.  **Grouping Algorithm**: Determining how to compute overall groupings (e.g., K-means vs. Mean-shift).

### Feature Selection 
The choice of feature space determines how pixels are grouped:
* **Intensity Similarity**: Groups based on grayscale values.
* **Color Similarity**: Uses 3D color values (RGB).
* **Spatial Coherence**: Including $(x,y)$ positions allows the algorithm to encode both similarity and proximity. (intensity + position)

---

## 3. K-Means Clustering
An iterative algorithm that assigns points to the nearest cluster center and recomputes those centers.

### The Algorithm
1.  **Initialize**: Randomly pick $k$ points as cluster centers $c_j$.
2.  **Assign**: $y_i = \arg \min_j ||p_i - c_j||^2$ (Assign point $i$ to nearest center).
3.  **Update**: $c_j = \frac{\sum_{i:y_i=j} p_i}{\sum_{i:y_i=j} 1}$ (Set center to the mean of assigned points).
4.  **Repeat**: Until convergence (centers no longer change).

### Pros and Cons
* **Pros**: Simple, fast, and always converges to a local minimum.
* **Cons**: Requires pre-specifying $k$, sensitive to initialization and outliers, and assumes spherical clusters.

---

## 4. SLIC Superpixels
**Simple Linear Iterative Clustering (SLIC)** adapts K-means for efficient superpixel generation.

### Distance Measures
SLIC uses a composite distance $D$ to weigh color similarity ($d_c$) against spatial proximity ($d_s$):
$$d_c = \sqrt{(r_j-r_i)^2 + (g_j-g_i)^2 + (b_j-b_i)^2}$$
$$d_s = \sqrt{(x_j-x_i)^2 + (y_j-y_i)^2}$$
$$D = \sqrt{d_c^2 + \left(\frac{d_s}{s}\right)^2 m^2}$$
* $s$: Initial grid interval.
* $m$: Hyperparameter weighing color vs. spatial importance.

---

## 5. Mean-Shift Clustering
A "model-free" algorithm that finds modes (local density maxima) in the feature space.

### The Procedure
1.  Define a window around a data point.
2.  Compute the centroid (mean) of the points within that window.
3.  Shift the window center to the centroid.
4.  Repeat until convergence.

### Mathematical Formulation 
* **Kernel Density Estimate**: $\hat{f}_{K} = \frac{1}{nh^d} \sum\_{i=1}^n K(\frac{x-x_i}{h})$
* **Mean Shift Vector**: $m(x) = \left[ \frac{\sum_{i=1}^n x_i g(||\frac{x-x_i}{h}||^2)}{\sum_{i=1}^n g(||\frac{x-x_i}{h}||^2)} - x \right]$

### Pros and Cons
* **Pros**: Does not assume cluster shape, robust to outliers, and finds a variable number of modes.
* **Cons**: Computationally expensive, scales poorly with dimensions, and output depends heavily on window size ($h$).

---

## 6. Comparison Summary

| Feature | K-Means | Mean-Shift |
| :--- | :--- | :--- |
| **Parameters** | $k$ (number of clusters) | $h$ (window size/bandwidth) |
| **Cluster Shape** | Spherical | Any shape |
| **Efficiency** | Fast | Slow/Expensive |
| **Outliers** | Sensitive | Robust |
