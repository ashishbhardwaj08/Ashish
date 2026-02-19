2026-02-19  16:52
Status: 
Tags: [[Image Analysis]]
# Definition
Region filling means:
> **Filling holes or empty regions inside an object** in a binary image.

In simple words:  
If an object has a hollow part (black area inside white), region filling makes it **solid white**.
# Basic Idea

Suppose you have a donut-shaped object
There is a hole inside.
We:
1. Pick a point inside the hole (seed point)
2. Expand from that point
3. Stop when we reach object boundary

So we fill:

> Only the region connected to the seed point.

# Main Concept

Region filling is done using:

- **Complement of image**
- **Marker image (seed point inside hole)**
- **Iterative dilation + AND operation**

It is based on **morphological reconstruction**.
Original:

 ██████
 ██       ██ 
 ██       ██ 
 ██████`

Hole inside object.

After region filling:
 ██████ 
 ██████
 ██████ 
 ██████`
# Mathematical Formula

$X_k = (X_{k-1} ⊕ B) \cap A^c$  

Where:

- (A) = original binary image
- (A^c) = complement of A
- $(X_0)$ = marker (seed point inside hole)
- (B) = structuring element
- ⊕ = dilation
- ∩ = intersection  
    Repeat until $(X_k = X_{k-1})$

Final filled image:  
$Filled = X_k \cup A$  
# Working
#### Step 1: Choose seed point
Must be inside hole
#### Step 2: Initialize X₀
Binary image with only seed point white.
#### Step 3: Iterative dilation + intersection
Grow region until no change.
#### Step 4: Combine with original
Union gives filled object.

# Code
```python
import cv2
import numpy as np

img = cv2.imread("binary.png", 0)
_, binary = cv2.threshold(img, 127, 255, cv2.THRESH_BINARY)

# Copy image and create mask
h, w = binary.shape
mask = np.zeros((h+2, w+2), np.uint8)

# Flood fill from (0,0) background
floodfill = binary.copy()
cv2.floodFill(floodfill, mask, (0,0), 255)

# Invert floodfilled image
floodfill_inv = cv2.bitwise_not(floodfill)

# Combine with original to fill holes
filled = binary | floodfill_inv

cv2.imshow("Original", binary)
cv2.imshow("Region Filled", filled)
cv2.waitKey(0)
#
#
#
#
```

# Merits | Demerits | Constraints

| Parameter          | Effect                    |
| ------------------ | ------------------------- |
| Kernel size        | Controls growth direction |
| Connectivity (4/8) | Affects fill shape        |
| Seed location      | Determines region         |

| Region Filling        | Closing                      |
| --------------------- | ---------------------------- |
| Needs seed            | No seed                      |
| Fills specific region | Fills small holes everywhere |
| Controlled            | Automatic                    |
| Iterative             | One operation                |
# Summary

|Feature|Region Filling|
|---|---|
|Purpose|Fill holes|
|Needs|Seed point|
|Type|Iterative|
|Based on|Dilation + Intersection|
|Image type|Binary|




# Next: [[Convex hull]]