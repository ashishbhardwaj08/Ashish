2026-02-23  14:04
Tags: [[Image Analysis]]
# Definition
Connected component extraction means:

> **Finding and labeling each separate object** in a binary image.

So instead of:

```
██   ██
██   ██
```

We label them as:

```
1   2
1   2
```

Each object becomes a separate region.

# Purpose


# Main Concept
Two pixels are connected if:

- They have the **same value (white)**
- They are neighbors (4-connected or 8-connected)

# Mathematical Formula

**Connected components** =  
Find all maximal connected sets of foreground pixels.

Connectivity:

- **4-connected** → up, down, left, right
- **8-connected** → includes diagonals

# Working

1. Convert image to binary
2. Scan image pixel by pixel
3. Group pixels that touch each other
4. Assign unique label to each group
5. Output labeled regions


# Code
```python
import cv2
import numpy as np

img = cv2.imread("binary.png", 0)
_, binary = cv2.threshold(img, 127, 255, cv2.THRESH_BINARY)

num_labels, labels = cv2.connectedComponents(binary)

print("Number of objects:", num_labels-1)  # excluding background

# Color each component
colored = np.zeros((binary.shape[0], binary.shape[1], 3), dtype=np.uint8)

for label in range(1, num_labels):
    colored[labels == label] = np.random.randint(0,255, size=3)

cv2.imshow("Connected Components", colored)
cv2.waitKey(0)
```

# Merits | Demerits | Constraints
### Applications

- Counting objects  
- Blob detection  
- Cell counting  
- License plate characters  
- Industrial inspection





# Next: [[Convex hull]]