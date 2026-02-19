 2026-02-17  18:24
Status: 
Tags: [[Image Analysis]]
# Definition

==**Dilation**== is a morphological operation that **adds pixels to object boundaries**, making objects **thicker, larger, and brighter** (in binary images).
- It expands foreground regions.
---
==**Erosion**== is a morphological operation that **removes pixels from object boundaries**, making objects **thinner and smaller**.
-  It shrinks foreground regions.


# Main Concept

Think of an image as made of:

- **Foreground (object)** = white (1 or 255)
- **Background** = black (0)

And a **structuring element (kernel)** as a small mask (like a window).

|Operation|Effect|
|---|---|
|Dilation|Grows objects|
|Erosion|Shrinks objects|

Example:

- Dilation = **painting with a thick brush**
- Erosion = **scraping edges** or removing a layer of paint

# Working

Assume binary image and 3×3 kernel:
### Kernel:

```
1 1 1
1 1 1
1 1 1
```

### For each pixel:

#### Dilation:

- Place kernel center at pixel
- If **any kernel position overlaps white pixel**
- Output pixel = white

#### Erosion:

- Place kernel center at pixel
- If **all kernel positions overlap white pixels**
- Output pixel = white
- Else black
# Mathematical Formula

Let:

- Image = `A`
- Structuring element = `B`

### Dilation
$$
A \oplus B = \{z \mid (B)_z \cap A \neq \emptyset\} 
$$
Meaning:  
If **any pixel under kernel is 1 → output pixel = 1**

---

### Erosion
$$

A \ominus B = \{z \mid (B)_z \subseteq A\}   
$$

Meaning:  
If **all pixels under kernel are 1 → output pixel = 1**
# Code

```python
import cv2
import numpy as np
# Load image
img = cv2.imread("image.png", cv2.IMREAD_GRAYSCALE)
# Convert to binary
_, binary = cv2.threshold(img, 127, 255, cv2.THRESH_BINARY)
# Structuring element (kernel)
kernel = np.ones((5,5), np.uint8)
# Dilation
dilation = cv2.dilate(binary, kernel, iterations=1)
# Erosion
erosion = cv2.erode(binary, kernel, iterations=1)
# Show results
cv2.imshow("Original", binary)
cv2.imshow("Dilation", dilation)
cv2.imshow("Erosion", erosion)
cv2.waitKey(0)
cv2.destroyAllWindows()
```
# Merits | Demerits | Constraints

## APPLICATIONS

### Dilation used in:

- Filling holes in objects
- Connecting broken characters (OCR)
- Thickening edges
- Closing gaps in lines
- Object detection preprocessing

### Erosion used in:

- Removing salt noise
- Separating touching objects
- Boundary extraction
- Thinning shapes
- Removing small blobs
---

## LIMITATIONS

### Dilation:

- Merges nearby objects
- Increases noise
- Distorts shape

### Erosion:

- Can remove useful small objects
- May break thin structures
- Shrinks important features




# Summary

| Feature    | Dilation    | Erosion       |
| ---------- | ----------- | ------------- |
| Effect     | Expand      | Shrink        |
| Noise      | Fills holes | Removes noise |
| Pixel rule | ANY = 1     | ALL = 1       |
| Shape      | Grows       | Reduces       |













# Next: [[Opening]]