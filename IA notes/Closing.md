2026-02-17  19:00
Status: 
Tags:  [[Image Analysis]]
# Definition
**Closing** is a morphological operation defined as:
>**Dilation followed by Erosion using the same structuring element.**

# Main Concept
### Closing:

- **Fills small holes inside objects**
- **Closes small gaps and cracks**
- **Connects nearby components**
- **Smooths object boundaries**
- **Preserves overall object size*

Think of it as:

> First you **expand** the object (dilation),  
> then you **shrink it back** (erosion),  
> but the **holes and gaps get sealed**.

---
# Mathematical Formula
Mathematically:  
$A \bullet B = (A \oplus B) \ominus B$  

Where:
- `A` = input image
- `B` = structuring element
- `⊕` = dilation
- `⊖` = erosion
## PIXEL-LEVEL LOGIC

For a pixel (x, y):

### Dilation:
$D(x,y) = \max{I(x+i, y+j)}$  
### Erosion:
$C(x,y) = \min{D(x+i, y+j)}$  

So Closing = **max filter then min filter**

# Working
Assume binary image + 3×3 kernel.
### Step 1: Dilation
- Kernel slides over image
- Pixel becomes white if **any kernel overlaps white**
- Gaps and holes get filled
### Step 2: Erosion
- Kernel slides again
- Pixel remains white only if **entire kernel fits inside white**
- Shape is restored but holes stay closed
# Code
```python
import cv2
import numpy as np

# Read image
img = cv2.imread("image.png", cv2.IMREAD_GRAYSCALE)

# Convert to binary
_, binary = cv2.threshold(img, 127, 255, cv2.THRESH_BINARY)

# Structuring element
kernel = np.ones((5,5), np.uint8)

# Closing (dilation + erosion)
closing = cv2.morphologyEx(binary, cv2.MORPH_CLOSE, kernel)

# Display results
cv2.imshow("Original", binary)
cv2.imshow("Closing", closing)

cv2.waitKey(0)
cv2.destroyAllWindows()
```
## Manual Process
```python
#This is exactly what `cv2.MORPH_CLOSE` does.
dilated = cv2.dilate(binary, kernel, iterations=1)
closed = cv2.erode(dilated, kernel, iterations=1)
```

# Merits | Demerits | Constraints | Examples
## APPLICATIONS

### Hole Filling
- Filling small black holes inside objects
### Gap Closing
- Closing small cracks in text
- Repairing broken edges
### Noise Reduction
- Removing pepper noise (black dots)
### Object Connection
- Connecting nearby components
### Preprocessing
- Before contour detection
- Before region labeling
- Before shape analysis    
---

## REAL EXAMPLES

1. Document image:
	- Letters broken → joined
	- Small gaps in strokes → removed
2. Medical image:
	- Dark cavities inside bright regions → filled
3. Satellite image:
	- Roads broken → reconnected
---

## LIMITATIONS

- May merge nearby objects unintentionally  
- Can fill important holes (loses shape info)  
- Thickens thin structures  
- Depends heavily on kernel size

# Summary
| Feature       | Closing                   |
| ------------- | ------------------------- |
| Order         | Dilation → Erosion        |
| Purpose       | Fill holes & gaps         |
| Noise removed | Black noise               |
| Shape         | Smoothed & connected      |
| Kernel role   | Controls what gets filled |
- Object with black holes becomes solid object
- Broken lines become continuous
- Rough boundaries become smooth

| Feature | Opening            | Closing            |
| ------- | ------------------ | ------------------ |
| Order   | Erosion → Dilation | Dilation → Erosion |
| Removes | Small white noise  | Small black noise  |
| Fills   | Nothing            | Holes              |
| Breaks  | Thin connections   | Joins connections  |


Imagine filling cracks in a wall:

- Dilation = pouring plaster
- Erosion = scraping excess
- Closing = wall becomes smooth and solid










# Next: [[Hit-or-Miss]]