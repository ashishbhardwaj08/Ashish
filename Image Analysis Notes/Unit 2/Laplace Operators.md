Tags:  [[_Unit -2]]

> Second Derivative Edge Detection
# Why Second Derivative?

`Gradient (first derivative):
 
$\nabla f = \frac{\partial f}{\partial x}, \frac{\partial f}{\partial y}$  

Detects where intensity changes rapidly.

---
`Second derivative detects:

> Where the rate of change itself changes.

In simple terms:
- First derivative → finds slope
- Second derivative → finds peak of slope
- 
Edges occur where intensity changes sharply → second derivative highlights this strongly.
---
---

# Mathematical Definition

The Laplacian operator:

 
$$\nabla^2 f =  
\frac{\partial^2 f}{\partial x^2} +  
\frac{\partial^2 f}{\partial y^2}  
$$

It is:

- Isotropic (same in all directions)
- Rotation invariant
- No direction bias
---
---

# Discrete Laplacian Masks

Because digital images are discrete, we approximate derivatives.
## 4-neighbour Laplacian

 
$$\begin{bmatrix}  
0 & -1 & 0 \\  
-1 & 4 & -1 \\  
0 & -1 & 0  
\end{bmatrix}  $$

## 8-neighbour Laplacian
 
$$\begin{bmatrix}  
-1 & -1 & -1 \\  
-1 & 8 & -1 \\  
-1 & -1 & -1  
\end{bmatrix}$$
---
---

# How Laplacian Detects Edges

If region is uniform:
	All neighboring pixels similar → output ≈ 0

At edge:
	Center pixel very different → large positive or negative value

So: 
$$R(x,y) = \text{large magnitude} \Rightarrow \text{edge} $$ 

---

# -> Important Property

Unlike gradient:

- Laplacian gives **double edge effect**
- Produces positive and negative values
- Very sensitive to noise

Therefore:
Usually apply Gaussian smoothing before Laplacian
That is called:

 **==Laplacian of Gaussian (LoG)==**

# Python Code – Laplacian Operator

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

# Read grayscale image
img = cv2.imread("image.jpg", 0)

# -------- Using OpenCV Built-in Laplacian --------
laplacian = cv2.Laplacian(img, cv2.CV_64F)

# Convert to uint8
laplacian_abs = np.uint8(np.absolute(laplacian))


# -------- Using Manual 4-neighbour Kernel --------
kernel_4 = np.array([[0,-1,0],
                     [-1,4,-1],
                     [0,-1,0]])

lap_4 = cv2.filter2D(img, cv2.CV_64F, kernel_4)
lap_4 = np.uint8(np.absolute(lap_4))


# -------- Using Manual 8-neighbour Kernel --------
kernel_8 = np.array([[-1,-1,-1],
                     [-1,8,-1],
                     [-1,-1,-1]])

lap_8 = cv2.filter2D(img, cv2.CV_64F, kernel_8)
lap_8 = np.uint8(np.absolute(lap_8))


# -------- Display --------
plt.figure(figsize=(12,5))

plt.subplot(1,4,1)
plt.imshow(img, cmap='gray')
plt.title("Original")
plt.axis("off")

plt.subplot(1,4,2)
plt.imshow(laplacian_abs, cmap='gray')
plt.title("OpenCV Laplacian")
plt.axis("off")

plt.subplot(1,4,3)
plt.imshow(lap_4, cmap='gray')
plt.title("4-Neighbour")
plt.axis("off")

plt.subplot(1,4,4)
plt.imshow(lap_8, cmap='gray')
plt.title("8-Neighbour")
plt.axis("off")

plt.tight_layout()
plt.show()
```

> [!NOTE] OUTPUT
>- Produces thin edges
>- More noise compared to Sobel
>- Detects edges in all directions
>- Often gives double edges

# Summary

| Property            | Laplacian |
| ------------------- | --------- |
| Directional?        | No        |
| Rotation invariant? | Yes       |
| Noise sensitivity   | Very High |
| Edge thickness      | Thin      |
| Computational cost  | Low       |

- Laplacian is second derivative.
- It is isotropic.
- Produces double edges.
- Very noise sensitive.
- Often combined with Gaussian smoothing.
- Used in zero-crossing method (next topic).

# Next: [[Zero crossing]]
