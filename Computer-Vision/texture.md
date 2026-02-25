## 1. The Concept of Visual Textures
* **Definition**: A pattern with repeating elements. While repetitions can have variations, we can still separate what repeats from what stays the same.
* **Scale Consideration**: Often, the same thing can be considered an object or a texture, depending entirely on the scale of consideration (e.g., a tree vs. a leaf).
* **Categories**: Textures range from regular, near-regular, irregular, near-stochastic, to stochastic.
* **Importance**: Textures are an important appearance cue indicative of material properties.

## 2. Filter Banks and Representations
To analyze textures, we need features one step above basic colour or simple edges.
* **Filter Banks**: A generalization of applying multiple filters at various orientations and scales. \For $d$ filters, feature vectors are $d$-dimensional.

### Gabor Filters
Gabor filters are commonly used in filter banks to represent textures. They combine sinusoids with an exponential (Gaussian) envelope.



* **1D Gabor Filter**: 
$$e^{-\frac{x^{2}}{2\sigma^{2}}}cos(2\pi f x)$$
* **2D Gabor Filter**:
$$f_{mn}=\frac{1}{2\pi\sigma^{2}}exp[-\frac{m^{2}+\gamma^{2}n^{2}}{2\sigma^{2}}]sin[\frac{2\pi(cos[\omega]m+sin[\omega]n)}{\lambda}+\phi]$$

**Key Parameters**:
* $\sigma$: Rate of decay for the exponential envelope.
* $\gamma$: Aspect ratio of the envelope coverage.
* $\lambda$: Wavelength of the sinusoid.
* $\omega$: Orientation of the sinusoid in 2D.
* $\phi$: Phase of the sinusoid.

## 3. Textons and Histograms
Instead of dealing with continuous feature spaces, we can characterize textures by replacing pixels with an integer representing a texture 'type'.

* **Texton Dictionary**: Created by clustering the filter responses for all pixels in training images (e.g., using K-means) and storing the cluster centers.
* **Assignment**: For a new image, filter it with the same filter bank and assign each pixel's feature vector to the nearest cluster. The cluster ID is the texton ID.
* **Texton Histograms**: For a given region, a histogram of textons is computed to represent the spatial arrangement of texton IDs.

## 4. Comparing Textures & Applications

### Distance Metrics
To compare textures (e.g., windows $a$ and $b$), Euclidean distance ($L2$) is used to see how dissimilar they are:
$D(a,b)=\sqrt{(a_{1}-b_{1})^{2}+(a_{2}-b_{2})^{2}}$ 

### Material Classification vs. Image Segmentation
| Feature | Material Classification | Image Segmentation |
| :--- | :--- | :--- |
| **Input** | Image $(h \times w)$ | Image $(h \times w)$ |
| **Algorithm** | Nearest-neighbor classification | Clustering (e.g. k-means) |
| **Data Sample** | $(h \times w)$ image is represented as a single data poin] | Each pixel is a single data point to be clustered |
| **Feature** | Texton histogram over the entire image | Spatially smoothed filter bank response (texton histograms work poorly here) |

### Perceived Boundaries (Texture Gradients)
Regions with very distinct textures are separated by a texture boundary. To identify these boundaries, the algorithm considers a disc split into two halves by a diameter of a particular orientation. It measures the texture difference by comparing the texton histograms of the two halves.
