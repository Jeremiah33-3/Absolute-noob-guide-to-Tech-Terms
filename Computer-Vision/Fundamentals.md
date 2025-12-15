## Key Definitions and Concepts

### Machine Vision
> The seeing ability to machines, which includes image acquisition plus understanding.

### Vision
> The sense where qualities of an object's appearance are perceived through a process where light rays entering the eye are transformed into signals that pass to the brain.

### Pattern Recognition
> Automated recognition of patterns and regularities in data
> 
> Features include recognising and classifying unfamiliar and similar objects, accurately recognising shapes from different angles, identifying objects even when partly hidden, and dealing with diverse data.
> 
> A visual system is an image grabber plus an image processor

### Digital image
> A 2D, discrete, digital signal, limited in its domain (size or spatial, XY, domain, finite-length).
>
> Often a M $\times$ N or M $\times$ N $\times$ 3 or a matrix of integers
>
> A signal: a physical phenomenon which conveys information and energy.

### Colour Image
> An M $\times$ N $\times$ 3 matrix, with a 24-bit true colour standard where each pixel is an 8-bit number between 0 and 255 (3 pages/channels)
>
> 1st page is RED, next is GREEN, last is BLUE (OpenCV uses BGR format)
>
> M $\times$ N = resolution = spatial domain dimensions = number of pixels in columns/rows

### Grey-level/gray-scale image
> A digital image where each pixel represents a single shade of gray, ranging from black (0) to white (255), different shades of gray, single channel
- simplifies image data and reduces computational demands

## Human and Computer Vision System

| Human Vision System | Computer Vision System |
| :--- | :--- |
| Eye for sensing | Sensing device for input |
| Brain for interpreting | An interpreting device for output |

## Computer Vision System Workflow

Layers:
1. Data acquisition (sensing layer): using devices like cameras (RGB, infrared, stereo, etc.), video feeds (CCTV, drones, phones), or 3D sensors (e.g. LiDAR, Kinect)
2. (Model training/updating) Preprocessing: resizing, denoising, normalization, contrast enhancement, colour correction, converting formats
3. (Model training/updating) Processing: object detection/classification, object tracking, scene understanding, decision making/reasoning
4. Postprocessing & output delivery: JSON, alert, command, to a dashboard or actuator
5. Storage & Logging

## Operations

Possible application: logical operations, transforms, statistical operations, geometrical operations, mathematical operations, morphology/coding, fourier/walsh/PCA, histograms/correlation/max min, affine transforms, filtering

### Geometric Transformations

Geometric Transformations of digital images consist of two basic operations:
1. spatial transformation of coordinates
2. intensity interpolation that assigns intensity values to the spatially transformed pixels
