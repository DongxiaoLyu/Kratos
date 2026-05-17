# Review of Thermo- Mechanical Coupling Problem

## Introduction
This review presents a simplified overview of current research and engineering applications of Thermo-Mechanical Coupling (TMC) problems. The objective is to classify common thermo-mechanical coupling scenarios according to their coupling types, physical mechanisms, and linear or nonlinear characteristics. In addition, the general numerical solution procedures for each category are summarized, and representative benchmark test models are recommended for computational implementation and verification.

Thermo-mechanical coupling problems arise when thermal fields and mechanical fields interact with each other. Temperature variations may induce thermal expansion, thermal stress, material degradation, or phase transformation, while mechanical processes such as plastic deformation, friction, and crack propagation may generate heat. Such interactions are widely encountered in aerospace engineering, additive manufacturing, welding, metal forming, electronic packaging, energy systems, and geomechanics.

## Classification of Thermo-Mechanical Coupling Problems

### Classification Criteria
#### Coupling Type
1. One-way coupling (weak coupling)
   
   Temperature impact structual mechanics, however, structural deformation does not influent thermal field.(e.g. Thermal expansion, Thermal Stress, Temperature-Dependent Material Behavior)
2. Fully coupling (strong coupling)
   
   Thermal field and mechanical field impact each other simultaneously. (Plastic deformation generating heat, Friction heat, Thermal transform path change due to large deformation)
#### Physical Mechanism
1. Thermoelasticity

   Temperatual change causes elastic deformation. (Small deformation, linear, recovable)
   
2. Thermoviscoplasticity
   
   Temperatual change causes plastic deformation and material hardening.

3. Thermo-contact
   
   Thermal transform or friction heat generation at contact area.

4. Thermo-fracture
   
   Thermal crack propagation


5. Thermo-phase transformation

   Temperature change causes material phase change. (e.g. melt, solidification)

6. Thermo-fluid-structure interaction

   Thermal field, fluid field, and structural field couple.

#### Mathematic Model
1. Steady
2. Transient

#### Linear/non linear
1. Linear coupling

   Small deformation, constant material properties, linear heat conduction.

2. Non linear coupling

   Large deformation, temperature relied materials, contact, plasticity, phase transform.


### Problem Classification
#### Linear thermoelasticity (Weak coupling)

1. Charateristics:
   - Weak coupling
   - Linear
   - Steady

2. Problem Statement:

   We consider the case of a rectangular 2D domain of dimensions $L×H$ fully clamped on both lateral sides and subjected to a self-weight loading. The bottom side is subjected to a uniform temperature increase of $\Delta T = +100 °C$ while the top and lateral boundaries remain at the initial temperature $T_0$. The geometry and boundary regions are first defined.


3. Governing equations:

   The problem consists of a steady-state thermal analysis followed by a
   linear thermoelastic mechanical analysis.

   Steady-state Heat Conduction:

   $$
   \nabla \cdot (k \nabla T) = 0
   \quad \text{in } \Omega
   $$
   
   $$k = \mathrm{const.}$$
   
   with boundary

   $$
   \partial \Omega = \Gamma_u \cup \Gamma_t \cup \Gamma_T .
   $$

   Under the assumption of infinitesimal deformation, the strain tensor is

   
   $$\boldsymbol{\varepsilon}(\mathbf{u}) = \frac{1}{2} \left(\nabla \mathbf{u} + \nabla \mathbf{u}^{T} \right)$$
   

   where

   $$
   \mathbf{u} =
   \begin{bmatrix}
   u_x \\
   u_y
   \end{bmatrix}
   $$ 

   is the displacement vector field.

   Thermal Strain：

   The thermal strain tensor is given by

   $$\boldsymbol{\varepsilon}^{th} = \alpha (T-T_0)\mathbf{I}$$
   
   where

   - $\alpha$ is the coefficient of thermal expansion
   - $T_0$ is the reference temperature
   - $\mathbf{I}$ is the identity tensor

   Constitutive Equation：

   The thermoelastic constitutive relation is

   
   $$\boldsymbol{\sigma}
   =
   \mathbb{C}
   :
   \left(
   \boldsymbol{\varepsilon}
   -
   \boldsymbol{\varepsilon}^{th}
   \right)$$
   

   where

   - $\boldsymbol{\sigma}$ is the Cauchy stress tensor
   - $\mathbb{C}$ is the elasticity tensor

   For isotropic linear elasticity:

   $$\boldsymbol{\sigma}
   =
   \lambda
   \, \mathrm{tr}(\boldsymbol{\varepsilon})
   \mathbf{I}
   +
   2\mu
   \boldsymbol{\varepsilon}
   -
   \alpha (3\lambda + 2\mu)(T-T_0)\mathbf{I}$$

   where $\lambda,\mu$ are the Lamé constants:

   $$\mu = \frac{E}{2(1+\nu)}$$
   $$\lambda = \frac{E\nu}{(1+\nu)(1-2\nu)}$$

   with

   - $E$: Young's modulus
   - $\nu$: Poisson ratio

4. Solving procedures:
   1. Solve the thermal conduction problem to obtain the temperature field $T(x,y)$.
   2. Use that temperature field as a load in the mechanical elasticity problem

#### Thermo-elastic evolution problem (weak coupling)

1. Charateristics:
   - weak coupling
   - Linear
   - Transient thermoelastic problem

2. Problem Statement:
   
   We consider a transient thermoelastic evolution problem in which both thermo-mechanical fields are coupled, we will however assume that the evolution is quasi-static and will neglect inertial effects. Note that a staggered approach could also have been adopted in which one field is calculated first (say the temperature for instance) using predicted values of the other field and similarly for the other field in a second step.

   The problem consists of a rectangular plate under self-weight. The material is homogeneous and isotropic aluminium. Linear thermoelasticity is formulated around a reference temperature of $T_0=293K$.The left boundary of the plate is fully fixed in all displacement directions and subjected to a uniform temperature increase of $\Delta T$. The remaining boundaries are assumed to be traction-free and thermally insulated.
   
   This setup induces thermal expansion constrained at the left edge, resulting in thermal stress development within the structure.

3. Governing Equation

   The problem consists of a transient thermal analysis followed by a
   linear thermoelastic mechanical analysis.

   Transient heat equation (heat diffusion):

   $$
   \rho c \frac{\partial T}{\partial t} = \nabla \cdot (k\nabla T)
   $$
   
   $$k = \mathrm{const.}$$
   
   with boundary

   $$
   T = T_0 \ \mathrm{on} \ \Gamma_L \\
   -k \nabla T \cdot n = 0 \ \mathrm{on} \ \Gamma_T \cup \Gamma_B \cup \Gamma_R
   $$

   Under the assumption of infinitesimal deformation, the strain tensor is

   
   $$\boldsymbol{\varepsilon}(\mathbf{u}) = \frac{1}{2} \left(\nabla \mathbf{u} + \nabla \mathbf{u}^{T} \right)$$
   

   where

   $$
   \mathbf{u} =
   \begin{bmatrix}
   u_x \\
   u_y
   \end{bmatrix}
   $$ 

   is the displacement vector field.

   Thermal Strain：

   The thermal strain tensor is given by

   $$\boldsymbol{\varepsilon}^{th} = \alpha (T-T_0)\mathbf{I}$$
   
   where

   - $\alpha$ is the coefficient of thermal expansion
   - $T_0$ is the reference temperature
   - $\mathbf{I}$ is the identity tensor

   Constitutive Equation：

   The thermoelastic constitutive relation is

   
   $$\boldsymbol{\sigma}
   =
   \mathbb{C}
   :
   \left(
   \boldsymbol{\varepsilon}
   -
   \boldsymbol{\varepsilon}^{th}
   \right)$$
   

   where

   - $\boldsymbol{\sigma}$ is the Cauchy stress tensor
   - $\mathbb{C}$ is the elasticity tensor

   For isotropic linear elasticity:

   $$\boldsymbol{\sigma}
   =
   \lambda
   \, \mathrm{tr}(\boldsymbol{\varepsilon})
   \mathbf{I}
   +
   2\mu
   \boldsymbol{\varepsilon}
   -
   \alpha (3\lambda + 2\mu)(T-T_0)\mathbf{I}$$

   where $\lambda,\mu$ are the Lamé constants:

   $$\mu = \frac{E}{2(1+\nu)}$$
   $$\lambda = \frac{E\nu}{(1+\nu)(1-2\nu)}$$

   with

   - $E$: Young's modulus
   - $\nu$: Poisson ratio
  
4. Solving procedures:
   1. Initialization problem, set up initial temperature and displacement.
   2. Time step loop
      1. Solve thermal euquation
      2. Solve mechanical equation



####



