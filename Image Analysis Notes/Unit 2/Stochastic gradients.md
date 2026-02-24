Tags:  [[_Unit -2]]

# ==**Stochastic Gradient Edge Detection**==
# Need for Stochastic Gradient

So far:

- Sobel → deterministic
- Laplacian → deterministic
- Kirsch → deterministic

They directly compute derivatives.

But real world images contain:

- Noise
- Random intensity variations
- Illumination changes

So edges are not perfectly sharp.

Instead of treating image as fixed values,  
we treat pixel intensities as:

> Random variables (stochastic process)

Hence:

**Stochastic Gradient = Statistical estimation of gradient in presence of noise**
# Basic Idea

In noisy images:

Observed image:
$$g(x,y) = f(x,y) + n(x,y)  $$


Where:
- ( f(x,y) ) = true image
- ( n(x,y) ) = random noise

Traditional gradient detects both:

- True edges
- Noise edges

Stochastic gradient tries to:

-  Estimate expected gradient  
- Reduce noise influence 
- Improve edge reliability
# Conceptual Approach

Instead of direct derivative:

We estimate:
  
$$E[\nabla g(x,y)] $$ 

Where:

E = Expected value (statistical mean)

This is done using:
- Local averaging
- Probability modeling
- Statistical tests
# Methods Used in Stochastic Gradient

Common approaches:

### Smoothing before gradient
(Gaussian is a statistical filter)

### Canny Edge Detector
(Uses gradient + statistical thresholding)

### Hypothesis testing
Check whether intensity change is statistically significant.
# Example: Canny (Best Practical Example)

Canny includes:

1. Gaussian smoothing
2. Gradient calculation (Sobel)
3. Non-maximum suppression
4. Double threshold
5. Edge tracking by hysteresis
It is statistically motivated.


# Canny (Stochastic-like Approach)

```python
import cv2
import matplotlib.pyplot as plt

# Read image
img = cv2.imread("image.jpg", 0)

# Apply Canny
edges = cv2.Canny(img, 100, 200)

plt.figure(figsize=(8,4))

plt.subplot(1,2,1)
plt.imshow(img, cmap='gray')
plt.title("Original")
plt.axis("off")

plt.subplot(1,2,2)
plt.imshow(edges, cmap='gray')
plt.title("Canny Edge Detection")
plt.axis("off")

plt.show()
```

---

# Why Canny is Considered Stochastic?

Because:

- Uses Gaussian smoothing (statistical filtering)
- Uses thresholding based on gradient magnitude
- Uses hysteresis (probabilistic linking)

It minimizes:

- False positives  
- Noise edges  
-  edges

---

# Performance Comparison

| Operator  | Noise Handling | Accuracy         | Complexity |
| --------- | -------------- | ---------------- | ---------- |
| Sobel     | Low            | Medium           | Low        |
| Laplacian | Very Low       | Medium           | Low        |
| Kirsch    | Low            | High directional | High       |
| Canny     | High           | Very High        | Moderate   |

---

# Important Exam Points

- Stochastic methods treat intensity as random variable.
- Based on statistical estimation.
- Reduce noise impact.
- Canny is best practical example.
- More reliable in real-world images.


# Next: [[Performance of edge detector operators]]