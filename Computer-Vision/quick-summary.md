# Table of content
- [Goals of CV](#Goals-of-CV)
- [Digital Images](#Digital-Images)

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
