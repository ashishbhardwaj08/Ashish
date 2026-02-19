2026-02-19  13:22
Status: 
Tags: 
# Definition
Boundary extraction means:

> **Extract only the border (outline) of an object** in a binary image.

Instead of the whole filled object, we get just its **edges**.
# Purpose
We use **erosion** to shrink the object and then subtract it from the original image.

# Main Concept

# Mathematical Formula

Boundary(A) = A - (A ⊖ B)  
Where:
- (A) = binary image
- (B) = structuring element (kernel)
- ⊖ = erosion
- − = subtraction
# Working
1. Convert image to binary
2. Apply erosion which will shrink objects
3. Subtract eroded image from original image
4. Result will an image with only edge pixels

Original object:
```
████████
████████
████████
████████
```

After erosion:
```
  ██████
  ██████
```

Subtract:
```
████████
█      █
█      █
████████
```

Only boundary remains.
# Code
```python
import cv2
import numpy as np

img = cv2.imread("binary.png", 0)
_, binary = cv2.threshold(img, 127, 255, cv2.THRESH_BINARY)

#Use larger kernel for thicker boundary
kernel = np.ones((3,3), np.uint8)

#Use more iterations to erode more and get thicker boundary
eroded = cv2.erode(binary, kernel, iterations=1)

boundary = cv2.subtract(binary, eroded)

cv2.imshow("Original", binary)
cv2.imshow("Boundary", boundary)
cv2.waitKey(0)
```

# TYPES OF MORPHOLOGICAL BOUNDARIES
#### Internal Boundary
	$A - (A \ominus B)$ (Subtract eroded from original)

Gives boundary inside object.

---

#### External Boundary

	$(A \oplus B) - A$  ( Dilation then subtract original )
Gives boundary outside object.

---

#### Morphological Gradient

	$(A \oplus B) - (A \ominus B))$  (Subtract eroded from dilated)

Gives thick boundary (both sides).
# Merits | Demerits | Constraints
#### Applications

- Shape analysis  
- Object perimeter detection  
- OCR preprocessing  
- Medical image outlines
#### LIMITATIONS

- Works best on binary images  
- Sensitive to noise  
- Boundary thickness depends on kernel  
- Not sub-pixel accurate


# Summary

| Feature    | Boundary Extraction                  |
| ---------- | ------------------------------------ |
| Formula    | A − (A ⊖ B)                          |
| Uses       | Extract outlines                     |
| Works on   | Binary images                        |
| Thickness  | Depends on kernel & No.of iterations |
| Complexity | Low                                  |










# Next: [[]]