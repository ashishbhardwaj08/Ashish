
# Definition

A **digital image** is a 2D function:
$$f(x, y)$$  
where  
• (x, y) → spatial coordinates (pixel position)  
• (f(x, y)) → intensity (brightness or color value)

In computers, an image is stored as a **matrix (array of numbers)**.

So an image = **numerical data arranged in rows and columns**.

---

# Pixel (Picture Element)

A **pixel** is the smallest unit of an image.

Each pixel stores:  
• brightness  
• or color information

Example:

```
[ 52,  80, 120, 200 ]
```

Each number = pixel intensity.

---

# Image Representation (Mathematical Form)

## (A) Grayscale Image

Represented as a **2D matrix**:
$$
I =  
\begin{bmatrix}  
52 & 55 & 61\\  
68 & 70 & 75\\  
80 & 85 & 90  
\end{bmatrix} $$ 

Pixel values usually in range:   
$$0 \le I(x,y) \le 255  $$

0 = black  
255 = white

---

## (B) Binary Image

Pixel values:  
$$I(x,y) \in {0, 255}  $$
Example:

```
0   0 255
0 255 255
0   0   0
```

---

## (C) Color Image (RGB)

Represented as a **3D matrix**:
$$I(x,y) = [R, G, B] $$ 

Example:
$$I =  
\begin{bmatrix}  
[255,0,0] & [0,255,0]\\  
[0,0,255] & [255,255,0]  
\end{bmatrix}  
$$

So shape is:

```
(height, width, 3)
```

---

# Bit Depth and Image Range

|Bit depth|Possible values|
|---|---|
|1-bit|0,1|
|8-bit|0–255|
|16-bit|0–65535|
|24-bit (color)|8 bits per channel|

Most OpenCV images are **8-bit unsigned integers (uint8)**.

---

# Image as NumPy Array (Core Idea)

In Python, images are stored as **NumPy arrays**.

Example:

```python
import numpy as np

img = np.array([[10, 20, 30],
                [40, 50, 60],
                [70, 80, 90]])

print(type(img))      # numpy.ndarray
print(img.shape)     # (3,3)
```

So: **Image = NumPy array**

---

# Image Handling using OpenCV

## 1. Reading an Image

```python
import cv2

img = cv2.imread("image.jpg")

print(type(img))      # numpy.ndarray
print(img.shape)     # (height, width, 3)
```

OpenCV reads images in **BGR format**, not RGB.

---

## 2. Displaying an Image

```python
cv2.imshow("Image", img)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

---

## 3.  Convert to Grayscale

```python
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
```

Now:

```
shape = (height, width)
```

---

## 4.  Saving an Image

```python
cv2.imwrite("output.jpg", gray)
```

---

# Accessing Pixel Values (NumPy)

```python
pixel = img[100, 50]     # row=100, col=50
print(pixel)             # [B, G, R]
```

For grayscale:

```python
value = gray[100, 50]
```

---

# Modifying Pixel Values

```python
img[100, 50] = [0, 0, 255]   # make that pixel red
```

---

# Slicing (Region of Interest – ROI)

```python
roi = img[100:200, 200:300]
cv2.imshow("ROI", roi)
```

This extracts a **sub-image**.

---

# Image Properties using NumPy

```python
print(img.shape)   # (h, w, c)
print(img.size)    # total pixels
print(img.dtype)  # uint8
```

---

# Creating Images using NumPy

## Black Image

```python
black = np.zeros((300,300), dtype=np.uint8)
cv2.imshow("Black", black)
```

---

## White Image

```python
white = np.ones((300,300), dtype=np.uint8) * 255
cv2.imshow("White", white)
```

---

## Color Image

```python
color = np.zeros((300,300,3), dtype=np.uint8)
color[:] = [255,0,0]  # Blue in BGR
cv2.imshow("Color", color)
```

---

# Image Arithmetic (NumPy + OpenCV)

```python
bright = cv2.add(img, 50)
dark = cv2.subtract(img, 50)
```

---

# Image Coordinate System

```
(0,0) --------> x (columns)
  |
  |
  v
  y (rows)
```

Access:

```python
img[y, x]
```

---

# Image Data Flow (Pipeline)

```
Image file (.jpg/.png)
        ↓
cv2.imread()
        ↓
NumPy Array
        ↓
Processing (filtering, thresholding, etc.)
        ↓
cv2.imshow() / cv2.imwrite()
```

---

# Applications

• Computer vision  
• Medical imaging  
• Satellite image processing  
• OCR  
• Face recognition  
• Motion detection

---

# Limitations

- Large images → high memory  
- Noise affects pixel values  
- OpenCV uses BGR not RGB (confusing)  
- Precision loss in 8-bit images

---

# Summary

- Image = matrix of pixel values  
- Binary → 2 values  
- Grayscale → 0–255  
- Color → 3 channels  
- OpenCV stores image as NumPy array  
- NumPy allows pixel-level operations  
- Python + OpenCV = easy image handling

---
