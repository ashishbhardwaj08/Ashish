# What is a “Frequency Dimension”?

In a normal image, we work in **spatial dimensions**:

:  f(x, y) 

where  
• (x) = horizontal position  
• (y) = vertical position

After Fourier Transform, the image is represented as:
   F(u, v)  
where,
• (u) = frequency in x-direction  
• (v) = frequency in y-direction

 So **frequency dimension** means:

> instead of “where is a pixel?”,  
> we ask “how fast does intensity change in this direction?”

---

# Spatial Dimension vs Frequency Dimension

|Spatial Domain|Frequency Domain|
|---|---|
|x, y|u, v|
|pixel position|rate of change|
|brightness|frequency strength|
|image itself|spectrum of image|

Spatial:

```text
f(x, y)
```

Frequency:

```text
F(u, v)
```

---

# Meaning of Frequency in Images

Frequency = **how rapidly pixel values change**.

### Low frequency

• slow intensity change  
• smooth regions  
• background  
• large objects

### High frequency

• rapid intensity change  
• edges  
• noise  
• fine details

Example:

```text
1111111111   → very low frequency
1010101010   → high frequency
```

---

# What do u and v represent?

After Fourier Transform:

• **u-axis** → horizontal frequency  
• **v-axis** → vertical frequency

So:
$$F(u, v)  $$
means:  
frequency component that varies  
• u times in x-direction  
• v times in y-direction

---

# Center of Frequency Image

After shifting (fftshift):

```text
High freq   High freq
     \        /
       (0,0)
     /        \
High freq   High freq
```

• Center = (0,0) = **DC component** (average brightness)  
• Away from center = higher frequency

---

# Why it is called a “dimension”

Because Fourier transform converts:

2D spatial image  
→ 2D frequency representation

So we still have **two dimensions**, but now they don't represent position. They represent rate of change

Thus:
$$(x, y) \rightarrow (u, v)  $$

This is called a **dimension transformation**.

---

# Example: Vertical stripes image

Image:

```text
|||||||||||||
|||||||||||||
|||||||||||||
```

• Changes fast in x-direction  
• No change in y-direction

So in frequency domain:  
• strong u-frequency  
• weak v-frequency

That means energy appears along u-axis.

---

# Visual Example using Code

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

img = cv2.imread("image.jpg", 0)

f = np.fft.fft2(img)
fshift = np.fft.fftshift(f)

magnitude = 20*np.log(np.abs(fshift))

plt.subplot(121), plt.imshow(img, cmap='gray')
plt.title("Spatial Domain"), plt.axis('off')

plt.subplot(122), plt.imshow(magnitude, cmap='gray')
plt.title("Frequency Domain"), plt.axis('off')
plt.show()
```

Left → spatial dimension (x, y)  
Right → frequency dimension (u, v)

---

# Important Interpretation

A point in frequency domain:
$$F(u_0, v_0) $$ 
means:

> a sinusoidal pattern that changes u₀ times horizontally and  v₀ times vertically.

So frequency domain is actually a **map of patterns** inside the image.

---

# Why frequency dimension is useful

Because some operations are easier there:

• Blurring → remove high frequencies  
• Sharpening → amplify high frequencies  
• Periodic noise → appears as spikes  
• Texture analysis → frequency patterns

---
- Frequency dimension ≠ time  
- It is not audio frequency  
- It is **spatial frequency**

Unit:  
“cycles per pixel” (or per image width)

---

# Summary

In image processing, the **frequency dimension (u, v)** represents  how fast pixel intensities change in the image, while the spatial dimension (x, y) represents where the pixels are.

Or
$$f(x,y) \xrightarrow{FT} F(u,v) $$
**position → frequency**

---


# Next: [[Fourier Transform]]