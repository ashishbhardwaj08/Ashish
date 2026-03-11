---

# 🧱 PART 1: BLOCK EFFECT

---
# Boundary Extraction & Representation

---

## DEFINITION

**Connectivity** defines **how pixels are considered neighbors of each other** in a digital image and determines whether two pixels belong to the **same region or boundary**.

In boundary extraction, connectivity tells us:

> “Are these two pixels part of the same object boundary?”

It is the foundation for:  
Contour tracing  
Region labeling  
Edge linking  
Shape extraction

---

## TYPES OF CONNECTIVITY

### 4–Connectivity

A pixel is connected to its **up, down, left, right** neighbors.

```
   (x-1,y)
(x,y-1)  P  (x,y+1)
   (x+1,y)
```

Used when:  
Want simple connections  
Avoid diagonal linking

---

### 8–Connectivity

A pixel is connected to **all 8 surrounding pixels**.

```
(x-1,y-1) (x-1,y) (x-1,y+1)
(x, y-1)     P     (x,y+1)
(x+1,y-1) (x+1,y) (x+1,y+1)
```

Used when:  
Diagonal boundaries exist  
More natural shapes

---

### Mixed Connectivity (m-connectivity)

Avoids ambiguous diagonal connections:  
Diagonal pixels are connected only if they do NOT share a common 4-neighbor.

Used in:  
Medical imaging  
Noise-sensitive segmentation

---

## WORKING PRINCIPLE (STEP-BY-STEP)

Assume we have a **binary image** (foreground = 1, background = 0)

### Step 1: Pick a foreground pixel

Start from any pixel with value 1.

### Step 2: Check neighbors

Based on connectivity rule:  
• 4-connectivity → check 4 neighbors  
• 8-connectivity → check 8 neighbors

### Step 3: If neighbor = 1

Then that neighbor is part of same region/boundary.

### Step 4: Continue recursively

Repeat until all connected pixels are found.

This is implemented using:  
Flood fill  
DFS  
BFS  
Union-find  
Contour following

---

## CODE (CONNECTIVITY USING OPENCV)

### Connected Components (8-connectivity)

```python
import cv2
import numpy as np

# Read binary image
img = cv2.imread("binary.png", 0)

# Threshold to ensure binary
_, binary = cv2.threshold(img, 127, 255, cv2.THRESH_BINARY)

# Connected components
num_labels, labels = cv2.connectedComponents(binary, connectivity=8)

print("Number of connected components:", num_labels)

# Color each component
output = np.zeros((binary.shape[0], binary.shape[1], 3), dtype=np.uint8)

for i in range(1, num_labels):
    mask = labels == i
    output[mask] = np.random.randint(0,255,3)

cv2.imshow("Connected Regions", output)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

---

### Contour extraction (connectivity-based)

```python
contours, hierarchy = cv2.findContours(binary, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_NONE)

cv2.drawContours(img, contours, -1, (255,0,0), 2)
cv2.imshow("Contours", img)
cv2.waitKey(0)
```

Contours rely directly on pixel connectivity.

---

## APPLICATIONS

### Boundary Extraction

Connectivity helps determine which pixels form the same boundary.
Used in:  
Object outline detection  
Shape analysis

---

### Region Labeling

Used in:  
OCR  
Medical segmentation  
Satellite image segmentation

Example:  
Each connected tumor region is one label.

---

### Edge Linking

Connectivity links broken edges into continuous boundaries.

Used in:  
Road detection  
Crack detection  
Face segmentation

---

### Shape Representation

Before using:  
Chain codes  
Fourier descriptors  
B-splines

We must know which pixels are connected.

---

## LIMITATIONS

### Noise Sensitivity

Small noisy pixels may be falsely connected.

Solution:  
Morphological opening  
Smoothing

---

### Ambiguous Diagonal Connections

In 8-connectivity, diagonal pixels may join separate objects incorrectly.

Solution:  
Use m-connectivity

---

### Cannot Handle Gray Images

Connectivity works best on:  
Binary images  
Thresholded edges

Needs preprocessing for grayscale.

---

### Topology Errors

Thin connections may break:  
Weak edges  
Low contrast boundaries

---

## SUMMARY

| Concept        | Meaning                         |
| -------------- | ------------------------------- |
| Connectivity   | Defines neighbor relationship   |
| 4-connectivity | Horizontal & vertical neighbors |
| 8-connectivity | All 8 surrounding pixels        |
| Used for       | Region extraction, contours     |
| Key role in    | Boundary representation         |

---

