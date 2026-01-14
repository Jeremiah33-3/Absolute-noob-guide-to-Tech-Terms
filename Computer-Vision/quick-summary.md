# Table of content
- [Goals of CV](#Goals-of-CV)
- [Digital Images](#Digital-Images)
- [Colour Images](#Colour-Images)

# Goals of CV

Perceive the 'story' behind the picture by computing properties of the world (3D shape, names of people or objects, what happened, when how why)
- Measure: Compute the 3D shape of the world
- Recognise objects & people (includes activies, feelings, gestures,...)
- Generate: Enhance images (read image reflected in iris), improve photos/videos, create new
- Organisation & search (by image)

**Applications**: safety, health, security, comfort, entertainment, access

## Difficulty

👓 Viewpoint variation
🔦 Illumination
📏 Scale
📋 Intra-class variation (differneces within a single class of data)
🚂 Motion
👚 Background clutter
🕶️ Occlusion

# Digital Images

> Imaging sensors, exposure time, spatial and intensity resolution

## Image Acquisition

> The initial process of capturing visual information from the physical world and converting it into a digital image format that a computer can process and analyze.

**Process**
1. Illumination Source: The process often starts with an illumination source (e.g., visible light, X-rays, or ultrasound) that interacts with the scene or object being imaged.

<p align="center">
_energy transfer from souce to scene to imaging system._
</p>

2. Optics (in imaging system): An optical system, such as a lens, collects the energy (e.g., light photons) reflected from or transmitted through the object and focuses it onto a sensor.

3. Sensing (Transduction): An image sensor, typically a Charge-Coupled Device (CCD) or Complementary Metal-Oxide-Semiconductor (CMOS) sensor, converts the incoming energy (photons) into an electrical signal (voltage). Every cell corresponds to one pixel and contains filter, housing and sensor -> measures amount of energy

4. Analog-to-Digital Conversion: The continuous electrical signal is then amplified and converted into a digital signal using an analog-to-digital converter (ADC). This process involves sampling the coordinate values and quantizing the amplitude values into discrete quantities (pixels). Values are proportional to the energy.

5. Digital Image Output: The result is a raw digital image represented as a numerical array (bitmap) in the computer's memory, where each value corresponds to the intensity and color (pixel) at a specific location. -> internal image plane

## Image formulation model

> $f(x,y)$ - 2D image function, where $x, y$ are coordinates on the internal image plane

$$
f(x,y) = i(x,y) \cdot r(x,y)
$$

**$i(x,y)$**:  Illumination component which captures amount of source illumination incident on the scene 
- no upper bound: $0 \leq i(x,y) \lt \infty$

**$r(x,y)$**:  Reflectance component which captures amount of illumination reflected by objects in the scene 
- 0 for total absorption, 1 for total reflectanc: $0 \leq r(x,y) \leq 1$

### Properties
**Exposure time:**
- Longer exposure time -> over exposed as too much light reaches sensor.
- Under exposed vice versa (not enough light reaches sensor).
- Motion blur: the more challenging problem (obj alr moved by exposure time)
**Resolution:**
- Spatial resolution (sampling): defines the smallest discernible detail (sharpness) using pixels per unit area (e.g., dpi) - pixel density which affects clarity
- Intensity reolution (quantization): (or bit depth) determines the number of distinct shades or brightness levels (e.g., 8-bit for 256 levels) - colour/grayscale accuracy to prevent banding
- higher values in both improving image quality by adding detail and smoother transitions, respectively
- Spatial and intensity resolution determines the file size and also transmission time if we were to send images over the internet.
- An image of size $M \cdot N$ with a bit-depth of $k$ requires $b$ bits to store, where:

$$
b = M \cdot N \cdot k
$$

- $b$ is the storage requirement for a raw bitmap (.bmp).  Compressed formats (.png, .jpg) can reduce file sizes.

# Colour Images

In python, represented as a matrix, e.g.

```python
import cv2

# Load image as a NumPy array
image = cv2.imread("example.jpg")  # BGR format by default
print(type(image))  # <class 'numpy.ndarray'>
print(image.shape)  # (height, width, channels)
```

3 channels, roughly `im(y, x, c)`: y pixels down, x pixels to the right in the cth channel. (RGB - 012)

### Bayer filter
> A Bayer filter is a color filter array (CFA) used in most digital cameras, placing red, green, and blue filters in a specific mosaic pattern over a single image sensor, with twice as many green pixels as red or blue, to capture color information efficiently, leveraging human eye sensitivity to green to create full-color images through interpolation (demosaicing).

**Process:** Incoming light -> filter layer -> sensor array -> resulting pattern

**Demosaicing:**
Borrowing from the nearest neighbour to populate the rest of the channel values given a specific pattern:

$$
g(x,y)=
\begin{cases}
[R,G,B]_B  = [\, f(x+1,y+1),\; f(x+1,y),\; f(x,y) \,] \\
[R,G,B]_{GB} = [\, f(x,y+1),\; f(x,y),\; f(x-1,y) \,] \\
[R,G,B]_{GR} = [\, f(x+1,y),\; f(x,y),\; f(x,y-1) \,] \\
[R,G,B]_R  = [\, f(x,y),\; f(x-1,y),\; f(x-1,y-1) \,]
\end{cases}
$$

## Colour models

### RBG

- “default” colour space
- additivemodel used in electronic displays & photography
- based on trichromatic perception of colours
- [0-255, 0-255, 0-255] -> higher intensity, closer to white (lower is black)
- intensity of colours carry information

**Colour to greyscale**: $I = W_{R} \cdot R + W_G \cdot G + W_{B} \cdot B$
- sum of weights ($W_{i}$) = 1 to keep values within [0, 255]
- weights can be chosen (default is equal split)

### Normalized RGB Color Space

In standard RGB space (represented as a 3D cube), **color** (chromaticity) and **intensity** (brightness) are entangled.

* **Vector Nature:** Colors can be visualized as vectors starting from the origin $(0,0,0)$.
* **Illumination:** Points lying on the same vector represent the **same color** under **different lighting**.

> **Example:** The points $(40, 20, 50)$, $(100, 50, 125)$, and $(200, 100, 250)$ lie on the same vector. They appear as the same hue, just brighter or darker.

---

To make color recognition invariant to lighting conditions (e.g., shadows vs. bright light), we convert **Raw RGB** $(R, G, B)$ into **Normalized RGB** $(r, g, b)$.

**The Formula**
To normalize, divide each component by the sum of all components:

$$
r = \frac{R}{R + G + B}
$$

$$
g = \frac{G}{R + G + B}
$$

$$
b = \frac{B}{R + G + B}
$$

**Key Properties**
1.  **The Sum Constraint:**
    $$r + g + b = 1$$
2.  **Over-specification:** Since we know the sum is 1, knowing just $r$ and $g$ allows us to calculate $b$ ($b = 1 - r - g$). The third coordinate is redundant.
3.  **Edge Case:** If $R=G=B=0$ (pure black), normalized values are defined as $(0,0,0)$ to prevent division by zero.

---

#### Separating Color and Intensity
This process transforms the data from $(R, G, B)$ to $(r, g, I)$, effectively separating the "true color" from the lighting.

| Component | Symbol | Calculation | Meaning |
| :--- | :---: | :--- | :--- |
| **Chromaticity** | $(r, g)$ | Normalized RGB formulas | The "True Color" (invariant to lighting). |
| **Intensity** | $I$ | $I = \frac{R + G + B}{3}$ | The brightness or "amount of light." |

---

#### Visualizing the Space
* **The Projection:** All normalized colors fall onto a 2D triangular plane connecting $(1,0,0)$, $(0,1,0)$, and $(0,0,1)$.
* **The Triangle Layout:**
    * **Vertices:** Pure Red, Pure Green, Pure Blue.
    * **Edges:** Pure mixtures of two primary colors.
    * **Center:** White (equal mixture).

**Goal:** Separating colour and intensity gives a robust Computer Vision.
By separating color and intensity, algorithms can track objects based on their color even if the lighting in the room changes.

### HSV Color Space

**Concept: Human Perception vs. Machine Output**

While RGB is designed for hardware (screens/sensors), **HSV (Hue, Saturation, Value)** is designed to match human perception of color.

**The Three Components**
| Component | Definition | Range | Visual Intuition |
| :--- | :--- | :--- | :--- |
| **Hue (H)** | The "Pure Color" category. | $0^{\circ} \to 360^{\circ}$ | The angle on a color wheel (Red=0, Green=120, Blue=240). |
| **Saturation (S)** | The "Purity" of the color. | $0 \to 1$ | **0**: White/Gray (washed out)<br>**1**: Pure Vivid Color |
| **Value (V)** | The "Brightness" or intensity. | $0 \to 255$ | **0**: Pitch Black<br>**255**: Full Brightness |

---

**Geometric Model**

HSV is often represented as a **Cone** or **Inverted Pyramid**:
* **Vertical Axis:** Value (Black at the bottom tip, bright at the top).
* **Radial Distance:** Saturation (Grayscale at the center axis, vivid at the outer shell).
* **Circumference:** Hue (The specific color).

---

**RGB to HSV Conversion Formulas**

To convert standard RGB $(R, G, B)$ to HSV:

**A. Calculate Value (V) and Chroma**

First, find the dominant channel (Max) and the range of colors (Delta/Chroma).

$$
V = \max(R, G, B)
$$

$$
\Delta = V - \min(R, G, B)
$$

**B. Calculate Saturation (S)**

Saturation is the ratio of the color range to the brightness.

$$
S = \frac{\Delta}{V}
$$

$S \in [0, 1]$

> [!NOTE]
> *(If $V=0$, $S=0$)*

**C. Calculate Hue (H)**

Hue depends on which color channel is the maximum. The formula determines the sector of the color wheel ($60^{\circ}$ sectors).

$$
H = 60^{\circ} \cdot
\begin{cases}
\frac{G - B}{\Delta} & \text{if } V = R \text{ and } G \ge B \\
\frac{R - B}{\Delta} + 5 & \text{if } V = R \text{ and } G < B \\
\frac{B - R}{\Delta} + 2 & \text{if } V = G \\
\frac{R - G}{\Delta} + 4 & \text{if } V = B
\end{cases}
$$

$H \in [0^{\circ}, 360^{\circ}]$

### Summary and applications
Colours are good for indexing and retrieval, as well as colour-based segmentation.
