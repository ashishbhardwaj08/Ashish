2026-02-11  00:42


# Edge Detection

These filters are used to highlight intensity changes (edges)
#  Mathematical Insight

Boundary is treated as periodic signal:

$$
$$

$$
z(n) = \sum_{k=1}^{p} a_k \, z(n-k)
$$

The AR coefficients capture:

- Curvature behavior
- Oscillation


### Prewitt Operator

- Detects edge in horizontal and vertical direction
- Gx (horizontal edges):
$$
\begin{bmatrix}
-1 & 0 & 1 \\
-1 & 0 & 1 \\
-1 & 0 & 1
\end{bmatrix}
$$

- Gy (vertical edges):
$$
\begin{bmatrix}
-1 & -1 & -1 \\
0 & 0 & 0 \\
1 & 1 & 1
\end{bmatrix}
$$

- Edge Magnitude 
$$
\sqrt{Gx2+Gy2}​
$$



### Sobel Operator

Improved Prewitt (more weight to center).

Gx:
$$
\begin{bmatrix} -1 & 0 & 1 \\ -2 & 0 & 2 \\ -1 & 0 & 1 \end{bmatrix}​​

$$


Gy:
$$
\begin{bmatrix} 1 & 2 & 1 \\ 0 & 0 & 0 \\ -1 & -2 & -1 \end{bmatrix}​
$$


-  Stronger edge detection  
-  Noise resistant  
- Used in: object detection, feature extraction

###  Laplacian Operator

Second-order derivative → detects edges in all directions.

Kernel:
$$
\begin{bmatrix} 0 & -1 & 0 \\ -1 & 4 & -1 \\ 0 & -1 & 0 \end{bmatrix}
$$
​

or
$$
\begin{bmatrix} -1 & -1 & -1 \\ -1 & 8 & -1 \\ -1 & -1 & -1 \end{bmatrix}​
$$


✔ Direction-independent  
❌ Very sensitive to noise  
Often applied after Gaussian blur (LoG – Laplacian of Gaussian)

### Next: [[]]
