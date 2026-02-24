Tags:  [[_Unit -2]]

>**Unlike boundary-based methods (which detect edges), region-based methods group pixels based on similarity**.

# What is Region-Based Segmentation?

Instead of detecting boundaries, we:

> Group neighboring pixels that have similar properties.

Similarity may be based on:

- Intensity
- Color
- Texture
- Statistical properties

Mathematically:

If$$|f(x,y) - f(x',y')| < T  $$

then pixels belong to same region.

# Basic Region-Based Methods
1. Region Growing
2. Region Splitting and Merging
3. Clustering (K-means, etc.)

# 1. Region Growing

Start from a seed point.

Steps:

1. Choose seed pixel.
2. Compare neighbors.
3. Add similar pixels.
4. Repeat until no more pixels satisfy condition.

Condition example:
  $$|I_{neighbor} - I_{seed}| < T  $$

---

## Python Example – Simple Region Growing

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

img = cv2.imread("image.jpg", 0)

# Seed point
seed = (100, 100)
threshold = 10

segmented = np.zeros_like(img)
seed_value = img[seed]

rows, cols = img.shape

stack = [seed]

while stack:
    x, y = stack.pop()

    if segmented[x, y] == 0:
        if abs(int(img[x, y]) - int(seed_value)) < threshold:
            segmented[x, y] = 255

            # Add neighbors
            for dx in [-1,0,1]:
                for dy in [-1,0,1]:
                    nx, ny = x+dx, y+dy
                    if 0 <= nx < rows and 0 <= ny < cols:
                        stack.append((nx, ny))

plt.imshow(segmented, cmap='gray')
plt.title("Region Growing")
plt.axis("off")
plt.show()
```

---

# 2. Region Splitting and Merging

Based on Quad-tree decomposition.

### Splitting:

Divide image into 4 regions recursively if not homogeneous.

### Merging:

Combine adjacent regions if similar.

Homogeneity condition:
$$\sigma^2 < T$$  
(variance less than threshold)

---

# 3. Clustering (Very Important)

Clustering groups pixels based on similarity without spatial constraint.

Most common: **K-means clustering**

---

# K-Means Clustering

Goal:

Divide image into K clusters.

Algorithm:

1. Choose K cluster centers.
2. Assign each pixel to nearest center.
3. Update centers.
4. Repeat until convergence.

Distance metric:
$$d = ||x - \mu_k||$$  
---

# Python Code – K-Means Image Segmentation

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

img = cv2.imread("image.jpg")
img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)

# Reshape image
pixel_values = img_rgb.reshape((-1, 3))
pixel_values = np.float32(pixel_values)

# Define criteria
criteria = (cv2.TERM_CRITERIA_EPS + 
            cv2.TERM_CRITERIA_MAX_ITER, 100, 0.2)

K = 3
_, labels, centers = cv2.kmeans(pixel_values, 
                                 K, None, 
                                 criteria, 
                                 10, 
                                 cv2.KMEANS_RANDOM_CENTERS)

# Convert back to image
centers = np.uint8(centers)
segmented_data = centers[labels.flatten()]
segmented_image = segmented_data.reshape(img_rgb.shape)

plt.figure(figsize=(8,4))

plt.subplot(1,2,1)
plt.imshow(img_rgb)
plt.title("Original")
plt.axis("off")

plt.subplot(1,2,2)
plt.imshow(segmented_image)
plt.title("K-Means Segmentation")
plt.axis("off")

plt.show()
```



# Differences: Region vs Clustering

|Region-Based|Clustering|
|---|---|
|Uses spatial connectivity|No spatial constraint|
|Seed-based possible|Unsupervised|
|Good for local segmentation|Good for color grouping|

---
---
# Summary
## Advantages

- Works when edges are weak  
- Handles smooth regions well  
- Good for color segmentation

---

## Limitations

- Sensitive to threshold choice  
- K-means requires choosing K  
- May ignore spatial continuity

---

## Important Exam Points

- Region-based segmentation uses similarity.
- Region growing depends on seed selection.
- Splitting and merging use quad-tree.
- K-means is unsupervised clustering.
- Clustering ignores spatial relationship.

---


# Next: [[Template Matching]]