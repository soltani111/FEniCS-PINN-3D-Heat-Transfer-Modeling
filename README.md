# FEniCS-PINN-3D-Heat-Transfer-Modeling

# Comparative Analysis of 3D Heat Transfer Modeling Using FEniCS and Physics-Informed Neural Networks (PINNs)

## Introduction

In this study, first the 3D heat transfer problem is solved with FEniCS. Afterwards, the temperature data on the domain is used as ground truth data for a Physics-Informed Neural Network (PINN). A comparison is made between the PINN and FEniCS data to evaluate the accuracy of the PINN model.

## Geometry Model

The 3D geometry of a fin is considered in this problem. Boundary conditions in this setup are:

- Constant wall temperature \(T = 400 \, \text{K}\) at \(x = 0\)
- \(T = 350 \, \text{K}\) at \(x = 100\)
- \(T = 375 \, \text{K}\) at \(y = 60\)
- Constant heat flux \(q'' = 250 \, \text{W/m}^2\) at \(y = 0\)
- Convection boundary condition \(h = 40 \, \text{W/m}^2\cdot\text{K}\), \(T_\infty = 300 \, \text{K}\) at other boundaries.

## FEniCS Solver

For two-dimensional steady-state conditions with no generation and constant thermal conductivity, the governing equation of this model is:

\[
\nabla^2 T = 0
\]

In the two-dimensional model, the equation becomes:

\[
\frac{\partial^2 T}{\partial x^2} + \frac{\partial^2 T}{\partial y^2} + \frac{\partial^2 T}{\partial z^2} = 0
\]

FEniCS is based on the finite element method, which is a general and efficient mathematical machinery for the numerical solution of PDEs. The starting point for the finite element methods is a PDE expressed in variational form. To obtain the variational form of the equation, first multiply the equation by the test function \(v\) and integrate over the boundary (\(\Omega\)):

\[
\int_\Omega \nabla^2 T \, dx = 0 \quad (x \in \Omega)
\]

Expanding the equation gives:

\[
-\int_\Omega \nabla T \cdot \nabla v \, dx + \int_{\partial \Omega} \frac{\partial T}{\partial n} v \, dx = 0 \quad (x \in \Omega)
\]

On the convection boundary condition, the right-hand term of the equation becomes:

\[
\int_{\partial \Omega} \frac{\partial T}{\partial n} v \, dx = -\int_{\partial \Omega} h(T - T_\infty) v \, dx - \int_{\partial \Omega} q'' v \, dx
\]

The variational form of the equation is:

\[
a(T, v) = L(T, v)
\]

\[
a(T, v) = \int_\Omega \nabla T \cdot \nabla v \, dx + \int_{\partial \Omega} hTv \, dx
\]

\[
L(T, v) = -\int_{\partial \Omega} q'' v \, dx + \int_{\partial \Omega} h T_\infty v \, dx
\]

## PINN Inverse Problem

PINNs directly embed physical laws within the loss function of neural networks. By minimizing the loss function, this approach allows the output variables to automatically satisfy physical equations. In this study, we consider an inverse problem with FEniCS ground truth data. Implementation of the PINN with these data obtains the temperature distribution over the domain.

In this work, we first apply a function to the input data that takes \(x\), \(y\), and \(z\) of the input point and gives an array representing the distance of each point proportional to the input point. The formulation of this function is:

\[
B_x = e^{-\left(\frac{x - x_0}{L_0}\right)^2}
\]

\[
B_y = e^{-\left(\frac{y - y_0}{L_0}\right)^2}
\]

\[
B_z = e^{-\left(\frac{z - z_0}{L_0}\right)^2}
\]

\[
B = \frac{B_x + B_y + B_z}{3}
\]

For each point, \(B\) is calculated and fed into a multi-layer perceptron (MLP) with \(N\) input neurons (\(N\): number of points in the entire domain), six hidden layers with \(N_{45}\), \(N_{81}\), \(N_{125}\), \(N_{125}\), \(N_{125}\), \(N_{125}\) neurons respectively, and an output layer with one neuron. Equation [2] is used as the loss function of PINN.

The MLP gets \(x\),
