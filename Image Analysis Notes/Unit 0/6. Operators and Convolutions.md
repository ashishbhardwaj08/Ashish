
# Operators (in Image Processing)

### Definition:

An **operator** is a mathematical function applied to an image (or its pixels) to produce a new image.
It transforms the input image into an output image.

---

### Simple Meaning:

> An operator takes an image as input and modifies it.
---

### Types of Operators

### 1. Point Operator

Operates on **one pixel at a time**.

Example:
- Negative image
- Thresholding
- Brightness change

Mathematically: 
$$g(x,y) = T(f(x,y))  $$

Each output pixel depends only on the corresponding input pixel.

---

### 2. Neighborhood Operator

Uses a **group of nearby pixels** (kernel/mask).

Example:
- Smoothing
- Sharpening
- Edge detection
Here output pixel depends on surrounding pixels.

---
### Example:
Blur filter  
Sobel operator  
Laplacian operator

---

# Convolution

### Definition:

**Convolution is a mathematical operation where a small matrix (kernel) is moved across the image to compute weighted sums of neighboring pixels.**

It is the most common neighborhood operation.

---

###  Mathematical Form:

For discrete image:
$$g(x,y) = \sum_{i}\sum_{j} f(x-i, y-j) \cdot h(i,j)  $$

Where:
- ( f(x,y) ) → input image
- ( h(i,j) ) → kernel (mask)
- ( g(x,y) ) → output image
---

### How It Works (Step-by-Step)

1. Take a kernel (example 3×3 matrix)
2. Place it over image pixels
3. Multiply corresponding values
4. Add them
5. Replace center pixel with result
6. Slide kernel and repeat
---
### Example: 3×3 Averaging Filter

$$Kernel:  
\frac{1}{9}  
\begin{bmatrix}  
1 & 1 & 1 \\  
1 & 1 & 1 \\  
1 & 1 & 1  
\end{bmatrix}$$ 
Used for **image smoothing (blurring)**.

---
### Why Convolution is Important?
It is used for:
- Blurring
- Sharpening
- Edge detection (Sobel, Prewitt)
- Feature extraction
- CNNs (Deep Learning)
---
# Difference Between Operator and Convolution

|Operator|Convolution|
|---|---|
|General term|Specific type of operator|
|Can be point or neighborhood|Always neighborhood|
|Includes thresholding|Used for filtering|

---

# Short Definition

**Operator:**  
A mathematical transformation applied to an image to produce another image.

**Convolution:**  
A neighborhood operation where an image is filtered using a kernel to produce a new image through weighted summation.
