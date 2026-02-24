When you write:
```python
_, binary = cv2.threshold(gray, 127, 255, cv2.THRESH_BINARY)
```
you see **two variables on the left side** because:
> `cv2.threshold()` returns **two outputs**, not one.

---

# What Does `cv2.threshold()` Return?

The function actually returns:

```python
ret, thresh = cv2.threshold(...)
```

So internally it gives:
1. **ret** → the threshold value used
2. **thresh** → the thresholded image
---

# What Each Output Means

### 1. `ret`

This is the **threshold value used**.
- If you manually set threshold = 127 → `ret = 127`
- If you use Otsu’s method → `ret` will be automatically computed threshold
Example:
```python
ret, binary = cv2.threshold(gray, 127, 255, cv2.THRESH_BINARY)
print(ret)
```
Output:
```
127.0
```

---

### 2. `binary`
This is the **resulting binary image**.
Pixels become:
```
0        if gray < 127
255      if gray ≥ 127
```
This is what we usually need for morphology.

---

# Why Use `_` Instead of `ret`?

In Python, `_` means:
> "I am intentionally ignoring this value."
So:
```python
_, binary = cv2.threshold(...)
```
means:
- We don’t care about threshold value
- We only want the binary image
It’s just a Python convention.

---

# When Should We NOT Use `_`?

When using **Otsu thresholding**:
```python
ret, binary = cv2.threshold(gray, 0, 255,
                            cv2.THRESH_BINARY + cv2.THRESH_OTSU)

print("Optimal threshold:", ret)
```
Here:
- `ret` is important because OpenCV calculates the best threshold automatically.
---

# Why Does OpenCV Return Two Values?

Because thresholding can be:
- Manual (you give threshold)
- Automatic (Otsu, Triangle methods)
So OpenCV always returns the used threshold value.

---
# Summary

|Variable|Meaning|
|---|---|
|`_` or `ret`|Threshold value used|
|`binary`|Output thresholded image|

---

