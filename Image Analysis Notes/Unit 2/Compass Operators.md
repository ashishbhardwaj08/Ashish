Tags:  [[_Unit -2]]
 
 > **Edge Detection – Directional Masks**

# Basic Idea

Gradient operators detect edges in **x and y direction only**.

But compass operators detect edges in:

> All 8 directions (N, NE, E, SE, S, SW, W, NW)

They use **8 different masks**, each rotated by 45°.

Idea:

1. Apply all 8 masks.
2. Take maximum response.
3. That direction = edge direction.

Gradient only gives:

- Horizontal
- Vertical

But edges can exist in:

- 45°
- 135°
- etc.

Compass operators improve direction detection.
## Types of Compass Operators

Main types includes:

- Robinson operator
- Kirsch operator
# 1. Kirsch Operator (Very Important)

It uses strong positive weights in one direction.

### North mask:
$$  
\begin{bmatrix}  
5 & 5 & 5 \\  
-3 & 0 & -3 \\  
-3 & -3 & -3  
\end{bmatrix}  
$$

Other 7 masks are rotated versions.

---

## All 8 Kirsch Masks

### North (N)

```
 5  5  5
-3  0 -3
-3 -3 -3
```

### North-East (NE)

```
 5  5 -3
 5  0 -3
-3 -3 -3
```

### East (E)

```
 5 -3 -3
 5  0 -3
 5 -3 -3
```

### South-East (SE)

```
-3 -3 -3
 5  0 -3
 5  5 -3
```

### South (S)

```
-3 -3 -3
-3  0 -3
 5  5  5
```

### South-West (SW)

```
-3 -3 -3
-3  0  5
-3  5  5
```

### West (W)

```
-3 -3  5
-3  0  5
-3 -3  5
```

### North-West (NW)

```
-3  5  5
-3  0  5
-3 -3 -3
```

---
## Working

For each pixel:

1. Convolve with all 8 masks
2. Compute response
3. Take maximum absolute value


$$Edge(x,y) = max(|R_1|, |R_2|, ..., |R_8|)  $$


> Direction = mask with highest response.

## Properties of Kirsch

- Very strong directional detection  
- High edge response  
- Very sensitive to noise  
- Computationally heavy (8 convolutions)

# Robinson Operator

Similar to Kirsch but simpler weights.

### North mask:

```
-1  0  1
-2  0  2
-1  0  1
```

Rotated 8 times.

Difference from Kirsch:

- Uses smaller weights
- Less aggressive
- Slightly less noise sensitive

# Python Code – Kirsch Operator

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

# Read image in grayscale
img = cv2.imread("image.jpg", 0)

# ==============================
# 🔹 KIRSCH OPERATOR
# ==============================

kirsch_masks = [
    np.array([[5,5,5],[-3,0,-3],[-3,-3,-3]]),      # N
    np.array([[5,5,-3],[5,0,-3],[-3,-3,-3]]),      # NE
    np.array([[5,-3,-3],[5,0,-3],[5,-3,-3]]),      # E
    np.array([[-3,-3,-3],[5,0,-3],[5,5,-3]]),      # SE
    np.array([[-3,-3,-3],[-3,0,-3],[5,5,5]]),      # S
    np.array([[-3,-3,-3],[-3,0,5],[-3,5,5]]),      # SW
    np.array([[-3,-3,5],[-3,0,5],[-3,-3,5]]),      # W
    np.array([[-3,5,5],[-3,0,5],[-3,-3,-3]])       # NW
]

kirsch_responses = []

for mask in kirsch_masks:
    response = cv2.filter2D(img, cv2.CV_64F, mask)
    kirsch_responses.append(np.abs(response))

kirsch_edge = np.max(np.stack(kirsch_responses), axis=0)
kirsch_edge = np.uint8(np.clip(kirsch_edge, 0, 255))


# ==============================
# 🔹 ROBINSON OPERATOR
# ==============================

robinson_masks = [
    np.array([[-1,0,1],[-2,0,2],[-1,0,1]]),   # E
    np.array([[0,1,2],[-1,0,1],[-2,-1,0]]),   # NE
    np.array([[1,2,1],[0,0,0],[-1,-2,-1]]),   # N
    np.array([[2,1,0],[1,0,-1],[0,-1,-2]]),   # NW
    np.array([[1,0,-1],[2,0,-2],[1,0,-1]]),   # W
    np.array([[0,-1,-2],[1,0,-1],[2,1,0]]),   # SW
    np.array([[-1,-2,-1],[0,0,0],[1,2,1]]),   # S
    np.array([[-2,-1,0],[-1,0,1],[0,1,2]])    # SE
]

robinson_responses = []

for mask in robinson_masks:
    response = cv2.filter2D(img, cv2.CV_64F, mask)
    robinson_responses.append(np.abs(response))

robinson_edge = np.max(np.stack(robinson_responses), axis=0)
robinson_edge = np.uint8(np.clip(robinson_edge, 0, 255))


# ==============================
# 🔹 DISPLAY OUTPUTS
# ==============================

plt.figure(figsize=(12,5))

plt.subplot(1,3,1)
plt.imshow(img, cmap='gray')
plt.title("Original Image")
plt.axis("off")

plt.subplot(1,3,2)
plt.imshow(kirsch_edge, cmap='gray')
plt.title("Kirsch Edge Detection")
plt.axis("off")

plt.subplot(1,3,3)
plt.imshow(robinson_edge, cmap='gray')
plt.title("Robinson Edge Detection")
plt.axis("off")

plt.tight_layout()
plt.show()
```
> [!NOTE] OUTPUT
> **Kirsch** → stronger, sharper edges, more noise
> **Robinson** → smoother directional edges
> Kirsch generally gives stronger response

# Performance Comparison

|Operator|Directions|Noise Sensitivity|Computation|
|---|---|---|---|
|Sobel|2|Low|Fast|
|Kirsch|8|High|Slow|
|Robinson|8|Medium|Slow|

Compass operators give better orientation detection but are heavier.

---

# Important Points

- Compass operators detect edges in 8 directions.
- Kirsch uses weights 5 and -3.
- Edge = maximum directional response.
- More computationally expensive than Sobel.


## Next: [[Laplace Operators]]