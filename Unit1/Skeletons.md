2026-02-23  14:22
Tags: [[Image Analysis]]

==**Medial Axis Transform**==
# Definition
The **Skeleton** of a binary object is:

> The set of points that are **equidistant from the object boundaries**.

It represents the **true centerline structure** of a shape.

Think of it as:  
🧠 The “bones” of the object.

# Basic Idea

Original object:

```
████████
████████
████████
```

Skeleton:

```
   ████
   ████
   ████
```

For complex shapes:

Original:

```
   ███
 ███████
   ███
```

Skeleton:

```
   █
 █████
   █
```


# Main Concept

Imagine:

1. Fire starts from all boundaries
2. Fire moves inward at equal speed
3. Where fire fronts meet → that forms the skeleton

Those meeting points are:  
- Equidistant from boundaries  
- Central structure
# Mathematical Formula

Skeleton of set (A):

$S(A) = \bigcup_{k=0}^{K} S_k(A)$  

Where:

$S_k(A) = (A ⊖ kB) - ((A ⊖ kB) \circ B)$  

Where:

- ⊖ = erosion
- ∘ = opening
- B = structuring element

This extracts center components at each erosion stage.
# Working

1. Convert to binary
2. Compute distance transform  
    → Each pixel stores distance from nearest boundary
3. Maximum distance points form skeleton
4. Threshold distance map


# Code
This is the **correct skeleton approach**.

```python
import cv2
import numpy as np

img = cv2.imread("binary.png", 0)
_, binary = cv2.threshold(img, 127, 255, cv2.THRESH_BINARY)

# Distance Transform
dist = cv2.distanceTransform(binary, cv2.DIST_L2, 5)

# Normalize for display
dist_norm = cv2.normalize(dist, None, 0, 255, cv2.NORM_MINMAX)
dist_norm = np.uint8(dist_norm)

# Threshold distance map to get skeleton
_, skeleton = cv2.threshold(dist_norm, 40, 255, cv2.THRESH_BINARY)

cv2.imshow("Original", binary)
cv2.imshow("Distance Map", dist_norm)
cv2.imshow("Skeleton", skeleton)
cv2.waitKey(0)
```


# Merits | Demerits | Constraints

## Applications

- Shape analysis  
- Road centerline extraction  
- Medical vessel detection  
- Fingerprint recognition  
- Pattern recognition


# Summary


Skeleton has two key properties:

1. **Topology preserved**
2. **Reconstruction possible**

Original image can be reconstructed by:

$A = \bigcup_{k} (S_k ⊕ kB)$  


|Skeleton|Thinning|
|---|---|
|True medial axis|Approximate centerline|
|Based on distance from boundary|Based on pattern deletion|
|More mathematically correct|More practical|
|Can reconstruct original shape|May not fully reconstruct|

Important:

> Skeleton allows reconstruction of original image.


# Next: [[Pruning]]