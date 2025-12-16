# Interactive Bézier Rope with Physics & Geometry Visualization

## 1. Overview

This project implements an **interactive cubic Bézier curve** that behaves like a **springy rope** in real time.  
The curve responds smoothly to user input using a **spring–damper physics model** and visualizes important geometric properties such as **tangents, normals, and curvature**.

The implementation is done **entirely from scratch** using HTML Canvas and JavaScript, without relying on any prebuilt Bézier, physics, or animation libraries.

---

## 2. Bézier Curve Mathematics

A **cubic Bézier curve** is defined using four control points:

- **P₀, P₃** – fixed endpoints  
- **P₁, P₂** – dynamic control points  

The curve equation is:

\[
B(t) = (1−t)³P₀ + 3(1−t)²tP₁ + 3(1−t)t²P₂ + t³P₃
\]

where t∈[0,1]

The curve is rendered by sampling the equation at small intervals of \( t \) (Δt ≈ 0.01).

---

## 3. Tangent and Normal Vectors (Frenet Frame)

### Tangent Vector

The tangent at any point on the curve is computed using the first derivative:

\[
B'(t) = 3(1−t)²(P₁−P₀) + 6(1−t)t(P₂−P₁) + 3t²(P₃−P₂)
\]

The derivative is normalized and drawn along the curve.

### Normal Vector

The **normal vector** is computed as a perpendicular to the tangent:

\[
N(t)=(−Ty​Tx​​)
\]

Together, the tangent and normal vectors form the **local Frenet frame**, describing the curve’s local orientation.

---

## 4. Curvature Visualization

Curvature is estimated numerically by measuring the change in tangent direction between nearby points:

\[
κ(t)≈∥T(t+Δt)−T(t)∥
\]

The curve is color-mapped based on curvature magnitude:
- **Low curvature** → cyan
- **High curvature** → warmer colors

This highlights regions where the curve bends more sharply.

---

## 5. Spring–Damper Physics Model

The dynamic control points (P₁ and P₂) follow a target position using a **spring–damper system**:

\[
a=−k(x−xtarget​)−cv
\]

Where:
x — current position

𝑥
𝑡
𝑎
𝑟
𝑔
𝑒
𝑡
x
target
	​

 — target position

𝑣
v — velocity

𝑘
k — spring stiffness

𝑐
c — damping coefficient
- \( k \) is the stiffness constant
- \( c \) is the damping coefficient
- \( v \) is velocity

Each frame:
1. Acceleration is computed
2. Velocity is updated
3. Position is updated

This produces smooth, realistic rope-like motion.

---

## 6. Interaction Model

- Mouse movement defines target positions for P₁ and P₂
- Control points respond with physical lag
- Endpoints remain fixed

The simulation runs at approximately **60 FPS** using `requestAnimationFrame`.

---

## 7. Rendering Features

The visualization includes:
- Cubic Bézier curve
- Control polygon (dashed)
- Control points
- Tangent vectors (orange)
- Normal vectors (blue)
- Curvature-based coloring
- Subtle 2D reference grid

All rendering is performed using the HTML Canvas API.

---


## 9. Conclusion

This project demonstrates a complete understanding of **Bézier curve mathematics**, **differential geometry**, and **physics-based motion**, combined with real-time interactive rendering. The additional visualizations provide deeper insight into the geometric and dynamic behavior of the curve.

---

**Author:** Srishty

