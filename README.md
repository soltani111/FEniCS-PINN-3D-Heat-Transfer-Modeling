# 3D Heat Transfer Modeling: FEniCS vs. Physics-Informed Neural Networks (PINNs)

## Introduction

In this study, the 3D heat transfer problem was first solved using FEniCS. The temperature data obtained from the domain was then used as ground truth data for a Physics-Informed Neural Network (PINN). A comparison was made between the PINN and FEniCS data to assess the accuracy of the PINN model.

## Geometry Model

The 3D geometry of a fin was considered in this problem. The boundary conditions in this setup are:
- Constant Wall Temperature \(T = 400\, \${K}$\) at \(x = 0\)
- \(T = 350\, \${K}$\) at \(x = 100\)
- \(T = 375\, \${K}$\) at \(y = 60\)
- Constant Heat Flux \(q'' = 250\, \${W/m}^2$\) at \(y = 0\)
- Convection boundary condition \(h = 40\, \${W/(m}^2\cdot \{K)}$\), \(T_\infty = 300\, \text{K}\) at other boundaries.

## FEniCS Solver

For two-dimensional, steady-state conditions with no generation and constant thermal conductivity, the governing equation of this model is:

\[
\nabla^2 T = 0
\]

In the two-dimensional model, equation [1] becomes:

\[
\frac{\partial^2 T}{\partial x^2} + \frac{\partial^2 T}{\partial y^2} + \frac{\partial^2 T}{\partial z^2} = 0
\]

FEniCS is based on the finite element method, a general and efficient mathematical machinery for the numerical solution of PDEs. The starting point for the finite element method is a PDE expressed in variational form. To obtain the variational form of equation [2], first multiply equation [2] by the test function \(v\) and integrate over the boundary (\(\Omega\)):

\[
\int_\Omega \nabla^2 T \, dx = 0 \quad (x \in \Omega)
\]

Expanding equation [3]:

\[
-\int_\Omega \nabla T \cdot \nabla v \, dx + \int_{\partial \Omega} \frac{\partial T}{\partial n} v \, dx = 0 \quad (x \in \Omega)
\]

On the convection boundary condition, the right-hand term of equation [4] becomes:

\[
\int_{\partial \Omega} \frac{\partial T}{\partial n} v \, dx = -\int_{\partial \Omega} h(T - T_\infty) v \, dx - \int_{\partial \Omega} q'' v \, dx
\]

From equations [4] and [5], the variational form of equation [2] is:

\[
a(T, v) = L(T, v)
\]

\[
a(T, v) = \int_\Omega \nabla T \cdot \nabla v \, dx + \int_{\partial \Omega} hTv \, dx
\]

\[
L(T, v) = -\int_{\partial \Omega} q'' v \, dx + \int_{\partial \Omega} h T_\infty v
