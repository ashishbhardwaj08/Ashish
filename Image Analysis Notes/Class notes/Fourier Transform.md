# DEFINITION

**Fourier Transform (FT)** is a mathematical tool that converts a signal from the **spatial (or time) domain** into the **frequency domain**.

> It represents a signal as a sum of sine and cosine waves of different frequencies, amplitudes, and phases.

In image processing:

> Fourier Transform converts an image from **pixel intensity representation** into **frequency representation**.

---
# Basic Idea

An image has:  
• **Slow changes** → low frequency  
• **Sharp edges & noise** → high frequency

Fourier Transform answers:  
_How much of each frequency is present in the image?_

So instead of:

```
pixel values (x, y)
```

we get:

```
frequencies (u, v)
```

---
# 📌 3. MATHEMATICAL FORMULA

### 1D Fourier Transform:

$$F(u) = \int_{-\infty}^{\infty} f(x); e^{-j2\pi ux} dx  $$

### 2D Fourier Transform (for images):

$$F(u,v) = \sum_{x=0}^{M-1} \sum_{y=0}^{N-1} f(x,y) e^{-j2\pi\left(\frac{ux}{M}+\frac{vy}{N}\right)}  $$

Where:  
• ( f(x,y) ) = image in spatial domain  
• ( F(u,v) ) = frequency domain representation  
• ( u,v ) = frequency coordinates  
• $$(j = \sqrt{-1})$$
# WHAT IS FREQUENCY IN IMAGE?

|Concept|Meaning|
|---|---|
|Low frequency|Smooth regions|
|High frequency|Edges, noise|
|DC component|Average brightness|

Center of spectrum = low frequency  
Outer region = high frequency

# WORKING PRINCIPLE

### Step-by-step:

1. Take image in spatial domain
2. Apply Fourier Transform
3. Get complex values (real + imaginary)
4. Compute magnitude spectrum
5. Shift zero frequency to center
6. Apply filtering if needed
7. Apply inverse Fourier transform to reconstruct image

Flow:

```
Image → FFT → Frequency Domain → Modify → IFFT → Output Image
```
# WHY WE USE FOURIER TRANSFORM?

- To analyze frequency components  
- To remove noise  
- To enhance edges  
- For filtering  
- For compression  
- For texture analysis
# IMPORTANT PROPERTIES

1. **Linearity**  $$FT(af + bg) = aFT(f) + bFT(g)$$
2. **Translation property**  
    Shift in spatial → phase change in frequency
3. **Scaling**  
    Shrinking image → frequency spreads
4. **Convolution theorem**  
    Convolution in spatial = multiplication in frequency
5. **Energy preservation (Parseval’s theorem)**

---
# FREQUENCY DOMAIN FILTERING

|Filter|Passes|Removes|
|---|---|---|
|Low pass|Low freq|Noise|
|High pass|High freq|Smooth areas|
|Band pass|Selected band|Others|
# APPLICATIONS

- Image enhancement  
- Image restoration  
- Noise reduction  
- Edge detection  
- Texture analysis  
- Image compression (JPEG uses DCT – related to FT)  
- Medical imaging  
- Astronomy  
- Audio processing

---

# LIMITATIONS
- Computationally expensive  
- Loses spatial locality  
- Not good for non-stationary signals  
- Difficult to interpret visually  
- Phase information often ignored

---

# PYTHON CODE (FFT on Image)

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

# Read image in grayscale
img = cv2.imread('image.jpg', 0)

# Apply Fourier Transform
f = np.fft.fft2(img)

# Shift zero frequency to center
fshift = np.fft.fftshift(f)

# Magnitude spectrum
magnitude = 20 * np.log(np.abs(fshift) + 1)

# Inverse Fourier Transform
f_ishift = np.fft.ifftshift(fshift)
img_back = np.fft.ifft2(f_ishift)
img_back = np.abs(img_back)

# Display results
plt.subplot(131), plt.imshow(img, cmap='gray')
plt.title('Original Image'), plt.axis('off')

plt.subplot(132), plt.imshow(magnitude, cmap='gray')
plt.title('Magnitude Spectrum'), plt.axis('off')

plt.subplot(133), plt.imshow(img_back, cmap='gray')
plt.title('Reconstructed Image'), plt.axis('off')

plt.show()
```

---

# IMPORTANT POINTS

- Fourier Transform converts spatial → frequency domain  
- Low frequencies = smooth areas  
- High frequencies = edges & noise  
- DC component = average intensity  
- Filtering is easier in frequency domain  
- Uses complex numbers  
- Inverse FT reconstructs original image  
- Used in noise removal and enhancement
- Window size must stay same during transformation and inverse transformation

---

# SHORT NOTES

**Magnitude Spectrum:**  
$$|F(u,v)| = \sqrt{R^2 + I^2}  $$
**Phase Spectrum:**  
$$\theta = \tan^{-1}(I/R)  $$

Magnitude shows strength  
Phase shows structure
