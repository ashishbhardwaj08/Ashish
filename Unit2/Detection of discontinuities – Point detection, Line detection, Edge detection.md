# WHAT IS A DISCONTINUITY?

In image processing, a **discontinuity** means:

> A sudden change in intensity (brightness).

Mathematically:  
If intensity changes rapidly in a small neighborhood → it is a discontinuity.
Discontinuities help detect:

- Points
- Lines
- Edges
- Object boundaries
# TYPES OF DISCONTINUITIES

1. **Point Detection** → isolated pixel
2. **Line Detection** → thin structures
3. **Edge Detection** → object boundaries

---
---
---

# 1. POINT DETECTION

## Definition

Point detection identifies:

> Isolated pixels whose intensity is significantly different from neighbors.

Example:

```
0  0  0
0 255 0
0  0  0
```

Center is a point discontinuity.

---

## Mathematical Idea

We use a mask:

 
$$\begin{bmatrix}
-1 & -1 & -1 \\
-1 & 8 & -1 \\
-1 & -1 & -1 
\end{bmatrix}$$ 


This computes:

$R = 8f(x,y) - \sum neighbors$  

If |R| > threshold → point detected.

---

## Python Code

```python
import cv2
import numpy as np

img = cv2.imread("image.png", 0)

# Point detection mask
kernel = np.array([[-1,-1,-1],
                   [-1, 8,-1],
                   [-1,-1,-1]])

response = cv2.filter2D(img, -1, kernel)

# Threshold
_, points = cv2.threshold(response, 150, 255, cv2.THRESH_BINARY)

cv2.imshow("Points", points)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

---

## Applications

- Detect stars in astronomy
- Detect salt noise
- Defect detection
---
---
# 2. LINE DETECTION

---

## Definition

Line detection identifies:

> Thin lines in specific orientations.

---

## Line Detection Masks

### Horizontal Line

  
$$\begin{bmatrix}  
-1 & -1 & -1 \\  
2 & 2 & 2 \\  
-1 & -1 & -1  
\end{bmatrix}$$  


### Vertical Line

$$
\begin{bmatrix}  
-1 & 2 & -1 \\  
-1 & 2 & -1 \\  
-1 & 2 & -1  
\end{bmatrix}  
$$

### 45° Diagonal

  
$$\begin{bmatrix} 
-1 & -1 & 2 \\
-1 & 2 & -1 \\
2 & -1 & -1  
\end{bmatrix}$$


---

## Python Code

```python
import cv2
import numpy as np

img = cv2.imread("image.png", 0)

# Horizontal line mask
kernel = np.array([[-1,-1,-1],
                   [ 2, 2, 2],
                   [-1,-1,-1]])

response = cv2.filter2D(img, -1, kernel)

_, lines = cv2.threshold(response, 100, 255, cv2.THRESH_BINARY)

cv2.imshow("Lines", lines)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

---

## Applications

- Road detection in satellite images
- Crack detection
- Text line detection
- Fingerprint ridge detection
---
---
---

# 3. EDGE DETECTION

## Definition

Edge detection identifies:

> Boundaries between regions with different intensities.

Edge = large gradient.
##  Gradient Concept
 
$\nabla f = \left[ \frac{\partial f}{\partial x}, \frac{\partial f}{\partial y} \right]$  

Edge magnitude:

$|\nabla f| = \sqrt{G_x^2 + G_y^2}$  

---

## Sobel Operators

### Gx


$$\begin{bmatrix}  
-1 & 0 & 1 \\  
-2 & 0 & 2 \\  
-1 & 0 & 1  
\end{bmatrix}  $$

### Gy

$$  
\begin{bmatrix}  
-1 & -2 & -1 \\  
0 & 0 & 0 \\  
1 & 2 & 1  
\end{bmatrix}  $$

---

## Sobel Code

```python
import cv2
import numpy as np

img = cv2.imread("image.png", 0)

sobelx = cv2.Sobel(img, cv2.CV_64F, 1, 0, ksize=3)
sobely = cv2.Sobel(img, cv2.CV_64F, 0, 1, ksize=3)

magnitude = cv2.magnitude(sobelx, sobely)

cv2.imshow("Edges", magnitude.astype(np.uint8))
cv2.waitKey(0)
cv2.destroyAllWindows()
```

---

## Canny Edge Detection (Advanced)

```python
edges = cv2.Canny(img, 100, 200)
cv2.imshow("Canny", edges)
```

Canny includes:

1. Gaussian smoothing
2. Gradient calculation
3. Non-maximum suppression
4. Hysteresis thresholding

---

#  Comparison Table

|Type|Detects|Tool Used|Complexity|
|---|---|---|---|
|Point|Isolated pixel|Laplacian mask|Low|
|Line|Thin structures|Directional masks|Medium|
|Edge|Object boundary|Gradient operators|High|

---

#  Limitations

### Point Detection

- Sensitive to noise

### Line Detection
-  Only specific orientations

### Edge Detection

-  Detects too many edges  
-  Sensitive to threshold  
- Noise sensitive

---

# Relationship

| Operation       | Based On                    |
| --------------- | --------------------------- |
| Point detection | Second derivative           |
| Line detection  | Directional filtering       |
| Edge detection  | First derivative (gradient) |

---

# Summary

|Detection Type|Intensity Change Type|
|---|---|
|Point|Sudden change at one pixel|
|Line|Continuous change in one direction|
|Edge|Strong gradient boundary|

---

We have now covered:

- Morphological operations  
- Region filling  
- Connected components  
- Discontinuity detection

---

## Next: [[Gradient Operators]]