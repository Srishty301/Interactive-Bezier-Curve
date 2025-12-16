# Interactive Bézier Rope with Physics & Geometry Visualization

## 1. Overview

This project implements an interactive **cubic Bézier curve** that behaves like a **springy rope** in real time.  
The curve responds smoothly to user input using a **spring–damper physics model** and visualizes important geometric properties such as **tangents, normals, and curvature**.

The implementation is done **entirely from scratch** using **HTML Canvas and JavaScript**, without relying on any prebuilt Bézier, physics, or animation libraries.

---

## 2. Bézier Curve Mathematics

A cubic Bézier curve is defined using four control points:

- P0, P3 – fixed endpoints  
- P1, P2 – dynamic control points  

### Curve Equation

B(t) = (1 − t)³ P0  
      + 3(1 − t)² t P1  
      + 3(1 − t) t² P2  
      + t³ P3  

where:

t ∈ [0, 1]

The curve is rendered by sampling the equation at small intervals of  
Δt ≈ 0.01.

---

## 3. Tangent and Normal Vectors (Frenet Frame)

### Tangent Vector

The tangent at any point on the curve is computed using the first derivative:

B′(t) = 3(1 − t)² (P1 − P0)  
       + 6(1 − t) t (P2 − P1)  
       + 3 t² (P3 − P2)

The unit tangent vector is:

T(t) = B′(t) / ||B′(t)||

---

### Normal Vector

The normal vector is perpendicular to the tangent:

N(t) = ( −Ty , Tx )

Together, the tangent and normal vectors form the **local Frenet frame**, describing the curve’s local orientation.

---

## 4. Curvature Visualization

Curvature is estimated numerically by measuring the change in tangent direction between nearby points:

κ(t) ≈ || T(t + Δt) − T(t) ||

### Curvature-Based Coloring

- Low curvature → cyan  
- High curvature → warmer colors  

This highlights regions where the curve bends more sharply.

---

## 5. Spring–Damper Physics Model

The dynamic control points P1 and P2 follow a target position using a **spring–damper system**.

### Equation of Motion

a = −k (x − x_target) − c v

where:

x        → current position  
x_target → target position  
v        → velocity  
k        → spring stiffness  
c        → damping coefficient  

### Per-Frame Update

Each animation frame performs:

1. Acceleration computation  
2. Velocity update  
3. Position update  

This produces smooth, realistic rope-like motion.

---

## 6. Interaction Model

- Mouse movement defines target positions for P1 and P2  
- Control points respond with elastic lag  
- Endpoints P0 and P3 remain fixed  

The simulation runs at approximately **60 FPS** using:

```js
requestAnimationFrame()
```
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

All rendering is performed using the **HTML Canvas API**.

---

## 9. Conclusion

This project demonstrates a complete understanding of **Bézier curve mathematics**, **differential geometry**, and **physics-based motion**, combined with real-time interactive rendering. The additional visualizations provide deeper insight into the geometric and dynamic behavior of the curve.

---

**Author:** Srishty
