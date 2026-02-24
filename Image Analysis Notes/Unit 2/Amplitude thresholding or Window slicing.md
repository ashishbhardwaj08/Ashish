Tags:  [[_Unit -2]]

 # **Intensity-based segmentation**
 # What is Amplitude Thresholding?

Amplitude = Intensity value of pixel.

Thresholding means:

> Separate image into regions based on intensity value.

## Basic Idea

$$g(x,y) =  
\begin{cases}  
1 & \text{if } f(x,y) \ge T \\  
0 & \text{if } f(x,y) < T  
\end{cases}$$  

Where:

- ( f(x,y) ) = original pixel
- ( T ) = threshold
- ( g(x,y) ) = binary output
---
# Why Thresholding Works?

If object is brighter than background:

Example:

- Background intensity ≈ 50
- Object intensity ≈ 200

Choose: $$T = 120 $$ 
Then:

Object → white  
Background → black

This is segmentation.

---
# Types of Thresholding

### 1. Global Thresholding

Single threshold for entire image.
### 2. Local (Adaptive) Thresholding

Different threshold for different regions.
### 3. Otsu’s Method

Automatic threshold selection.

---
# What is Window Slicing?

Window slicing = Intensity range selection.
Instead of single threshold:
We define a range:
$$T_1 \le f(x,y) \le T_2$$  

If inside window → keep  
Else → suppress

Used when:
Object has intensity in specific range.

Example:

- Bone in X-ray  
- Road in satellite image

---

# Mathematical Representation

$$g(x,y) =  
\begin{cases}  
1 & \text{if } T_1 \le f(x,y) \le T_2 \\  
0 & \text{otherwise}  
\end{cases}  $$


---

# Python Code – Global Threshold

```python
import cv2
import matplotlib.pyplot as plt

img = cv2.imread("image.jpg", 0)

# Global Threshold
_, thresh = cv2.threshold(img, 127, 255, cv2.THRESH_BINARY)

plt.figure(figsize=(8,4))

plt.subplot(1,2,1)
plt.imshow(img, cmap='gray')
plt.title("Original")
plt.axis("off")

plt.subplot(1,2,2)
plt.imshow(thresh, cmap='gray')
plt.title("Global Threshold")
plt.axis("off")

plt.show()
```

---

# Python Code – Window Slicing (Range Threshold)

```python
import numpy as np

# Define window range
T1 = 100
T2 = 180

window = np.zeros_like(img)

window[(img >= T1) & (img <= T2)] = 255

plt.figure(figsize=(8,4))

plt.subplot(1,2,1)
plt.imshow(img, cmap='gray')
plt.title("Original")
plt.axis("off")

plt.subplot(1,2,2)
plt.imshow(window, cmap='gray')
plt.title("Window Slicing")
plt.axis("off")

plt.show()
```

---

# Adaptive Threshold Example

```python
adaptive = cv2.adaptiveThreshold(
    img, 255,
    cv2.ADAPTIVE_THRESH_MEAN_C,
    cv2.THRESH_BINARY,
    11, 2)

plt.imshow(adaptive, cmap='gray')
plt.title("Adaptive Threshold")
plt.axis("off")
plt.show()
```

---

# Advantages & Limitations

|Advantage|Limitation|
|---|---|
|Simple|Fails if illumination uneven|
|Fast|Sensitive to noise|
|Good for clear objects|Hard if object & background overlap|

---

# Performance Considerations

Thresholding works best when:

-  Histogram is bimodal  
-  Object and background clearly separated

Fails when:

-  Histogram overlaps  
-  Lighting uneven

---

# Important Points

- Thresholding is region-based segmentation.
- Converts grayscale to binary.
- Window slicing selects intensity range.
- Otsu automatically selects threshold.
- Works best for bimodal histogram.

---

# Next: [[Component labeling]]