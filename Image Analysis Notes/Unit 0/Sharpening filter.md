
##  Definition

A **sharpening filter** is used to **enhance edges and fine details in an image** by emphasizing high-frequency components (rapid intensity changes in intensity values).

In simple terms:

> **Sharpening makes blurred edges clearer and increases image detail.**

---

# Why Sharpening is Required
Images may appear blurred due to:

- Motion blur
- Defocus of camera
- Noise or smoothing operations
- Sensor limitations
   
Sharpening helps to:

 Highlight edges  
 Improve object boundaries  
 Increase visual clarity

---

# Basic Principle

Edges correspond to **high-frequency components** in an image.

Sharpening works by **adding edge information to the original image**.

$g(x,y) = f(x,y) + k \cdot \text{Edge}(x,y)$  

Where

- (f(x,y)) → original image
- (g(x,y)) → sharpened image
- (k) → scaling constant

---

# Sharpening Using Convolution Kernel

A common sharpening kernel:

$$\begin{bmatrix}  
0 & -1 & 0 \\ 
-1 & 5 & -1 \\  
0 & -1 & 0  
\end{bmatrix}$$  

Explanation:

- Center pixel is increased
- Neighbor pixels are subtracted
- This highlights edges.

---

# Strong Sharpening Kernel

Another kernel:
  
$$\begin{bmatrix}  
-1 & -1 & -1 \\  
-1 & 9 & -1 \\  
-1 & -1 & -1  
\end{bmatrix}$$

This produces **stronger edge enhancement**.

---

# Sharpening by “Doubling the Center and Subtracting Averaging Filter”

### Step 1: Averaging Filter

A smoothing filter is

$$\frac{1}{9}  
\begin{bmatrix}  
1 & 1 & 1 \\  
1 & 1 & 1 \\ 
1 & 1 & 1  
\end{bmatrix}$$

This produces a **blurred image**.

---

### Step 2: Sharpening Formula

Sharpening can be obtained as:

$$\text{Sharpened Image} = 2 \times \text{Original Image} - \text{Blurred Image} $$

Meaning:

- Double the center pixel
  - Subtract the average of surrounding pixels
---

#  Derivation of Sharpening Kernel

Original image kernel:
$$
\begin{bmatrix}  
0 & 0 & 0 \\ 
0 & 2 & 0 \\  
0 & 0 & 0  
\end{bmatrix}  
$$
Averaging filter:

$$\frac{1}{9}  
\begin{bmatrix}  
1 & 1 & 1 \\ 
1 & 1 & 1 \\  
1 & 1 & 1  
\end{bmatrix}$$  
Subtracting them:
 
$$\begin{bmatrix}  
-\frac{1}{9} & -\frac{1}{9} & -\frac{1}{9} \\  
-\frac{1}{9} & \frac{17}{9} & -\frac{1}{9} \\ 
-\frac{1}{9} & -\frac{1}{9} & -\frac{1}{9}  
\end{bmatrix}$$  


This matrix acts as a **sharpening kernel**.

---

# Code (Sharpening Kernel)

```python
import cv2
import numpy as np

img = cv2.imread("image.jpg")

kernel = np.array([
[-1/9, -1/9, -1/9],
[-1/9, 17/9, -1/9],
[-1/9, -1/9, -1/9]
])

sharpened = cv2.filter2D(img, -1, kernel)

cv2.imshow("Original", img)
cv2.imshow("Sharpened", sharpened)

cv2.waitKey(0)
cv2.destroyAllWindows()
```

---

# Alternative Implementation (Using Averaging)

Instead of manually creating the kernel:

```python
import cv2

img = cv2.imread("image.jpg")

blur = cv2.blur(img,(3,3))

sharpened = cv2.addWeighted(img,2,blur,-1,0)

cv2.imshow("Original",img)
cv2.imshow("Sharpened",sharpened)

cv2.waitKey(0)
cv2.destroyAllWindows()
```

This directly implements:
 
$$2 \times Original - Blurred$$  


---

# Applications of Sharpening

- Medical imaging
- Satellite image analysis
- Document enhancement
- Object detection preprocessing
- Computer vision pipelines

---

# Summary

A **sharpening filter enhances edges and fine details** by emphasizing high-frequency components in an image. It can be obtained by **doubling the center pixel and subtracting the average of neighboring pixels using a (1/9) averaging mask**, which enhances edges while maintaining image brightness.

---