# 11.03.26
---
---

# 1. Gaussian Kernel

## Definition

A **Gaussian kernel** is a smoothing filter based on the **Gaussian (normal) distribution**.  
It is widely used in **image processing to reduce noise and smooth images** before further processing like edge detection.

The Gaussian function is:

$$G(x,y)=\frac{1}{2\pi\sigma^2}e^{-\frac{x^2+y^2}{2\sigma^2}}
$$

Where

- (x,y) = spatial coordinates
- ($\sigma$) = standard deviation (controls blur amount)

---

## Properties

### 1. Smooth and continuous

Gaussian produces **natural blurring** without sharp artifacts.

### 2. Isotropic

Blur is **equal in all directions**.

### 3. Noise reduction

High-frequency noise gets suppressed.

### 4. Controlled smoothing

Higher ($\sigma$ ) → stronger blur.

---

## Example Gaussian Kernel (3×3)

[  
$$
\frac{1}{16}  
\begin{bmatrix}  
1 & 2 & 1 \\  
2 & 4 & 2 \\  
1 & 2 & 1  
\end{bmatrix}  
$$

Characteristics

- Center pixel has highest weight
- Neighbor influence decreases with distance
---

## Purpose of Gaussian Filtering

Used before many image operations:

- Edge detection
- Feature extraction
- Image segmentation
- Computer vision preprocessing
Example pipeline

Image → Gaussian smoothing → Edge detection

---

# 2. Coherence

## Definition

**Coherence** describes the **consistency or similarity of pixel values or structures in a region** of an image.

It indicates whether **neighboring pixels follow a common pattern or direction**.

---

## Types of Coherence

### 1. Intensity Coherence

Neighboring pixels have **similar intensity values**.

Example

Smooth sky region in an image.

---

### 2. Directional Coherence

Edges or textures align in **a specific direction**.

Example

Wood grain patterns.

---

### 3. Motion Coherence (in video)

Objects move **in a consistent direction across frames**.

---

## Importance in Image Processing

Coherence helps in:

- Edge detection
- Texture analysis
- Optical flow
- Segmentation
- Object recognition

---

## Example

Edge region:

Pixels change rapidly → **low coherence**

Flat region:

Pixels similar → **high coherence**

---

# 3. Using Derivative of Gaussian Instead of Two Separate Operations

## Traditional Approach

Edge detection often uses **two steps**:

### Step 1: Smooth Image

Apply Gaussian filter to remove noise.

### Step 2: Apply Edge Operator

Use operators such as

- Sobel
- Prewitt
- Laplacian

Pipeline:

Image → Gaussian → Edge Operator

This requires **two convolutions**.

---

# Optimized Approach: Derivative of Gaussian (DoG)

Instead of applying **Gaussian first and derivative operator later**, we can combine both into **one single operator**.

Mathematically:

$$\frac{\partial}{\partial x}(G * f) = (\frac{\partial G}{\partial x}) * f  $$

Meaning:

Derivative of the smoothed image =  
Convolution of image with **derivative of Gaussian kernel**.

---

## Key Idea

Instead of

Gaussian → Sobel
we use
**Derivative of Gaussian kernel**
and apply it **once**.

---

## Why This Works

Because **differentiation and convolution commute**.

So
Smooth → Differentiate = Differentiate Gaussian → Convolve once

---

## Advantages

### 1. Faster computation

Only **one convolution operation**.

### 2. Better edge detection

Noise suppression and edge detection happen **simultaneously**.

### 3. More mathematically consistent

---

## Example: First Derivative of Gaussian


$$

\frac{\partial G}{\partial x} = -\frac{x}{2\pi\sigma^4} e^{-\frac{x^2+y^2}{2\sigma^2}}
$$


This kernel detects **horizontal intensity changes**.

Similarly


$\frac{\partial G}{\partial y}$  

detects **vertical edges**.

---

## Where This Idea Is Used

Many advanced edge detectors rely on this concept:

- Canny Edge Detector
- Scale-space edge detection
- Feature detection algorithms

---

# Conceptual Comparison

|Method|Steps|Convolutions|
|---|---|---|
|Gaussian + Sobel|Smooth then detect edge|2|
|Derivative of Gaussian|Combined operator|1|

---

# Simple Intuition

Imagine:

- Gaussian = **remove noise**
- Derivative = **detect change**
Instead of doing them **separately**,  
we create **one smart filter that does both together**.

---


Derivative of Gaussian is used because it

- smooths the image
- detects edges
- requires only **one convolution*
making it **efficient and mathematically elegant**.

---
---
---
# -->                                17.03.26                         <--
---
---

# 1. Convolution vs Correlation

## Definition

Both **convolution** and **correlation** are mathematical operations used in **image filtering**. They combine an **image** with a **kernel (filter)** to produce a new image.

---

## Convolution

### Mathematical Definition

$$
(f * g)(x,y) = \sum_{m}\sum_{n} f(m,n)\, g(x-m, y-n)
$$

Where

- (f) = input image
- (g) = filter/kernel
- Kernel is **flipped horizontally and vertically** before applying.

### Steps

1. Flip kernel
2. Place kernel over image pixel
3. Multiply overlapping values
4. Sum results
5. Assign to output pixel

### Example Kernel (Edge Detection)

$$
\begin{bmatrix}  
-1 & -1 & -1 \\  
-1 & 8 & -1 \\  
-1 & -1 & -1  
\end{bmatrix}  
$$

### Applications

- Edge detection
- Image sharpening
- Blurring
- Feature extraction

---

## Correlation

### Mathematical Definition
$$

(f \star g)(x,y) = \sum_{m}\sum_{n} f(x+m, y+n)\, g(m,n)
$$

### Key Difference

|Property|Convolution|Correlation|
|---|---|---|
|Kernel flipped|Yes|No|
|Used in|Signal processing|Pattern matching|
|Operation|Mathematical|Similarity measure|

---

# 2. Conversion from Function to Integer

Images in real-world mathematics are **continuous functions**, but computers store them as **integers**.

### Continuous Image

f(x,y)  

Where

- (x,y) = spatial coordinates
- (f) = intensity value

### Computer Representation

Image becomes:
f[i,j]  

Where

- (i,j) = pixel indices
- Values stored as integers (0–255 typically)

---

# 3. Digitization and Quantization

Digital image formation involves **two major steps**.

---

## Digitization

Digitization converts **continuous signals into digital form**.

It includes two processes:

### 1. Sampling

Converting **continuous spatial coordinates** into discrete pixels.
Example

Continuous image → grid of pixels.

---

### 2. Quantization

Mapping **continuous intensity values** into discrete levels.
Example

Real intensity:
0 – 1

Quantized:
0 – 255 (8-bit image)

---

## Example

Real value
0.742

Quantized value
190

---

# 4. Light is Frequency

Light behaves as an **electromagnetic wave**.

$c = \lambda f$  

Where

- (c) = speed of light
- (\lambda) = wavelength
- (f) = frequency

Different frequencies correspond to **different types of imaging**.

---

# 5. Images in Different Frequencies

Different imaging technologies use different parts of the **electromagnetic spectrum**.

|Imaging Method|Frequency Type|Application|
|---|---|---|
|Visible Light|Medium frequency|Cameras|
|X-ray|High frequency|Medical imaging|
|Ultrasound (Sonography)|Sound waves|Fetus imaging|
|Infrared|Heat radiation|Night vision|

---

## X-Ray Imaging

Uses **high-energy electromagnetic radiation** to penetrate body tissues.

Application:

- Bone fracture detection
- Lung examination
---

## Sonography (Ultrasound)

Uses **high-frequency sound waves** instead of light.

Application:

- Pregnancy monitoring
- Organ imaging
---

# 6. Image in Time Domain

Images are normally considered **spatial signals**.

But video images also change over **time**.

Thus:

$f(x,y,t)$  

Where

- (x,y) = spatial coordinates
- (t) = time

Example

Video = sequence of images.

Applications

- Motion detection
- Surveillance
- Video compression

---

# 7. A Pixel Needs Neighbours to Provide Information

A **single pixel has very little meaning alone**.

Information comes from **neighboring pixels**.

Example:

Edge detection works by comparing **intensity differences between neighbors**.

Neighborhood types:

### 4-Neighbourhood

Up, Down, Left, Right

### 8-Neighbourhood

Includes diagonal pixels.

Importance:

- Edge detection
- Texture analysis
- Image segmentation

---

# 8. Edge Detection Operators

Edge detection identifies **sudden intensity changes**.

---

# Sobel Operator

Detects edges using **gradient approximation**.

Horizontal filter:

$$
  
\begin{bmatrix}  
-1 & 0 & 1 \\  
-2 & 0 & 2 \\  
-1 & 0 & 1  
\end{bmatrix}  
$$

Vertical filter:

$$\begin{bmatrix}  
-1 & -2 & -1 \\  
0 & 0 & 0 \\  
1 & 2 & 1  
\end{bmatrix}  


$$
Features

- Smooths noise slightly
- Widely used

---

# Prewitt Operator

Similar to Sobel but **simpler weights**.

Horizontal kernel

$$

\begin{bmatrix}  
-1 & 0 & 1 \\  
-1 & 0 & 1 \\  
-1 & 0 & 1  
\end{bmatrix}  
$$

Vertical kernel

$$
\begin{bmatrix}  
1 & 1 & 1 \\  
0 & 0 & 0 \\  
-1 & -1 & -1  
\end{bmatrix}  

$$

---

# Laplacian Operator

Uses **second derivative** to detect edges.
$$
\nabla^2 f = \frac{\partial^2 f}{\partial x^2} + \frac{\partial^2 f}{\partial y^2}
$$

Kernel example

$$
\begin{bmatrix}  
0 & -1 & 0 \\  
-1 & 4 & -1 \\  
0 & -1 & 0  
\end{bmatrix}  
$$

Properties

- Detects edges in all directions
- Sensitive to noise

---

# Compass Operators

Detect edges in **specific directions**.

Examples

- Kirsch
- Robinson
- Frei-Chen

They analyze **8 directions**:

N, NE, E, SE, S, SW, W, NW

Used in:

- directional edge detection
- texture analysis

---

# 9. Image Smoothing Filters

Used to **remove noise**.

---

## Mean Filter

Averages pixel values.

Kernel
$$

\frac{1}{9}  
\begin{bmatrix}  
1 &1 &1\\  
1 &1 &1\\  
1 &1 &1  
\end{bmatrix}  
$$

Effect

- Reduces noise
- Blurs edges

---

## Median Filter

Replaces pixel with **median value** of neighbors.
Example

Values:
2, 4, 6, 7, 100

Median = 6

Good for removing **salt-and-pepper noise**.

---

## Gaussian Filter

Uses **Gaussian distribution** for smoothing.

$G(x,y) = \frac{1}{2\pi \sigma^2} e^{-\frac{x^2+y^2}{2\sigma^2}}$

Advantages

- Smooth blur  
- Preserves structures better than mean filter


---

# 10. Pixel as a Vector

???

---

# 11. Pixel Representation Using Polar Coordinates

????

---

# 12. Pixel as Complex Number

???

---

# 13. Color Representation

---

# RGB Color Model

RGB uses Red, Green, Blue

Pixel example

(255,0,0) = Red

### Problem

RGB is **non-linear and not perceptually uniform**.
Small numerical changes do **not correspond to equal visual change**.

Also

- difficult to separate brightness and color.

---

# HSV / HSI Color Models

These represent color more **similar to human perception**.

Components

|Component|Meaning|
|---|---|
|H|Hue (color type)|
|S|Saturation (purity)|
|V/I|Brightness|

Shape representation

HSV/HSI forms a **cone or cylinder**.

Why useful?

- color segmentation
- object tracking
- color detection
---

# 14. Problems of 2D Representation

Real world is **3D**, but images are **2D projections**.

This causes problems:

### Depth Loss

Distance information disappears.

### Occlusion

Objects hide behind others.

### Perspective distortion

Objects appear smaller when far.

### Lighting effects

Same object may look different under different illumination.

---


---

