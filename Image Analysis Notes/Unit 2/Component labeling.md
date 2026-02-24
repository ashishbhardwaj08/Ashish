Tags:  [[_Unit -2]]

# **`Component Labeling (Connected Component Analysis – CCA)

# What is Component Labeling?

After thresholding, we get a **binary image**:

- Object pixels → 1 (white)
- Background pixels → 0 (black)

But there may be multiple objects.

Component labeling:

> Assigns a unique label to each connected region (object).

Example:

Before labeling:

```
1 1 0 0
1 1 0 1
0 0 0 1
```

After labeling:

```
1 1 0 0
1 1 0 2
0 0 0 2
```

Now:

- Object A → label 1
- Object B → label 2
# Connectivity

There are two types:
## 4-Connectivity

Pixel connected to:

- Up
- Down
- Left
- Right

## 8-Connectivity

Pixel connected to:

- All 8 neighbors

Choice affects number of components.

---

# Algorithm (Two-Pass Algorithm – Theory)

### First Pass:

- Scan image row by row
- Assign temporary labels
- Store equivalences

### Second Pass:

- Resolve equivalent labels
- Assign final labels

---

# Mathematical Definition

Let binary image be:
 
$$B(x,y) \in {0,1} $$ 

Two pixels are connected if:

- Both are 1
- They satisfy connectivity rule

Each connected region gets unique label:
$$L(x,y) \in {1,2,3,...,n}  
$$
---

# Uses

Used for:

- Object counting  
- Shape analysis  
- Region extraction  
- Feature extraction

---

# Connected Components Code

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

# Read grayscale image
img = cv2.imread("image.jpg", 0)

# Threshold to get binary image
_, binary = cv2.threshold(img, 127, 255, cv2.THRESH_BINARY)

# Connected Component Analysis
num_labels, labels = cv2.connectedComponents(binary)

print("Number of components:", num_labels - 1)

# Convert labels to color image for visualization
label_hue = np.uint8(179 * labels / np.max(labels))
blank = 255 * np.ones_like(label_hue)
colored = cv2.merge([label_hue, blank, blank])
colored = cv2.cvtColor(colored, cv2.COLOR_HSV2BGR)
colored[label_hue == 0] = 0

# Display
plt.figure(figsize=(12,4))

plt.subplot(1,3,1)
plt.imshow(img, cmap='gray')
plt.title("Original")
plt.axis("off")

plt.subplot(1,3,2)
plt.imshow(binary, cmap='gray')
plt.title("Binary Image")
plt.axis("off")

plt.subplot(1,3,3)
plt.imshow(colored)
plt.title("Labeled Components")
plt.axis("off")

plt.show()
```

---

# Output Explanation

- Each object has different color
- num_labels includes background
- So actual objects = num_labels − 1

---

# 4 vs 8 Connectivity in OpenCV

```python
num_labels, labels = cv2.connectedComponents(binary, connectivity=4)
```

or

```python
num_labels, labels = cv2.connectedComponents(binary, connectivity=8)
```

---

# Performance Characteristics

|Property|Component Labeling|
|---|---|
|Works on|Binary images|
|Detects|Regions|
|Sensitive to noise|Yes|
|Fast|Yes|
|Used for|Counting, region extraction|

---

# Applications

- Cell counting in microscopy
- Counting vehicles
- Character segmentation in OCR
- Medical image analysis

---

# Important Exam Points

- Works on binary images.
- Uses connectivity rule.
- Two-pass algorithm.
- Assigns unique labels to connected regions.
- Used after thresholding.

---

# Next: [[Boundary based approaches]]