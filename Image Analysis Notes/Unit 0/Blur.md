
> **Blur (Smoothing): Average Blur, Median Blur, and Gaussian Blur in Image Analysis using OpenCV**


---

# Definition

**Blurring** is an image processing operation used to:  
- reduce noise  
 - reduce fine details  
- smooth intensity variations

It works by **replacing each pixel value with a value computed from its neighbors** using a kernel (window).

Mathematically:  
  
$$g(x,y) = \sum_{i,j} f(x+i, y+j)\cdot h(i,j)$$  
 
where  
• (f(x,y)) = input image  
• (h(i,j)) = smoothing kernel  
• (g(x,y)) = output image

---

# Need

- Remove salt-and-pepper noise  
- Remove Gaussian noise  
- Preprocessing before edge detection  
- Reduce high-frequency components  
- Improve segmentation results

---

# Types of Blurring

We study 3 main types:

1. **Average (Mean) Blur**
2. **Median Blur**
3. **Gaussian Blur**

---

# 1. Average Blur (Mean Filter)

## Definition

Average blur replaces the center pixel with the **average of neighboring pixels**.

Kernel example (3×3):  
$$\frac{1}{9}  
\begin{bmatrix}  
1 & 1 & 1\\  
1 & 1 & 1\\  
1 & 1 & 1  
\end{bmatrix}  $$


## Working

For each pixel:

1. Take surrounding pixels
2. Add them
3. Divide by total number
4. Assign result to center pixel

## Effect

• Smooths image  
• Blurs edges  
• Reduces random noise

---

## OpenCV Code (Average Blur)

```python
import cv2

img = cv2.imread("image.jpg")
blur = cv2.blur(img, (5,5))   # 5x5 kernel

cv2.imshow("Original", img)
cv2.imshow("Average Blur", blur)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

---

## Limitations

• Blurs edges  
• Not good for salt-and-pepper noise  
• Produces unrealistic smoothing

---

# 2. Median Blur

## Definition

Median blur replaces the pixel value with the **median of neighboring pixels**, not the mean.

Example window:

```text
[10, 200, 30]
[40, 255, 50]
[60, 70, 80]
```

Sorted:

```text
10,30,40,50,60,70,80,200,255
```

Median = **60**

## Working

1. Extract neighborhood
2. Sort pixel values
3. Pick middle value
4. Replace center pixel

## Effect

• Removes impulse noise  
• Preserves edges better than average blur

---

## OpenCV Code (Median Blur)

```python
median = cv2.medianBlur(img, 5)

cv2.imshow("Median Blur", median)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

Kernel size must be **odd** (3,5,7…).

---

## Limitations

• Slow for large kernels  
• Not good for Gaussian noise  
• Removes thin lines

---

# 3. Gaussian Blur

## Definition

Gaussian blur uses a **Gaussian distribution kernel**:

$$G(x,y) = \frac{1}{2\pi\sigma^2} e^{-\frac{x^2+y^2}{2\sigma^2}}  $$


Kernel example (3×3):  
[  
$$\frac{1}{16}  
\begin{bmatrix}  
1 & 2 & 1\\  
2 & 4 & 2\\  
1 & 2 & 1  
\end{bmatrix} $$ 
]

## Working

• Center pixels get higher weight  
• Distant pixels get lower weight  
• Produces natural blur

## Effect

• Reduces Gaussian noise  
• Smooths image gradually  
• Preserves edges better than average blur

---

## OpenCV Code (Gaussian Blur)

```python
gaussian = cv2.GaussianBlur(img, (5,5), 0)

cv2.imshow("Gaussian Blur", gaussian)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

Here:  
• (5,5) = kernel size  
• 0 = auto sigma calculation

---

# Comparison Table

|Feature|Average Blur|Median Blur|Gaussian Blur|
|---|---|---|---|
|Method|Mean|Median|Weighted mean|
|Best for|Uniform noise|Salt & pepper noise|Gaussian noise|
|Edge preservation|Poor|Good|Medium|
|Speed|Fast|Slow|Medium|
|Nature|Artificial|Nonlinear|Natural|

---

# Combined Code

```python
import cv2

img = cv2.imread("image.jpg")

avg = cv2.blur(img, (5,5))
median = cv2.medianBlur(img, 5)
gaussian = cv2.GaussianBlur(img, (5,5), 0)

cv2.imshow("Original", img)
cv2.imshow("Average Blur", avg)
cv2.imshow("Median Blur", median)
cv2.imshow("Gaussian Blur", gaussian)

cv2.waitKey(0)
cv2.destroyAllWindows()
```

---

# Applications

• Noise removal  
• Face detection preprocessing  
• Medical image smoothing  
• Background smoothing  
• Edge detection preprocessing  
• Video noise filtering

---

# Limitations (General)

- Loss of details  
- Blurred edges  
- Choice of kernel size is critical  
- Over-blurring destroys features

---

# Summary

- Blur = smoothing operation  
- Average blur = simple mean  
- Median blur = nonlinear, best for impulse noise  
- Gaussian blur = weighted, natural smoothing  
- All use kernels  
- Used mainly for preprocessing

---
