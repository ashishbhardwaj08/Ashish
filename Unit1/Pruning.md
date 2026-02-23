2026-02-23  14:27
Tags: [[Image Analysis]]
# Definition


Pruning means:

> Removing small unwanted branches (spurs) from a skeleton.

After skeletonization, small noisy branches often appear.
# Basic Idea
Skeletonization may produce:

- small spurious branches
- noisy endpoints
- irregular tiny extensions

Pruning cleans the skeleton for:  
- OCR  
- fingerprint analysis  
- road detection 
- shape matching


Example:
Skeleton:

```
     |
-----|---  -
     |
     *
```

That small `*` branch and `-` branch is noise.

After pruning:

```
     |
-----|---
     |
```

# Main Concept


# Mathematical Formula
Pruning uses:

- Hit-or-Miss transformation
- Endpoint detection
- Iterative deletion

General idea:
 
$Pruned = Skeleton - SmallBranches$  

More formally:

1. Detect endpoints
---
`Endpoint pattern example:

```
0 0 0
0 1 0
0 1 0
```
---
2. Remove endpoints iteratively
3. Stop after fixed number of iterations

# Working

1. Start with skeleton image
2. Detect thin branch endpoints
3. Remove them
4. Repeat few iterations
5. Small branches disappear

# Code
```python
import cv2
import numpy as np

img = cv2.imread("skeleton.png", 0)
_, skeleton = cv2.threshold(img, 127, 255, cv2.THRESH_BINARY)

kernel = np.ones((3,3), np.uint8)

pruned = skeleton.copy()

# Remove small branches (3 iterations example)
for i in range(3):
    eroded = cv2.erode(pruned, kernel)
    pruned = cv2.subtract(pruned, eroded)

cv2.imshow("Original Skeleton", skeleton)
cv2.imshow("Pruned Skeleton", pruned)
cv2.waitKey(0)
```


# Summary

|Operation|Purpose|
|---|---|
|Thinning|Reduce to 1-pixel width|
|Skeleton|True medial axis|
|Pruning|Remove small unwanted branches|



# Next: [[Grayscale Morphology]]