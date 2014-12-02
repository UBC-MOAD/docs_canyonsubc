Approximating Flow Separation over a Half Cylinder
==================================================

Potential Flow
-------------------

Consider a half-cylinder at the bottom boundary of an idealized inviscid fluid with a 
background flow field moving at a constant speed :math:`U_0` from left-to-right. 
The governing equations are:

.. math:: 
    \frac{\partial u}{\partial t} + u \frac{\partial u}{\partial x} + w \frac{\partial u}{\partial z} &= -\frac{1}{\rho} \frac{\partial p}{\partial x} \\
    \frac{\partial w}{\partial t} + u \frac{\partial w}{\partial x} + w \frac{\partial w}{\partial z} &= -\frac{1}{\rho} \frac{\partial p}{\partial z} \\
    \frac{\partial u}{\partial x} + \frac{\partial w}{\partial z} &= 0

The form of topography is given by:

.. math:: 
    z = h(x) = \begin{cases} 0, x<-R_0, \\ \sqrt{R_0^2 - x^2}, -R_0 < x < R_0 \\ 0, x > R_0 \end{cases}
    
The boundary conditions that will be imposed for the flow away from the cylinder are: far field conditions and no-normal flow conditions at the boundary.

.. math::
	\lim_{x,z\to \infty} u &= U_0, \\
	\vec{u}\cdot \hat{n} &= 0, \quad z = h(x).
	
Away from the half-cylinder the flow is irrotational, :math:`\vec{\nabla} \times \vec{u}=\vec{0}`, allowing a potential function to be defined:

.. math::
	u = \frac{\partial \phi}{\partial x}, \quad w = \frac{\partial \phi}{\partial z}.
	
The incompressibility condition reduces to:

.. math::
	\nabla^2 \phi &= 0.
	
This is Laplace's equation. Noting the axial symmetry, the math may be simplified by converting to polar coordinates. The Laplacian in polar coordinates may be represented by:

.. math::
	\frac{\partial^2 \phi}{\partial r^2} + \frac{1}{r} \frac{\partial \phi}{\partial r} + \frac{1}{r^2} \frac{\partial^2 \phi}{\partial \theta^2} = 0.
	
This equation may be solved using a separation of variables decomposition, :math:`\phi(r,\theta) = R(r)T(\theta)`. Substituting this into the previous equation yields two ordinary differential equations:

.. math::
	r^2 R''(r) + r R'(r) - \mu^2 R(r) &= 0, \\
	T''(\theta) + \mu^2 T(\theta) &= 0.

Solutions must be considered for both :math:`\mu=0` and :math:`\mu\neq 0`.

Case :math:`\mu=0`
~~~~~~~~~~~~~~~~~~~~

Solving the ODEs yields:

.. math::
	R(r) &= A_1 \ln r + A_2, \\
	T(\theta) &= B_1 \theta + B_2.
	
The no-normal flow conditions in polar coordinates are:

.. math::
	\frac{\partial \phi}{\partial \theta} = u_\theta = 0 &= T'(\theta), \qquad \theta = 0,\pi \\
	\frac{\partial \phi}{\partial r} = u_r = 0 &= R'(R_0), \qquad 0<\theta<\pi, \quad r = R_0

This forces :math:`T(\theta)=B_2` and :math:`R(r)=A_2`. This cannot satisfy the far-field condition and so the :math:`\mu=0` case is degenerate.

Case :math:`\mu\neq 0`
~~~~~~~~~~~~~~~~~~~~~~~~

The general solution to the ODE for :math:`R(r)` is found by substituting an arbitrary polynomial of the form :math:`R(r)=r^\gamma`:

.. math::
	\left[ \gamma^2 - \mu^2 \right] r^\gamma = 0.

If :math:`r\neq 0` (which is always true on this domain), then the solution for :math:`R(r)` becomes:

.. math::
	R(r) = A_1 r^\mu + A_2 r^{-\mu}
	
The solution for :math:`T(\theta)` becomes:

.. math::
	T(\theta) = B_1 \sin ( \mu \theta ) + B_2 \cos ( \mu \theta ).
	
Applying the polar coordinate boundary conditions to the previous solutions yield:

.. math::
	B_1 = 0, \qquad A_1 R_0^{2\mu} = A_2. \\
	\Rightarrow \qquad \phi(r,\theta) = C \left[ r^\mu + R_0^{2\mu} r^{-\mu} \right] \cos \mu \theta.
	
Applying the far-field condition in polar coordinates:

.. math::
	\lim_{x,z \to \infty} \frac{\partial \phi}{\partial x} &= U_0, \\
	\lim_{r \to \infty} \left\{ \cos \theta \frac{\partial \phi}{\partial r} - \frac{\sin \theta}{r} \frac{\partial \phi}{\partial \theta} \right\} &= U_0, \\
	\lim_{r \to \infty} \left\{ \cos \theta \cos \mu \theta \left[ r^{\mu - 1} - R_0^{2\mu} r^{-\mu -1} \right] + \sin \mu \theta \sin \theta \left[ r^{\mu - 1} + R_0^{2\mu}r^{-\mu-1} \right] \right\} &= \frac{U_0}{\mu C}.
	
If this is to be bounded as :math:`r\to\infty`, then :math:`\mu \in [-1,1]/\{0\}`. It must also be independent of :math:`r,\theta` (because the right hand side is a constant). This is only satisfied when :math:`\mu = \pm 1`. The final solution for :math:`\phi` is the same for either choice of :math:`\mu`:

.. math::
	\phi(r,\theta) &= U_0 \left[ r + R_0^{-2} r^{-1} \right] \cos \theta, \\
	\phi(x,z) &= U_0 x \left[ 1 + \frac{R_0^2}{x^2 + z^2} \right].
	
This will be used as the outer flow field solution when considering the boundary layer solution for flow over cylinder.

Pressure at the Boundary
------------------------------

Using the solution for velocity potential, the pressure field at the boundary can be defined using Bernoulli's equation for steady state pressure:

.. math::
	p + \frac{\rho}{2} \vec{\nabla} \phi \cdot \vec{\nabla} \phi &= C.
	
The undetermined coefficient :math:`C` may be solved by using a predetermined pressure reference. For this example, that reference will be the left stagnation point pressure (at :math:`x=-R_0,z=0`). Here :math:`\vec{\nabla}\phi=\vec{0}`, and so :math:`C=p_{sp}` (using :math:`p_{sp}` to denote pressure at the stagnation point). The full equation for pressure becomes:

.. math::
	p = p_{sp} + \rho \frac{U_0^2}{2} \left[ \left( R_0^2 - x^2 \right)^2 + z^4 + 2x^2z^2 + 2 R_0^2 z^2 \right] \left(x^2 + z^2 \right)^{-2}.

Solving for pressure along the boundary yields:

.. math::
	p_{bdy}(x) &= p_{sp} + 2 \rho U_0^2 \left( 1 - \frac{x^2}{R_0^2} \right), \\
	p_{bdy}(\theta) &= p_{sp} + 2 \rho U_0^2 \sin^2 \theta.
	
Prandtl's Boundary Layer Equations
------------------------------------

The equations that balance viscosity, pressure and advection near the boundary in a steady state are Prandtl's boundary layer equations, given by:

.. math::
	u^* \frac{\partial u^*}{\partial x^*} + w^* \frac{\partial u^*}{\partial z^*} &= -\frac{1}{\rho} \frac{d p}{d x^*} + \nu \frac{\partial^2 u^*}{\partial z^{*2}}, \\
	\frac{\partial u^*}{\partial x^*} + \frac{\partial w^*}{\partial z^*} &= 0.
	
The components are starred here to denote that the coordinate system differs from the standard Cartesian system. The :math:`x^*` coordinate denotes the along boundary coordinate, and the :math:`z^*` coordinate denotes the normal coordinate. In terms of the half-cylinder problem:

.. math::
	x^* &= (\pi - \theta) R_0, \\
	z^* &= r - R_0.
	
Substituting in the equation for pressure at the boundary:

.. math::
	u^* \frac{\partial u^*}{\partial x^*} + w^* \frac{\partial u^*}{\partial z^*} &= \frac{4U_0^2}{R_0} \sin \frac{ x^*}{R_0} \cos \frac{x^*}{R_0} + \nu \frac{\partial^2 u^*}{\partial z^{*2}}, \\
	\frac{\partial u^*}{\partial x^*} + \frac{\partial w^*}{\partial z^*} &= 0.
	
The separation point is the point along the boundary that satisfies:

.. math::
	\left. \frac{\partial u^*}{\partial z^*} \right|_{z^* = 0} = 0