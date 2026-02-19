2026-02-19  16:10
Status: 
Tags: [[Image Analysis]]
# Definition

**Hit-or-Miss Transformation (HMT)** is a morphological operation used for:

> **Detecting a specific shape or pattern in a binary image.**

It finds locations where a certain **foreground pattern (hit)** exists and a certain **background pattern (miss)** exists **at the same time**.

# Simple Idea

Hit-or-miss checks:
> “Does THIS exact pattern exist here?”

It is like a **template matcher**, but using morphology.
You define:

- What should be **white (object)**
- What should be **black (background)**

Only if:  
- foreground pattern matches  
- background pattern matches  
- → pixel = white (hit)  
- Else → black (miss)
# Main Concept

Because pattern detection needs:

- Foreground structure (`B₁`)
- Background structure (`B₂`

Example: detect a T-shape  
You must say:
- where object pixels must exist
- where background pixels must exist
---
Suppose we want to detect vertical lines
Foreground kernel B₁:

```
0 1 0
0 1 0
0 1 0
```

Background kernel B₂:

```
1 0 1
1 0 1
1 0 1
```

Only pure vertical lines will match.


# Mathematical Formula

Mathematically:  

$A \otimes (B_1, B_2) = (A \ominus B_1) \cap (A^c \ominus B_2)$ 

Where:

- `A` = input binary image
- `Aᶜ` = complement of A
- `B₁` = structuring element for foreground
- `B₂` = structuring element for background
- `⊖` = erosion   
- `∩` = intersection
# Working

Given:
- Binary image A
- Structuring elements B₁ and B₂
### Step 1: Erode A with B₁  

   $E_1 = A \ominus B_1$       
- Keeps only pixels where **foreground pattern fits**
### Step 2: Complement image

$A^c = 255 - A$  
### Step 3: Erode Aᶜ with B₂

$E_2 = A^c \ominus B_2$  
Keeps only pixels where **background pattern fits**

### Step 4: AND the results
 
$Result = E_1 \cap E_2$  

Only locations where **both conditions match** survive.

### Pixel level logic 
Output pixel = 1, if:
- All 1’s in `B₁` match 1’s in image
- All 1’s in `B₂` match 0’s in image

So it is:

> **exact shape detection**
# Code
```python
import cv2
import numpy as np

# Load binary image
img = cv2.imread("image.png", cv2.IMREAD_GRAYSCALE)
_, binary = cv2.threshold(img, 127, 255, cv2.THRESH_BINARY)

# Define structuring elements
B1 = np.array([[0,1,0],
               [0,1,0],
               [0,1,0]], dtype=np.uint8)

B2 = np.array([[1,0,1],
               [1,0,1],
               [1,0,1]], dtype=np.uint8)

# Convert kernels to 255 format
B1 = B1 * 255
B2 = B2 * 255

# Step 1: Erode A with B1
E1 = cv2.erode(binary, B1)

# Step 2: Complement image
binary_comp = cv2.bitwise_not(binary)

# Step 3: Erode complement with B2
E2 = cv2.erode(binary_comp, B2)

# Step 4: AND
hit_or_miss = cv2.bitwise_and(E1, E2)

# Show results
cv2.imshow("Original", binary)
cv2.imshow("Hit-or-Miss", hit_or_miss)
cv2.waitKey(0)
cv2.destroyAllWindows()
```


# Merits | Demerits | Constraints
## Applications
#### 1. Pattern Detection
- Detect corners
- Detect endpoints
- Detect junctions
- Detect specific shapes

#### 2. Skeleton Analysis
- Finding endpoints in skeleton
- Finding branch points
#### 3. OCR
- Detect characters like T, L, +
#### 4. Medical Imaging
- Detect specific cell structures
## Limitations

1. Works only on **binary images**  
2. Very sensitive to:
- rotation
- scale
- noise  
3. Kernel must match exactly  
4. Computationally expensive if many patterns need

## Uses:
### - Thinning
Uses hit-or-miss repeatedly to remove boundary pixels
### - Skeletonization
Uses hit-or-miss to peel layers
### - Corner detection
Uses multiple rotated hit-or-miss kernels
# Summary

| Feature     | Hit-or-Miss                    |
| ----------- | ------------------------------ |
| Purpose     | Exact shape detection          |
| Needs       | Foreground + background kernel |
| Image type  | Binary only                    |
| Output      | Detected pattern locations     |
| Sensitivity | Very high                      |


| Operation   | Role              |
| ----------- | ----------------- |
| Erosion     | Pattern fit check |
| Dilation    | Pattern grow      |
| Opening     | Noise removal     |
| Closing     | Hole filling      |
| Hit-or-miss | Shape detection   







# Next: [[]]