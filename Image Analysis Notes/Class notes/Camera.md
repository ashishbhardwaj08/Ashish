# 1. Introduction – The Camera 

CLICK 3 DOTS AND OPEN TO RIGHT

![[lec02_camera.pdf]]

## 1.1 What is a Camera?

A **camera** is a device that **captures light from the real world and converts it into an image**.
In simple terms:
**Real world (3D objects) → Light enters camera → Image formed on sensor/film → 2D picture**
So a camera performs a very important transformation:
**3D world → 2D image**


---

# 2. How Do We See the World?

Before understanding cameras, we first understand **human vision**.

### In human eyes

1. Light reflects from objects.
2. Light enters the eye.
3. Lens focuses light.
4. Image forms on the **retina**.
5. Brain interprets the image.
The **camera works in a very similar way**.

|Human Eye|Camera|
|---|---|
|Cornea + Lens|Camera lens|
|Retina|Image sensor|
|Pupil|Aperture|
|Brain|Image processing|

---

# 3. First Attempt at Building a Camera

The slide proposes an experiment:

> Idea: Put a piece of film in front of an object.

### What happens?

Light from the object goes in **many directions**.

If we place film directly:

- Rays from different parts of the object mix together.
- The image becomes **blurry**.

This happens because **too many light rays reach each point on the film**.

---

# 4. Solution – Blocking Light Rays

To reduce blurring, we block most rays.
We place a **barrier with a small hole**.

This hole is called:

### **Aperture**

So now:

- Only a **small set of rays** pass through.
- Rays come from one direction.
- Image becomes clearer.

This leads to the **pinhole camera**.

---

# 5. Pinhole Camera

## Definition

A **pinhole camera** is a simple camera without a lens that forms an image using a **tiny hole (aperture)**.

### Structure

It contains:

1. A **dark box**
2. A **small hole (pinhole)**
3. An **image plane (film/sensor)**

```
Object → Light rays → Pinhole → Image plane
```

---

## Important Concept

All light rays pass through **one single point**.

This point is called:

### **Center of Projection (COP)**

Also called:

- Optical center
- Focal point

---

## Image Formation

Steps:

1. Light leaves object point.
2. Rays travel in many directions.
3. Only rays through **pinhole** enter camera.
4. Rays hit image plane.
5. Image is formed.

---

## Important Observation

The image formed is:

- **Upside down**
- **Left-right reversed**

This happens because light rays **cross at the pinhole**.

---

# 6. Dimensionality Reduction (3D → 2D)

In real life:

Objects exist in **3D space**.
But images are **2D**.
So camera performs:

### **Dimensionality Reduction**

```
3D World → 2D Image
```

Example:

|Real Object|Image|
|---|---|
|Cube|Square projection|
|Sphere|Circle|
|Building|Flat picture|

---

## What Information Is Lost?

When converting **3D → 2D**, we lose:

1. **Angles**
2. **Distances**
3. **Depth information**

This is why from a single photo we cannot easily tell:

- How far objects are
- Their true size

---

# 7. Projection Properties

Projection has several mathematical properties.

---

## 7.1 Many-to-One Mapping

Multiple 3D points may map to the **same image point**.
Example:
Imagine a **laser ray**.

All points on that ray project to **one pixel**.

```
P1
P2
P3
   \
    \ → same image point
```

---

## 7.2 Points → Points

Each **3D point** becomes a **2D point** in the image.

---

## 7.3 Lines → Lines

A straight line in 3D usually remains a **straight line in the image**.

Example:

- Edge of building
- Road line

But there is an exception.

### Exception

If a line passes through the **center of projection**, it becomes **a point in the image**.

---

## 7.4 Planes → Planes

A 3D plane generally becomes a **2D plane** in the image.

Example:

- Wall
- Ground
- Table surface

But if the plane passes through the **camera center**, it may appear as a **line**.

---

# 8. Parallel Lines and Vanishing Point

This is one of the most famous effects in perspective projection.

### Observation

Parallel lines appear to **meet at a point** in images.

Example:

- Railway tracks
- Roads
- Building edges

They appear to meet at:

### **Vanishing Point**

---

## Why Does This Happen?

Because objects further away appear **smaller**.

As distance increases, lines visually converge.

Each direction in space has its **own vanishing point**.

---

### Example

|Direction|Vanishing point|
|---|---|
|Road direction|Horizon|
|Vertical building lines|Sky point|
|Side walls|Side vanishing point|

---

### Exception

If parallel lines are **parallel to the image plane**, they remain **parallel**.

Example:

A wall directly facing the camera.

---

# 9. One-Point Perspective

Artists discovered this phenomenon long ago.

A famous example:

**Masaccio’s Trinity painting (1425)**.

In one-point perspective:

- All parallel lines converge to **one vanishing point**.

Common in:

- Hallways
- Roads
- Railway track
---

# 10. Perspective Distortion

Perspective projection causes **distortion**.

Example question from slide:

> What does a sphere project to?

Answer:

A **circle** (from most viewpoints).

But perspective can also change apparent sizes.

---

### Example: Columns of a Building

Columns closer to the camera appear:
- **Larger**

Columns further away appear:
- **Smaller**

This is **perspective distortion**.
It is **not caused by lens errors**.
It is a **natural geometric effect**.

This problem was noted by **Leonardo da Vinci**.

---

### Problem in Architecture Photography

When you tilt a camera upward to capture a building:

Vertical lines appear to **converge**.

This makes buildings look like they are **falling backward**.

---

### Solution
### **Perspective correction lens (tilt-shift lens)**

It shifts the lens relative to the sensor.

Result:
- Vertical lines remain **parallel**.
---

# 11. Modeling Projection (Camera Coordinate System)

To mathematically describe how a camera forms an image, we create a **coordinate system**.

### Setup of the Coordinate System

We assume:

1. The **camera center (optical center)** is at the origin
    ```
    O = (0,0,0)
    ```
2. The **image plane** is placed in front of the camera.
3. The world is represented using **3D coordinates**


```
P = (x, y, z)
```

Where:

|Coordinate|Meaning|
|---|---|
|x|horizontal direction|
|y|vertical direction|
|z|depth (distance from camera)|

So a point in the real world is:

```
P(x,y,z)
```

---

# 12. Projection Equations

Now we want to know:

**Where will this 3D point appear in the 2D image?**

We calculate where the **ray from the point through the camera center intersects the image plane**.

This is derived using **similar triangles**.

---

## Projection Formula

The projected image point is:
  
$x' = \frac{f x}{z}$  

$y' = \frac{f y}{z}$  

Where:

|Symbol|Meaning|
|---|---|
|x,y,z|3D coordinates of object|
|f|focal length|
|x',y'|2D image coordinates|

---

## Intuition

The division by **z** causes perspective.

Meaning:

- **Far objects (large z)** → appear smaller
- **Near objects (small z)** → appear larger

This explains **perspective effect in photos**.

---

# 13. Example of Projection

### Example 1

Suppose:

```
Object point P = (2, 4, 10)
Focal length f = 5
```

Using the projection formula:

 
$x' = \frac{5 \times 2}{10} = 1$  


$y' = \frac{5 \times 4}{10} = 2$  

So the point appears in the image at:

```
(1 , 2)
```

---

### Example 2 (Perspective Effect)

Two objects:

|Object|Coordinates|
|---|---|
|A|(2,2,5)|
|B|(2,2,20)|

Let:

```
f = 10
```

For A:

```
x' = 10*2/5 = 4
y' = 10*2/5 = 4
```

For B:

```
x' = 10*2/20 = 1
y' = 10*2/20 = 1
```

### Result

|Object|Image Position|
|---|---|
|Near object|(4,4)|
|Far object|(1,1)|

So the **far object appears smaller**.

This is exactly what we see in photos.

---

# 14. Removing the Z Coordinate

The 3D point becomes:

```
(x', y')
```

We **drop the z coordinate** because an image is **2D**.

---

# 15. Is Projection Linear?

The slide asks:

> Is this a linear transformation?

The answer is **No**.

Why?

Because the equation contains **division by z**.

Division makes it **non-linear**.

---

# 16. Homogeneous Coordinates

To convert projection into matrix multiplication, we use **homogeneous coordinates**.

### Idea

Add an extra coordinate.

For a 3D point:

```
(x, y, z)
```

becomes

```
(x, y, z, 1)
```

For image points:

```
(x', y')
```

becomes

```
(x', y', 1)
```

This trick allows projection to be written using **matrix multiplication**.

---

# 17. Perspective Projection Matrix

Using homogeneous coordinates, projection can be written as:

$$  
\begin{bmatrix}  
x' \\ 
y' \\  
z'  
\end{bmatrix}
=
\begin{bmatrix}  
f & 0 & 0 & 0 \\  
0 & f & 0 & 0 \\  
0 & 0 & 1 & 0  
\end{bmatrix}  
\begin{bmatrix}  
x \\  
y \\  
z \\ 
1  
\end{bmatrix}  
$$


After multiplication we divide by the third coordinate.

This gives the final:

```
(x'/z', y'/z')
```

---

# 18. Complete Camera Transformation Pipeline

In real cameras the transformation happens in **three stages**.

### Step 1 — World to Camera Coordinates

Transforms the world point relative to the camera.

Matrix size:

```
4 × 4
```

---

### Step 2 — Perspective Projection

Projects the 3D point onto the image plane.

Matrix size:

```
3 × 4
```

---

### Step 3 — Camera to Pixel Coordinates

Converts coordinates into **pixel location** on the sensor.
Matrix size:

```
3 × 3
```

---

### Final Pipeline

```
3D world point
     ↓
World → Camera transform
     ↓
Perspective projection
     ↓
Camera → Pixel transform
     ↓
2D pixel location
```

---

# 19. Orthographic Projection

This is a **special case of perspective projection**.

### Definition

Orthographic projection assumes the camera is **infinitely far away**.

So all rays become **parallel**.

---

## Orthographic Projection Formula

Instead of dividing by z:

```
x' = x
y' = y
```


---

## Example

3D point:

```
P = (5,3,10)
```

Projection:

```
(5,3)
```

Depth does **not affect size**.

---

## Where Orthographic Projection Is Used

- Engineering drawings
- CAD designs
- Blueprints
- Some computer graphics

---

## Difference Between Perspective and Orthographic

|Feature|Perspective|Orthographic|
|---|---|---|
|Distance effect|Objects shrink with distance|Size constant|
|Realistic|Yes|No|
|Parallel lines|Meet at vanishing point|Remain parallel|

---

# 20. Building a Real Camera


But real cameras are different because:

- They need **more light**
- They need **sharper images**
- They must capture images **quickly**

Therefore real cameras use **lenses** instead of a simple pinhole.
Before lenses were invented, people used something called **Camera Obscura**.

---

# 21. Camera Obscura

## Definition

**Camera Obscura** means **“dark chamber”** in Latin.

It is a **dark room or box with a small hole** that projects an external scene onto a surface.

---

## Historical Discovery

The concept was known by many scientists:

|Scientist|Contribution|
|---|---|
|**Mozi (470–390 BCE)**|First description of pinhole imaging|
|**Aristotle (384–322 BCE)**|Observed light projection|
|**Leonardo da Vinci**|Explained camera obscura and used it for drawing|

Artists used camera obscura to **trace realistic drawings**.

---

## Working Principle

Steps:

1. Light from an object travels in straight lines.
2. It enters the dark room through a **small hole**.
3. Rays cross at the hole.
4. An **inverted image** forms on the opposite wall.

Example:

If a tree is outside the room, the opposite wall shows an **upside-down image of the tree**.

---

## Real Example

A modern artist named **Abelardo Morell** converted entire rooms into camera obscura systems.
The outside city view is projected onto the walls of the room.

---

# 22. Home-Made Pinhole Camera

You can build a simple camera using:

- A **box**
- **Aluminum foil**
- A **small hole**
- **Photographic film or paper**

Working:

```
Object → Light rays → Small hole → Image plane
```

But there is a major problem.

---

# 23. Why Pinhole Camera Images Are Blurry

Even though pinhole cameras reduce blur, images are still **not perfectly sharp**.

Reasons:

### 1. Very small hole → Less light

A small aperture allows **very little light**.
So images become:

- dark
- noisy
- long exposure required

---

### 2. Diffraction Effect

If the hole becomes extremely small, **light bends around the edges**.

This phenomenon is called:

### Diffraction

This causes the image to become **blurry again**.

So there is a **trade-off**:

|Aperture size|Effect|
|---|---|
|Large hole|blurry image|
|Very small hole|diffraction blur|
|Medium size|best image|

---

# 24. Solution – Refraction

To allow more light while keeping the image sharp, cameras use **lenses**.
Lenses work using the principle of:

---

## Snell’s Law

Refraction describes how light bends when passing between two materials.

The mathematical law is:

$n_1 \sin(\alpha_1) = n_2 \sin(\alpha_2)$  

Where:

|Symbol|Meaning|
|---|---|
|n₁|refractive index of first medium|
|n₂|refractive index of second medium|
|α₁|incident angle|
|α₂|refracted angle|

---

### Example

Light moving from **air to glass**:

- Light slows down
- It bends toward the normal

This bending allows lenses to **focus light**.

---

# 25. Adding a Lens

A **lens** collects light rays and focuses them onto the sensor.

Key properties:

1. Rays passing through the **center of the lens** go straight.
2. Parallel rays converge at a **focal point**.

---

## Focal Length

The distance between:

```
Lens → Focal point
```

is called the **focal length (f)**.

This value controls:

- zoom
- field of view
- perspective

---

## How a Lens Forms an Image

Steps:

1. Light rays come from the object.
2. The lens bends the rays.
3. Rays converge at a point.
4. A sharp image forms on the image plane.

---

# 26. Circle of Confusion

A point in the scene should ideally become a **single pixel** in the image.
But if the object is **not at the correct focus distance**, it forms a **small blurred circle**.

This is called:

### Circle of Confusion

Example:

When you focus on a person:

- the background becomes blurry
- because those points produce circles instead of sharp points

---

# 27. Thin Lens Equation

The focusing behavior of a lens follows the **thin lens equation**.

$\frac{1}{f} = \frac{1}{d_o} + \frac{1}{d_i}$  

Where:

|Symbol|Meaning|
|---|---|
|f|focal length|
|dₒ|object distance|
|dᵢ|image distance|

---

## Example

Suppose:

```
f = 50 mm
object distance = 1000 mm
```

Then the image will form at a specific distance behind the lens according to the formula.

The camera adjusts **lens position** to satisfy this equation.

This is how **autofocus works**.

---

# 28. Depth of Field (DOF)

## Definition

Depth of field is the **range of distances in which objects appear sharp**.

Example:

If you focus on a person:

- Some objects in front and behind are also sharp.
- This region is **depth of field**.

---

## Two Types of Depth of Field

### 1. Shallow Depth of Field

Only a small region is in focus.
Example:

- portrait photography
- background blur (bokeh)

---

### 2. Large Depth of Field

Most of the scene is sharp.
Example:

- landscape photography

---

# 29. Controlling Depth of Field

Depth of field depends mainly on **aperture size**.

|Aperture|Depth of Field|
|---|---|
|Large aperture|small DOF|
|Small aperture|large DOF|

---

### Example

|Aperture|Result|
|---|---|
|f/1.8|blurry background|
|f/16|almost everything sharp|

But smaller aperture means:

- less light enters
- longer exposure needed
---

# 30. Changing the Plane of Focus

Normally:

```
Lens plane
Image plane
Focus plane
```

are **parallel**.

But special lenses allow changing the focus plane.

---

# 31. Tilt-Shift Lens

A **tilt-shift lens** can tilt relative to the sensor.

This allows photographers to:

- control perspective
- adjust focus plane
- correct building distortion

---

## Scheimpflug Principle

When the lens is tilted:

The **focus plane**, **lens plane**, and **image plane** intersect at a line.

This allows focusing on **tilted surfaces**.

Example:

- photographing a long table
- photographing landscapes

---

## Fake Miniature Effect

Tilt-shift lenses are also used to create the **miniature toy effect**.

Real scenes look like **tiny models**.

This is commonly seen in:

- drone photography
- city timelapses

---

# 32. Field of View (FOV)

## Definition

**Field of View (FOV)** is the **amount of the scene captured by the camera**.

In simple terms:

> How much of the world the camera can see.

---

## Example

Imagine standing in front of a building.

|Lens type|What you see|
|---|---|
|Wide lens|Entire building|
|Telephoto lens|Only a small portion|

---

## Relation with Focal Length

FOV depends on **focal length (f)**.

Relationship:

|Focal Length|Field of View|
|---|---|
|Small focal length|Large FOV|
|Large focal length|Small FOV|

Example:

|Lens|FOV|
|---|---|
|18mm|very wide|
|50mm|normal|
|200mm|zoomed|

---

## Example With Camera Position

Two ways to photograph a car:

### Case 1: Wide Lens

- Camera close to car
- Large FOV
- Background looks stretched

### Case 2: Telephoto Lens

- Camera far from car
- Small FOV    
- Background looks compressed

---

# 33. Effect on Faces

Lens choice changes **face proportions**.

|Lens|Effect|
|---|---|
|Wide-angle|nose appears larger|
|Telephoto|face looks flatter|

This is why portrait photographers prefer **85mm–135mm lenses**.

---

# 34. Approximating an Affine Camera

When the camera is **very far from the object**, perspective effects become very small.

So we approximate the camera as:

### **Affine Camera**

This is similar to **orthographic projection**.

Properties:

- Parallel lines remain parallel
- Objects do not shrink significantly with distance

Used in:

- computer vision simplifications
- satellite imaging
---

# 35. Real Lens Problems (Lens Aberrations)

Real lenses are **not perfect**.
They introduce **optical errors** called:

### Lens Aberrations

---

# 36. Chromatic Aberration

## Definition

Different colors of light bend by **different amounts** when passing through a lens.

This causes **color fringing** near edges.

Example:

You may see:

- purple edges
- green edges

around high contrast objects.

---

## Why It Happens

Because each wavelength has a **different refractive index**.

Example:

|Color|Refraction|
|---|---|
|Red|bends less|
|Blue|bends more|

So colors do not focus at the same point.

---

## Where It Appears

Most visible near:

- image corners
- strong contrast edges

Example:

- tree branches against sky

---

# 37. Spherical Aberration

## Definition

Spherical lenses do not focus all light rays to the same point.

Rays near the edge of the lens focus **closer** than central rays.

Result:

- blurry image
- reduced sharpness

---

# 38. Vignetting

## Definition

Image corners appear **darker than the center**.

Causes:

1. Lens design
2. Obstruction of light rays
3. Large aperture

Example:

Old photographs often show **dark corners**.

---

# 39. Radial Distortion

## Definition

Straight lines appear **curved** in images.

Types:

### 1. Barrel Distortion

Lines curve **outward**.

Common in:

- wide angle lenses
- action cameras

---

### 2. Pincushion Distortion

Lines curve **inward**.

Common in:

- telephoto lenses

---

Example:

A grid may appear like:

```
Barrel distortion:

| )   ( |
| )   ( |
| )   ( |
```

---

# 40. Digital Camera

Modern cameras replace **film with electronic sensors**.

A digital camera contains:

1. **Lens**
2. **Image sensor**
3. **Processor**
4. **Memory storage**

---

## How Digital Sensors Work

Each sensor contains a **grid of pixels**.

Each pixel is a **light-sensitive diode**.

Process:

1. Light hits the pixel.
2. Photons generate electrons.
3. Charge is measured.
4. Converted to digital value.

---

# 41. Types of Image Sensors

Two main types:

1. **CCD**
2. **CMOS**

---

# 42. CCD Sensor (Charge Coupled Device)

Working:

- Electrical charge moves across the chip
- Collected at one corner
- Converted to digital value

---

## Advantages

|Advantage|Explanation|
|---|---|
|Low noise|cleaner images|
|High sensitivity|good in low light|
|High image quality|professional cameras|

---

## Disadvantages

|Problem|Explanation|
|---|---|
|High power consumption|drains battery|
|Expensive|manufacturing cost|
|Slow readout|slower processing|

---

# 43. CMOS Sensor

CMOS sensors work differently.

Each pixel contains **its own amplifier and circuitry**.

---

## Advantages

|Advantage|Explanation|
|---|---|
|Low power|good for mobile phones|
|Cheap manufacturing|mass production|
|Fast readout|good for video|

---

## Disadvantages

|Problem|Explanation|
|---|---|
|Higher noise|slightly grainy images|
|Lower sensitivity|less effective in low light|

---

## Summary Comparison

|Feature|CCD|CMOS|
|---|---|---|
|Cost|high|low|
|Power|high|low|
|Noise|low|higher|
|Speed|slow|fast|

Today most cameras use **CMOS sensors**.

---

# 44. Color Sensing in Cameras

Camera sensors detect **light intensity only**, not color.

So we need a way to capture color.

---

# 45. Color Filter Array (Bayer Pattern)

Most cameras use a **Bayer filter**.

Pattern:

```
G R
B G
```

Where:

- R = Red
- G = Green
- B = Blue

There are **more green pixels** because the human eye is more sensitive to green light.

---

# 46. Demosaicing

Since each pixel captures **only one color**, the missing colors must be estimated.

This process is called:

### **Demosaicing**

Example:

If a pixel captures **red**, the camera estimates **green and blue** using neighboring pixels.

---

# 47. Color Moiré Problem

Sometimes fine patterns confuse the sensor.

Example:

- striped fabrics
- building grids

The sensor may misinterpret patterns as **false colors**.

This effect is called:

### Color Moiré

---

# 48. Alternative Color Sensor – Prism

Some professional cameras use a **prism system**.

Working:

1. Prism splits light into **red, green, blue**.
2. Each color goes to a **separate sensor**.

Advantages:

- accurate colors
- no demosaicing needed

Disadvantages:

- expensive
- complex design
---

# 49. Foveon X3 Sensor

Another technology uses **three layers in silicon**.

Each layer captures:

- red
- green
- blue

Because different colors penetrate silicon at different depths.

Advantage:

- very accurate color reproduction.

---

# 50. Problems in Digital Cameras

Several issues can occur.

---

## 1. Noise

Occurs in **low light**.

Higher ISO increases:

- brightness
- noise

Tradeoff:

```
High ISO → more noise
Low ISO → darker image
```

---

## 2. Stuck Pixels

Some pixels may become permanently bright or dark.

---

## 3. Resolution vs Megapixels

More megapixels do **not always mean better images**.

Higher resolution requires:

- better lenses
- better sensors

---

## 4. RAW vs Compressed Images

|Format|Advantage|
|---|---|
|RAW|highest quality|
|JPEG|smaller file size|

---

## 5. Blooming

When a pixel receives too much light, charge may overflow to nearby pixels.

Result:

- bright streaks around light sources.

---

# 51. Historical Timeline of Cameras

Important developments:

|Year|Development|
|---|---|
|470 BCE|Mozi describes pinhole imaging|
|1500s|Camera obscura used by artists|
|1822|First photograph|
|1889|Photographic film invented|
|1895|Cinema invented|
|1908|Color photography|
|1981|First CCD consumer camera|
|1990|First fully digital camera|

---

# Summary

---

### 1. Pinhole Projection Model

A **pinhole projection model** is a simple camera model where light passes through a **tiny hole (pinhole)** and forms an **inverted image on the image plane**. It represents how a **3D scene is projected onto a 2D image**.

---

### 2. Vanishing Points and Vanishing Lines

- **Vanishing Point:** The point in an image where **parallel lines appear to meet** due to perspective (e.g., railway tracks meeting at the horizon).
- **Vanishing Line:** A line formed by **multiple vanishing points of parallel planes**, usually the **horizon line**.

---

### 3. Orthographic Projection

**Orthographic projection** is a type of projection where **parallel rays project the object onto the image plane**.  
Objects **do not shrink with distance**, and parallel lines remain parallel.

---

### 4. Approximating Orthographic Projection

Orthographic projection can be approximated when the **camera is very far from the object** compared to the object size, making perspective effects negligible.

---

### 5. Lenses

A **lens** is an optical component that **bends (refracts) light rays** and focuses them onto the image sensor or film to produce a **sharp image**.

---

### 6. Why Do We Need Lenses?

Lenses are needed because:

- Pinhole cameras allow **very little light**.
- Lenses **collect more light** and produce **brighter and sharper images**.

---

### 7. What Controls Depth of Field?

**Aperture size** controls depth of field.

- **Large aperture → small depth of field** (blurred background)
- **Small aperture → large depth of field** (more scene in focus)

---

### 8. What Controls Field of View?

**Focal length of the lens** controls field of view.

- **Small focal length → wide field of view**
- **Large focal length → narrow field of view**

---

### 9. Kinds of Lens Aberrations

Common lens aberrations include:

- **Chromatic aberration** – color fringes due to different wavelengths.
- **Spherical aberration** – rays focus at different points causing blur.
- **Radial distortion** – straight lines appear curved (barrel or pincushion).
- **Vignetting** – image corners appear darker.

---

### 10. Digital Cameras

Digital cameras capture images using **electronic sensors** that convert light into **digital signals**.

---

### 11. Two Major Sensor Technologies

The two main image sensor types are:

1. **CCD (Charge Coupled Device)**
2. **CMOS (Complementary Metal Oxide Semiconductor)**

---

### 12. Types of Color Sensors

Different types of color sensing methods include:

1. **Bayer color filter array** (most common)
2. **Prism-based sensors** (separate RGB sensors)
3. **Foveon X3 sensor** (three-layer color detection)

---
