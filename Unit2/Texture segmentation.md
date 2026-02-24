## Texture

Texture refers to **spatial arrangement of intensity variations** in an image.

Unlike edges (which are abrupt intensity changes), texture represents:

- Repeated patterns
- Smooth vs rough surfaces
- Regular vs irregular patterns
- Fine vs coarse structures

Examples:

- Grass vs road
- Fabric vs wall
- Brick vs sky
- Tumor tissue vs normal tissue

Texture segmentation separates regions based on **statistical or structural properties**, not just intensity.
`Simple image analysis cannot detect differences between different materials that have same look or colour.`

---
# Why Intensity Segmentation Fails for Texture

Consider:

- A white wall and white cloth → same intensity
- But cloth has repetitive patterns
- Wall is smooth

Intensity thresholding cannot separate them.  
Texture analysis can.

# 🔷 Main Approaches for Texture Segmentation

1. Statistical Methods
2. Filter-Based Methods
3. Structural Methods
4. Model-Based Methods
5. Transform-Based Methods


# 1. Statistical Texture Segmentation

Texture is characterized using statistical features from a local window.

### Two Types:

### A) First Order Statistics (Histogram Based)

Uses:

- Mean
- Variance
- Standard deviation
- Entropy

But these ignore spatial relationships.

---

### B) Second Order Statistics – GLCM

Most important method.

Uses:

## ➜ Gray Level Co-occurrence Matrix (GLCM)

---

## GLCM Concept

GLCM measures how often pairs of pixels occur with specific values and spatial relationship.

It captures:

- Spatial dependency
- Directional information
- Texture patterns

---

## Steps of GLCM Texture Segmentation

1. Convert image to grayscale
2. Define displacement (distance d, angle θ)
3. Compute GLCM
4. Extract features
5. Cluster or threshold

---

## Important GLCM Features

Let P(i,j) be normalized GLCM.

### 1. Contrast

Measures intensity variation.
$$Contrast = \sum (i-j)^2 P(i,j) $$

High → rough texture  
Low → smooth texture

---

### 2. Energy

Uniformity measure.
$$Energy = \sum P(i,j)^2  $$
High → regular texture

---

### 3. Homogeneity

Measures closeness to diagonal. 
$$Homogeneity = \sum \frac{P(i,j)}{1+|i-j|}  $$

---

### 4. Entropy

Randomness measure.
$$Entropy = -\sum P(i,j)\log P(i,j)$$

High → complex texture

---

# Sliding Window Texture Segmentation

Instead of computing GLCM for entire image:

- Use small window (e.g., 7×7 or 11×11)
- Compute texture features at each pixel
- Create feature maps
- Apply clustering

---

# Python Code – GLCM Texture Segmentation

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
from skimage.feature import graycomatrix, graycoprops
from sklearn.cluster import KMeans

# Load image
img = cv2.imread("texture.jpg", 0)

# Reduce gray levels for better GLCM
img = (img / 16).astype(np.uint8)

window_size = 15
pad = window_size // 2

# Pad image
padded = cv2.copyMakeBorder(img, pad, pad, pad, pad, cv2.BORDER_REFLECT)

contrast_map = np.zeros(img.shape)

for i in range(img.shape[0]):
    for j in range(img.shape[1]):
        window = padded[i:i+window_size, j:j+window_size]
        
        glcm = graycomatrix(window,
                            distances=[1],
                            angles=[0],
                            levels=16,
                            symmetric=True,
                            normed=True)
        
        contrast = graycoprops(glcm, 'contrast')[0,0]
        contrast_map[i,j] = contrast

# Normalize feature map
contrast_map = cv2.normalize(contrast_map, None, 0, 255, cv2.NORM_MINMAX)
contrast_map = contrast_map.astype(np.uint8)

# K-means clustering
flat = contrast_map.reshape((-1,1))
kmeans = KMeans(n_clusters=2, random_state=0).fit(flat)
segmented = kmeans.labels_.reshape(img.shape)

plt.figure(figsize=(12,5))
plt.subplot(1,3,1); plt.imshow(img, cmap='gray'); plt.title("Original")
plt.subplot(1,3,2); plt.imshow(contrast_map, cmap='gray'); plt.title("Contrast Map")
plt.subplot(1,3,3); plt.imshow(segmented, cmap='gray'); plt.title("Texture Segmentation")
plt.show()
```

---

# Filter-Based Texture Segmentation

Uses special filters that respond to textures.

Common filters:

- Gabor filters
- Laws’ texture masks
- Wavelets

---

## Gabor Filter Based Texture

Uses:

## ➜ Gabor filter

---

## Why Gabor?

Gabor filter:

- Sensitive to specific frequency
- Sensitive to specific orientation
- Mimics human visual system

Very powerful for texture classification.

---

## Gabor Filter Equation

$$G(x,y) = e^{-\frac{x^2 + y^2}{2\sigma^2}}  
\cos(2\pi fx + \phi)  $$

Where:

- σ = Gaussian spread
- f = frequency
- θ = orientation
- φ = phase
---

## Python Code – Gabor Texture Segmentation

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
from sklearn.cluster import KMeans

img = cv2.imread("texture.jpg", 0)

# Apply multiple Gabor filters
kernels = []
for theta in np.arange(0, np.pi, np.pi / 4):
    kernel = cv2.getGaborKernel((21,21), 5.0, theta, 10.0, 0.5, 0, ktype=cv2.CV_32F)
    kernels.append(kernel)

features = []

for kernel in kernels:
    filtered = cv2.filter2D(img, cv2.CV_8UC3, kernel)
    features.append(filtered)

# Stack features
feature_stack = np.stack(features, axis=-1)

# Reshape for clustering
h, w, d = feature_stack.shape
flat = feature_stack.reshape((-1, d))

kmeans = KMeans(n_clusters=2, random_state=0).fit(flat)
segmented = kmeans.labels_.reshape(h, w)

plt.figure(figsize=(12,5))
plt.subplot(1,2,1); plt.imshow(img, cmap='gray'); plt.title("Original")
plt.subplot(1,2,2); plt.imshow(segmented, cmap='gray'); plt.title("Gabor Texture Segmentation")
plt.show()
```

---

# Laws’ Texture Energy Method

Uses special 1D kernels:

L5 = [1 4 6 4 1]  
E5 = [-1 -2 0 2 1]  
S5 = [-1 0 2 0 -1]  
W5 = [-1 2 0 -2 1]  
R5 = [1 -4 6 -4 1]

2D masks are formed by outer products.

Energy is computed in local window.

---

# Wavelet-Based Texture Segmentation

Uses:

## ➜ Discrete Wavelet Transform

Wavelets:
- Decompose image into frequency bands
- Capture texture at multiple scales
- Very powerful for medical imaging

---

# Clustering-Based Texture Segmentation

After extracting texture features:

Use:

- K-means
- Fuzzy C-means
- Mean shift
- Spectral clustering

---

# Performance Factors in Texture Segmentation

1. Window size selection
2. Number of clusters
3. Feature normalization
4. Noise sensitivity
5. Computation time

---

# Comparison of Methods

|Method|Accuracy|Speed|Complexity|
|---|---|---|---|
|GLCM|High|Slow|Medium|
|Gabor|Very High|Medium|High|
|Laws|Medium|Fast|Low|
|Wavelets|Very High|Medium|High|

---

# Important Viva Points

- Texture ≠ intensity
- GLCM captures spatial dependency
- Gabor captures frequency + orientation
- Window size affects resolution
- Feature selection is critical

---

# ==END OF UNIT - 2==