# What Does “Performance” Mean?

An ideal edge detector should:

1. Detect all real edges
2. Not detect noise
3. Localize edge accurately
4. Produce single thin edge
5. Be computationally efficient

---

# Three Main Performance Criteria (Very Important)

According to classical edge detection theory (Canny criteria):

---

## 1. Good Detection

> High probability of detecting real edges  
> Low probability of detecting false edges

Mathematically:
Maximize Signal-to-Noise Ratio (SNR)
If noise is high → performance decreases.

---

## 2 Good Localization

Edge should be detected:

- Exactly at true boundary  
- Not shifted left/right

Error in localization should be minimum.
Gradient operators usually localize well.

---

## Single Response

An ideal detector should:
- Give one response per edge  
 - Not double edges

`Laplacian often produces double edges.

---

# Performance Comparison of Major Operators

|Operator|Noise Resistance|Localization|Thin Edge|Computation|
|---|---|---|---|---|
|Roberts|Very Poor|Poor|Thin|Very Fast|
|Prewitt|Moderate|Moderate|Moderate|Fast|
|Sobel|Good|Good|Moderate|Fast|
|Laplacian|Very Poor|Good|Thin|Fast|
|Kirsch|Poor|Good|Thick|Slow|
|Canny|Excellent|Excellent|Very Thin|Moderate|

---

# Noise Sensitivity

**Why Laplacian is very noise sensitive?**

Because:

Second derivative amplifies high-frequency components.

Noise = high-frequency  
Therefore Laplacian amplifies noise strongly.

---

# Edge Thickness

- Gradient → thicker edges
- Laplacian → thin edges
- Canny → thinnest (due to non-maximum suppression)

---

# Computational Complexity

|Operator|Number of Convolutions|
|---|---|
|Sobel|2|
|Laplacian|1|
|Kirsch|8|
|Canny|Multiple stages|

More masks = more computation.

---

# Quantitative Evaluation Metrics (Advanced)

In research, we measure:

### 1. Precision

$$Precision = \frac{TP}{TP + FP}$$  
### Recall

$$Recall = \frac{TP}{TP + FN}$$  
### F1 Score
 
$$F1 = \frac{2PR}{P+R}$$  

Where:

- TP = True edges detected
- FP = False edges
- FN = Missed edges
# Compare Sobel vs Canny

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

img = cv2.imread("image.jpg", 0)

# Sobel
sobelx = cv2.Sobel(img, cv2.CV_64F, 1, 0)
sobely = cv2.Sobel(img, cv2.CV_64F, 0, 1)
sobel = cv2.magnitude(sobelx, sobely)
sobel = np.uint8(np.clip(sobel, 0, 255))

# Canny
canny = cv2.Canny(img, 100, 200)

plt.figure(figsize=(12,4))

plt.subplot(1,3,1)
plt.imshow(img, cmap='gray')
plt.title("Original")
plt.axis("off")

plt.subplot(1,3,2)
plt.imshow(sobel, cmap='gray')
plt.title("Sobel")
plt.axis("off")

plt.subplot(1,3,3)
plt.imshow(canny, cmap='gray')
plt.title("Canny")
plt.axis("off")

plt.show()
```

We will observe:

- Sobel → thicker, more noisy edges
- Canny → clean, thin, accurate edges

---

# Theoretical Conclusion

- If speed matters → Sobel  
- If direction matters → Kirsch  
- If thin edges needed → Laplacian  
- If best overall → Canny

---

# Important Exam Statements

- Ideal edge detector maximizes detection & localization.
- Laplacian produces double edges.
- Second derivative amplifies noise.
- Canny satisfies optimality criteria.
- Performance depends on noise level.


# Next: [[Amplitude thresholding or Window slicing]]