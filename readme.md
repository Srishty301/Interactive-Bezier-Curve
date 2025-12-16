# Interactive Bézier Rope with Physics & Geometry Visualization

## 1. Overview

This project implements an **interactive cubic Bézier curve** that behaves like a **springy rope** in real time.  
The curve responds smoothly to user input using a **spring–damper physics model** and visualizes important geometric properties such as **tangents, normals, and curvature**.

The implementation is done **entirely from scratch** using **HTML Canvas and JavaScript**, without relying on any prebuilt Bézier, physics, or animation libraries.

---

## 2. Bézier Curve Mathematics

A **cubic Bézier curve** is defined using four control points:

- **\( \mathbf{P}_0, \mathbf{P}_3 \)** – fixed endpoints  
- **\( \mathbf{P}_1, \mathbf{P}_2 \)** – dynamic control points  

### Curve Equation

\[
\mathbf{B}(t)
=
(1 - t)^3 \mathbf{P}_0
+ 3(1 - t)^2 t \mathbf{P}_1
+ 3(1 - t)t^2 \mathbf{P}_2
+ t^3 \mathbf{P}_3
\]

where:

\[
t \in [0, 1]
\]

The curve is rendered by sampling the equation at small intervals of  
\( \Delta t \approx 0.01 \).

---

## 3. Tangent and Normal Vectors (Frenet Frame)

### 3.1 Tangent Vector

The tangent at any point on the curve is computed using the **first derivative**:

\[
\mathbf{B}'(t)
=
3(1 - t)^2 (\mathbf{P}_1 - \mathbf{P}_0)
+ 6(1 - t)t (\mathbf{P}_2 - \mathbf{P}_1)
+ 3t^2 (\mathbf{P}_3 - \mathbf{P}_2)
\]

The **unit tangent vector** is:

\[
\mathbf{T}(t)
=
\frac{\mathbf{B}'(t)}{\left\| \mathbf{B}'(t) \right\|}
\]

---

### 3.2 Normal Vector

The **normal vector** is defined as a perpendicular to the tangent:

\[
\mathbf{N}(t)
=
\begin{pmatrix}
- T_y \\
\;\; T_x
\end{pmatrix}
\]

where:

\[
\mathbf{T}(t)
=
\begin{pmatrix}
T_x \\
T_y
\end{pmatrix}
\]

Together, the tangent and normal vectors form the **local Frenet frame**, describing the curve’s instantaneous orientation.

---

## 4. Curvature Visualization

Curvature is estimated numerically by measuring the change in tangent direction between nearby points:

\[
\kappa(t)
\approx
\left\|
\mathbf{T}(t + \Delta t)
-
\mathbf{T}(t)
\right\|
\]

### Curvature-Based Coloring

- **Low curvature** → cyan  
- **High curvature** → warmer colors  

This highlights regions where the curve bends more sharply.

---

## 5. Spring–Damper Physics Model

The dynamic control points \( \mathbf{P}_1 \) and \( \mathbf{P}_2 \) follow target positions using a **spring–damper system**.

### Equation of Motion

\[
\mathbf{a}
=
- k(\mathbf{x} - \mathbf{x}_{\text{target}})
- c \mathbf{v}
\]

where:

- \( \mathbf{x} \) — current position  
- \( \mathbf{x}_{\text{target}} \) — target position  
- \( \mathbf{v} \) — velocity  
- \( k \) — spring stiffness  
- \( c \) — damping coefficient  

### Per-Frame Integration

Each animation frame performs:

1. **Velocity update**
\[
\mathbf{v}_{t+1} = \mathbf{v}_t + \mathbf{a} \, \Delta t
\]

2. **Position update**
\[
\mathbf{x}_{t+1} = \mathbf{x}_t + \mathbf{v}_{t+1} \, \Delta t
\]

This produces smooth, realistic rope-like motion.

---

## 6. Interaction Model

- Mouse movement defines target positions for \( \mathbf{P}_1 \) and \( \mathbf{P}_2 \)
- Control points respond with elastic lag
- Endpoints \( \mathbf{P}_0 \) and \( \mathbf{P}_3 \) remain fixed

The simulation runs at approximately **60 FPS** using:

```js
requestAnimationFrame()
