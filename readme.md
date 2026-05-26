# Finite Element Stokes Solver for Laminar Pipe Flow

The aim of this project is to compute the laminar velocity profile in a circular pipe at low Reynold's number using the __finite element method__.

The FEM simulation is developed in python using the "scikit-fem" library:

https://scikit-fem.readthedocs.io/en/latest/index.html

The code is provided in the _notebook_ subfolder of this repository, in the jupyter notebook _flow.ipynb_. It is assumed that the user has a standard Anaconda installation.

## Assumptions

We assume that the flow is:

1) Steady,
2) Incompressible,
3) Fully developed,
4) in the low Reynold's numbers regime.

The pipe is oriented along the $z$-axis and $w(x,y)$ denotes the __axial velocity__, that is the velocity in the z-direction, at a point $(x,y)$ on a crosssection of the pipe.

Under these assumptions:

1) Only the axial velocity, $w(x,y)$ is nonzero, meaning that the no fluid motion occurs in the radial direction ( sideways ).
2) The pressure gradient, $\frac{dp}{dz}$ is constant.

Furthermore, we assume a __no-slip__ condition at the wall 

$$w=0\quad\text{on }\partial\Omega$$,

where $\Omega$ is the interior of the crosssection and $\partial\Omega$ denotes its boundary.

## 1. Derivation of the weak form

The strong form of the axial momentum equation on the cross-section $\Omega$ is:

$$-\mu\nabla^2w=\frac{dp}{dz} \qquad (1)$$

where $\mu$ is the __dynamic viscosity__ and $\frac{dp}{dz}$ is the __constant axial pressure gradient__ driving the flow.

Let 

$$f=-\frac{1}{\mu}\frac{dp}{dz}=const$$

, be the __normalized pressure gradient__. 


The weak form of equation (1) is obtained as: 

$$\int_\Omega \nabla w \cdot \nabla v \hspace{2pt} d\Omega = \int_\Omega f v \hspace{3pt} d\Omega \quad \forall v \in V_0\qquad (2)$$

with $V_0 = H_0^1(\Omega)$, the __Sobolov space__ of test functions that vanish on $\partial \Omega$ (corresponding to the no‑slip condition).

We seek the axial velocity $w \in V_0$, that satisfies the weak formulation above.

The resulting numerical solution for $w$ will be compared to the analytical __Hagen–Poiseuille__ velocity profile.

### 2. Discretization idea

A 2D triangular mesh is generated on the pipe cross‑section Ω. 

<img width="400" alt="Pasted image 20260507111542" src="figures/image.png" />

We use **piecewise linear** P1 **finite elements**, so the approximate solution is written as 

$$w_h(x,y) = \sum_{j=1}^{N} w_j \phi_j(x,y)$$, 

where $\phi_j$ are the __nodal basis functions__ associated with the mesh vertices.

The weak form above, (2), leads to the linear system: 

$$K \mathbf{w} = \mathbf{f}$$ 

, where

$$K_{ij} = \int_\Omega \nabla \phi_i \cdot \nabla \phi_j \hspace{3pt}d\Omega$$

is called the __stiffness matrix__ and has the properties of being symmetric and positive definite and:

 $$f_i = \int_\Omega f \phi_i  \hspace{3pt} d\Omega$$

is called the __load vector__.

# Results
figures/Pasted image 20260520222506.png
The following plot made in the accompanying code verifies that the velocity is at its maximum in the center of the pipe and deteriorates towards the wall, becoming zero at the wall in consistence with the Dirichlet no-slip boundary condition.
<img width="400" alt="Pasted image 20260507111542" src="figures/Pasted image 20260520222506.png" />

Plotting the radial velocity, $w$, gives the following plot:

<img width="400" alt="Pasted image 20260507111542" src="figures/Pasted image 20260521130354.png" />

¨From this plot it can seen that velocity it is a maximum in the center of the pipe and goes to zero when moving towards to wall in a manner that resembles a parabolic curve.

The maximum is, from python, $\omega_{max}=0.247 m/s$. 

The hagen-Poiseuille equations, as applied to these circumstances, gives:

𝑟
2
.
