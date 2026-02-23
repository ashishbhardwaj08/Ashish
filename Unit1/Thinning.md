2026-02-23  14:13
Tags: [[Image Analysis]]
# Definition
Thinning (Skeletonization) means:

> Reducing a binary object to a **1-pixel wide skeleton** while preserving its shape and connectivity.

# Basic Idea
It keeps:
- shape
- topology
- connectivity
But removes:
- Extra thickness

---
Original:

```
██████
██████
██████
```

After thinning:

```
  ██
  ██
  ██
```

Only the “center line” remains.
# Main Concept

Thinning works by:

1. Repeatedly removing boundary pixels
2. But **not removing pixels that break connectivity**

It uses:

- Hit-or-Miss transform
- Special structuring elements
- Iterative deletion

# Mathematical Formula

Skeleton of set (A):

$S(A) = \bigcup_{k=0}^{\infty} (A ⊖ kB) - ((A ⊖ kB) \circ B)$  

Where:

- ⊖ = erosion
- ∘ = opening
- B = structuring element

This keeps only the “center” structure.
# Working

Loop until object disappears:

1. Erode image
2. Open eroded image
3. Subtract → get boundary difference
4. Add to skeleton
5. Repeat

Final result → thin 1-pixel wide structure.

# Code

> OpenCV doesn’t have direct skeleton function, so we do manual skeletonization:

```python
import cv2
import numpy as np

img = cv2.imread("binary.png", 0)
_, binary = cv2.threshold(img, 127, 255, cv2.THRESH_BINARY)

binary = binary // 255  # Convert to 0 and 1

skeleton = np.zeros(binary.shape, np.uint8)
kernel = cv2.getStructuringElement(cv2.MORPH_CROSS, (3,3))

temp = np.zeros(binary.shape, np.uint8)

while True:
    eroded = cv2.erode(binary, kernel)
    opened = cv2.morphologyEx(eroded, cv2.MORPH_OPEN, kernel)
    temp = eroded - opened
    skeleton = cv2.bitwise_or(skeleton, temp)
    binary = eroded.copy()

    if cv2.countNonZero(binary) == 0:
        break

skeleton = skeleton * 255

cv2.imshow("Skeleton", skeleton)
cv2.waitKey(0)
```

# Merits | Demerits | Constraints
### Applications

- OCR character recognition  
- Fingerprint analysis  
- Road extraction in satellite images  
- Shape matching  
- Medical vessel detection



# Summary

| Thinning                  | Erosion               |
| ------------------------- | --------------------- |
| Preserves connectivity    | May break object      |
| Produces 1-pixel skeleton | Shrinks entire object |
| Iterative process         | Single operation      |



# Next: [[Thickening]]