
---

# Definition

A **binary image** is an image in which each pixel can take **only two possible intensity values**:

• **0 → Black (background)**  
• **1 or 255 → White (foreground/object)**

Mathematically, a binary image is:
  
$$B(x, y) \in {0, 1} \quad \text{or} \quad {0, 255}  $$

So instead of having 256 gray levels (0–255), it has only **two levels**.

---

# 2. Importance

Binary images are the **foundation** of many image processing tasks:

• Object detection  
• Shape analysis  
• Region labeling  
• Morphological operations  
• Boundary extraction  
• OCR (text recognition)  
• Medical image segmentation

They convert a complex image into a **logical image (YES/NO per pixel)**.
Example:

> “Is this pixel part of the object?”  
> → White = YES  
> → Black = NO

---

# How Binary Images are Created

Binary images are usually obtained from:
### (A) Grayscale Image
Convert RGB → Grayscale → Binary
### (B) Thresholding

Rule:  

$$B(x,y) =  
\begin{cases}  
255, & \text{if } I(x,y) \ge T \\  
0, & \text{if } I(x,y) < T  
\end{cases}$$  
Where:  
• (I(x,y)) = original gray pixel  
• (T) = threshold value

---

# Types of Binary Images

### 1. Global Threshold Binary Image
Single threshold value for whole image.

### 2. Adaptive Binary Image

Threshold changes for each local region.

### 3. Inverted Binary Image

Foreground becomes black, background white.

---

# OpenCV Implementation

## Step 1: Convert Image to Binary

```python
import cv2
import numpy as np

# Load image
image = cv2.imread("image.jpg")

# Convert to grayscale
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

# Apply binary thresholding
_, binary = cv2.threshold(gray, 127, 255, cv2.THRESH_BINARY)

# Show results
cv2.imshow("Original", image)
cv2.imshow("Grayscale", gray)
cv2.imshow("Binary Image", binary)

cv2.waitKey(0)
cv2.destroyAllWindows()
```

---

## Step 2: Inverted Binary Image

```python
_, binary_inv = cv2.threshold(gray, 127, 255, cv2.THRESH_BINARY_INV)

cv2.imshow("Inverted Binary", binary_inv)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

---

## Step 3: Adaptive Binary Image

```python
adaptive = cv2.adaptiveThreshold(
    gray,
    255,
    cv2.ADAPTIVE_THRESH_MEAN_C,
    cv2.THRESH_BINARY,
    11,
    2
)

cv2.imshow("Adaptive Binary", adaptive)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

---

# Pixel-Level Working Example

Suppose grayscale values:

```
120 140 160
90  200 180
60  130 255
```

Threshold T = 128

Binary result:

```
0   255 255
0   255 255
0   255 255
```

Logic:  
If pixel ≥ 128 → white  
Else → black

---

# Memory Representation

Binary image (8-bit):

• White = 255 = 11111111  
• Black = 0 = 00000000

It can also be stored as:  
• Boolean (True/False)  
• Bit-level image (1 bit per pixel)

---

# Applications of Binary Images

### 1. Object Segmentation
Separate object from background.
### 2. OCR (Text Extraction)
Text becomes white, background black.
### 3. Medical Imaging
Tumor vs non-tumor regions.
### 4. Industrial Vision
Detect defective parts.
### 5. Shape & Area Measurement
Count pixels of object.

---

# Limitations of Binary Images

- Sensitive to lighting  
- Threshold selection is difficult  
- Loses gray-level detail  
- Noise can appear as false objects  
- Shadows may become foreground

Example problem:  
Dark shadow may be detected as an object.

---

# Binary Image vs Grayscale vs Color

| Type      | Pixel Values                      | Information |
| --------- | --------------------------------- | ----------- |
| Color     | {R (0-255), G (0-255) ,B (0-255)} | Full color  |
| Grayscale | 0–255                             | Intensity   |
| Binary    | 0 or 255                          | Logical     |

Binary = **simplest but most aggressive reduction of information**.

---

# Binary Images in Image Processing Pipeline

Typical pipeline:

```
RGB Image
   ↓
Grayscale Image
   ↓
Binary Image
   ↓
Morphology
   ↓
Connected Components
   ↓
Feature Extraction
```

---

# Summary

- Binary image has only **two pixel values**  
- Created using **thresholding**  
- Used for **segmentation and object analysis**  
- Very fast and memory efficient  
- But sensitive to **noise and illumination**

---

