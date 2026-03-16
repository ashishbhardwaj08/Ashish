### Optical Zoom

**Optical zoom** is achieved by physically moving the camera lens to magnify the image before it is captured.

• Uses lens adjustment  
• Maintains original image resolution  
• No loss of image quality  
• True zooming method  
• Expensive and hardware-based

**Result:** Image remains sharp and clear.

---

### Digital Zoom

**Digital zoom** is achieved by cropping and enlarging a portion of the image using software after capture.

• Uses image processing  
• Reduces image resolution  
• Causes pixelation and blurring  
• Not true zooming  
• Cheaper and software-based

**Result:** Image quality degrades.

---
In **digital zoom**, we **increase image size by adding new pixels (rows & columns)** between existing ones, and then **fill those new pixels using interpolation**.

That means:  
- We **create blank pixel positions**  
-  Then **estimate their values** from nearby pixels

Common methods:  
• **Nearest neighbor** → copy closest pixel  
• **Bilinear** → average of nearby pixels  
• **Bicubic** → weighted average of more neighbors

So yes — conceptually:

> **we insert empty rows/columns and fill them with averaged (interpolated) values**,  
> but this **does NOT add new real detail**, only smooths the image.
---

### Key Differences

|Feature|Optical Zoom|Digital Zoom|
|---|---|---|
|Method|Lens movement|Image cropping|
|Image quality|Preserved|Degraded|
|Resolution|Same|Reduced|
|Nature|Hardware-based|Software-based|
|Cost|High|Low|

---

**Optical zoom magnifies using lenses without quality loss, whereas digital zoom enlarges pixels causing loss of resolution.**




# Next: [[Color Schemas]]