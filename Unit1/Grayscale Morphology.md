Tags: [[Image Analysis]]

# ==Grayscale Morphology==

Until now, all operations were mainly for **binary images (0 and 255)**.
Now we extend morphology to **grayscale images (0–255 intensity values)**.

---

# Grayscale Dilation

In grayscale dilation:

> Each pixel becomes the **maximum value** in its neighborhood defined by the structuring element.

---

## Mathematical Definition

- $(f \oplus b)(x,y) = \max_{(s,t) \in B} [f(x-s, y-t) + b(s,t)]$  

For flat structuring element (most common case):
 
- $(f \oplus B)(x,y) = \max { f(x-s, y-t) }$  

---

## Intuition

It:
- Brightens regions
- Expands bright areas
- Shrinks dark areas

---

##Code

```python
import cv2
import numpy as np

img = cv2.imread("image.jpg", 0)

kernel = np.ones((5,5), np.uint8)

gray_dilate = cv2.dilate(img, kernel)

cv2.imshow("Original", img)
cv2.imshow("Grayscale Dilation", gray_dilate)
cv2.waitKey(0)
```

---

# Grayscale Erosion

---

## What is it?

In grayscale erosion:

> Each pixel becomes the **minimum value** in its neighborhood.

---

## Mathematical Definition

$(f \ominus B)(x,y) = \min { f(x+s, y+t) }$  


---

## Intuition

It:

- Darkens regions
- Expands dark areas
- Shrinks bright areas

---

## Code

```python
gray_erode = cv2.erode(img, kernel)

cv2.imshow("Grayscale Erosion", gray_erode)
cv2.waitKey(0)
```

---

# Grayscale Opening

---

## Definition

$Opening = Erosion → Dilation$

$f \circ B = (f \ominus B) \oplus B$  

---

## Effect

- Removes small bright details
- Smooths image

---

## Code

```python
gray_open = cv2.morphologyEx(img, cv2.MORPH_OPEN, kernel)

cv2.imshow("Grayscale Opening", gray_open)
cv2.waitKey(0)
```

---

# Grayscale Closing

---

## Definition

$Closing = Dilation → Erosion$
  
$f \bullet B = (f \oplus B) \ominus B$  

---

## Effect

- Fills small dark gaps
- Smooths boundaries

---

## Code

```python
gray_close = cv2.morphologyEx(img, cv2.MORPH_CLOSE, kernel)

cv2.imshow("Grayscale Closing", gray_close)
cv2.waitKey(0)
```

---

# Key Difference: Binary vs Grayscale Morphology

|Binary|Grayscale|
|---|---|
|Pixels = 0 or 1|Pixels = 0–255|
|Logical operations|Min / Max operations|
|Shape based|Intensity based|

---

# Applications

- Noise removal  
- Background smoothing  
- Feature enhancement  
- Medical image processing  
- Industrial inspection

---
---


# ==END OF UNIT - 1==