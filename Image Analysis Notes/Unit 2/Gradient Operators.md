Tags:  [[_Unit -2]]

# Gradient Operators (Edge Detection – First Derivative)
## What is a Gradient Operator?

In image segmentation, a **gradient operator** detects edges by measuring:

> How rapidly pixel intensity changes in x and y directions.

Mathematically:
 
$$\nabla f =  
\begin{bmatrix}  
G_x \\  
G_y  
\end{bmatrix}$$

Where:

- $(G_x = \frac{\partial f}{\partial x})$
- $(G_y = \frac{\partial f}{\partial y})$

Edge strength (magnitude):
 
$|\nabla f| = \sqrt{G_x^2 + G_y^2}$

In practice:
  
$|\nabla f| \approx |G_x| + |G_y|$ 

If gradient is large → strong edge.

## How Gradient Detects Edges?

Consider intensity change:

|Region A|Region B|
|---|---|
|50|200|

At boundary:

```
50 50 50 200 200 200
```

Difference is high → gradient large → edge detected.

---
## Types of Gradient Operators

Your syllabus includes:

- Roberts
- Prewitt
- Sobel (most important in exams).

## 1. Roberts Operator (2×2)

### Masks:
 
$$G_x =  
\begin{bmatrix}  
1 & 0 \\  
0 & -1  
\end{bmatrix}  
\quad  
G_y =  
\begin{bmatrix}  
0 & 1 \\  
-1 & 0  
\end{bmatrix} $$ 
### Properties:

- Very small kernel
- Detects diagonal edges
- Highly noise sensitive
## 2. Prewitt Operator (3×3)

### Gx:

 
$$\begin{bmatrix}  
-1 & 0 & 1 \\  
-1 & 0 & 1 \\  
-1 & 0 & 1  
\end{bmatrix} $$ 


### Gy:

 
$$\begin{bmatrix}  
1 & 1 & 1 \\  
0 & 0 & 0 \\  
-1 & -1 & -1  
\end{bmatrix}$$  

### Properties:

- Detects vertical & horizontal edges
- Moderate noise sensitivity
---

## 3. Sobel Operator (Most Important)

### Gx:

 
$$\begin{bmatrix}  
-1 & 0 & 1 \\  
-2 & 0 & 2 \\  
-1 & 0 & 1  
\end{bmatrix}$$ 
### Gy:
  
$$\begin{bmatrix}  
1 & 2 & 1 \\  
0 & 0 & 0 \\  
-1 & -2 & -1  
\end{bmatrix}$$ 


### Why Sobel is better?

- Middle row/column has weight 2  
- Performs slight smoothing  
- Less sensitive to noise  
- Strong edge response
---

## Complete Python Code (All Gradient Operators)

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

# Read image
img = cv2.imread('image.jpg', 0)

# -------- ROBERTS --------
roberts_x = np.array([[1, 0],
                      [0, -1]], dtype=np.float32)

roberts_y = np.array([[0, 1],
                      [-1, 0]], dtype=np.float32)

rx = cv2.filter2D(img, -1, roberts_x)
ry = cv2.filter2D(img, -1, roberts_y)
roberts = cv2.magnitude(rx.astype(np.float32), ry.astype(np.float32))


# -------- PREWITT --------
prewitt_x = np.array([[-1,0,1],
                      [-1,0,1],
                      [-1,0,1]], dtype=np.float32)

prewitt_y = np.array([[1,1,1],
                      [0,0,0],
                      [-1,-1,-1]], dtype=np.float32)

px = cv2.filter2D(img, -1, prewitt_x)
py = cv2.filter2D(img, -1, prewitt_y)
prewitt = cv2.magnitude(px.astype(np.float32), py.astype(np.float32))


# -------- SOBEL --------
sobelx = cv2.Sobel(img, cv2.CV_64F, 1, 0, ksize=3)
sobely = cv2.Sobel(img, cv2.CV_64F, 0, 1, ksize=3)
sobel = cv2.magnitude(sobelx, sobely)

# Convert to uint8
sobel = np.uint8(np.absolute(sobel))

# Display
plt.imshow(sobel, cmap='gray')
plt.title("Sobel Edge Detection")
plt.show()
```
---
## Direction of Edge

Angle of edge:

$\theta = \tan^{-1}(G_y / G_x)$ 
This gives orientation of edge.

---
## Performance Comparison

|Operator|Noise Sensitivity|Accuracy|Speed|
|---|---|---|---|
|Roberts|Very High|Low|Very Fast|
|Prewitt|Medium|Medium|Fast|
|Sobel|Low|High|Moderate|

Sobel is preferred in practice.

---
## Important Points

- Gradient is first derivative.
- Large gradient → edge.
- Sobel adds smoothing effect.
- Gradient gives both magnitude & direction.
- Works best when image is pre-smoothed.


# Next: [[Compass Operators]]