# Finite Element Stokes Solver for Laminar Pipe Flow

The aim of this project is to compute the laminar velocity profile in a circular pipe at low Reynold's number using the __finite element method__.
    
We assume that the flow is:

1) Steady,
2) Incompressible,
3) Fully developed,
4) in the low Reynold's numbers regime.

ToDo: Insert picture here.

Under such assumptions:

1) Only the axial velocity, $w(x,y)$ is nonzero,
2) The pressure gradient, $\frac{dp}{dz}$, is constant.

The strong form of the axial momentum equation on the cross-section $\Omega$ is:
		$$-\mu\nabla^2w=\frac{dp}{dz}
,$$

where $\mu$ is the __dynamic viscosity__ and $\frac{dp}{dz}$ is the __constant axial pressure gradient__ driving the flow.

Furthermore, we are assuming a __no-slip__ condition at the wall 

$$w=0\quad\text{on }\partial\Omega$$

Let $$f=-\frac{1}{\mu}\frac{dp}{dz}=const,

$$
be the __normalized pressure gradient. 


The weak form of equation can be derived to be: 
$$\int_\Omega \nabla w \cdot \nabla v  d\Omega = \int_\Omega f v d\Omega \quad \forall v \in V_0$$

with $V_0 = H_0^1(\Omega)$ (zero on boundary → no-slip).

We seek the axial velocity, $w \in V_0$ that satisfies the above equation.

The resulting solution for $w$ will be compared to the analytical __Hagen–Poiseuille__ velocity profile.