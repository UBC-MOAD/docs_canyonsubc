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
    z = h(x) = \begin{cases} 0, & x<-R_0, \\ \sqrt{R_0^2 - x^2}, &-R_0 < x < R_0 \\ 0, &x > R_0 \end{cases}
    
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
	\phi(r,\theta) &= U_0 \left[ r + R_0^{2} r^{-1} \right] \cos \theta, \\
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
	u^* \frac{\partial u^*}{\partial x^*} + w^* \frac{\partial u^*}{\partial z^*} &= \frac{4U_0^2}{R_0} \sin \frac{ x^*}{R_0} \cos \frac{x^*}{R_0} + \nu \frac{\partial^2 u^*}{\partial z^{*2}} = U_{bdy}(x^*)\frac{dU_{bdy}}{dx^*} + \nu \frac{\partial^2 u^*}{\partial z^{*2}}, \\
	\frac{\partial u^*}{\partial x^*} + \frac{\partial w^*}{\partial z^*} &= 0.
	
The separation point is the point along the boundary that satisfies:

.. math::
	\left. \frac{\partial u^*}{\partial z^*} \right|_{z^* = 0} = 0
	
The far-field condition satisfies the velocity potential at the boundary. The far-field potential in terms of the boundary variable :math:`x^*` is:

.. math::
	\phi_{ff}(R_0,\theta) &= 2 U_0 R_0 \cos \theta, \\
	\phi_{ff}(x^*) &= - 2 U_0 R_0 \cos \frac{x^*}{R_0}
	
Explicitly stating the far-field condition:

.. math::
	\lim_{z^* \to \infty} u^* = U_{bdy}(x^*) = \frac{d \phi_{ff}}{d x^*} = 2 U_0 \sin \left( \frac{x^*}{R_0} \right).
	
Following "Boundary Layer Theory", Schlichting, 1979, the boundary layer equations may be treated using a Blausius series. In order to approach this problem, rewrite in terms of the streamfunction, :math:`\psi`:

.. math::
	u^* = \frac{\partial \psi}{\partial z^*}, \quad w^* = -\frac{\partial \psi}{\partial x^*}, \\
	\frac{\partial \psi}{\partial z^*}	\frac{\partial^2 \psi}{\partial x^* \partial z^*} - \frac{\partial \psi}{\partial x^*} \frac{\partial^2 \psi}{\partial z^{*2}} - \nu \frac{\partial^3 \psi}{\partial z^{*3}} &= \frac{4U_0^2}{R_0} \sin \frac{x^*}{R_0} \cos \frac{x^*}{R_0}
	
The solution must satisfy the no-slip condition, and the far field condition:

.. math::
	\frac{\partial \psi}{\partial x^*} = \frac{\partial \psi}{\partial z^*} &= 0, \qquad \hbox{at $z^*=0$}, \\
	\lim_{z^* \to \infty} \psi &= U_{bdy}(x^*)z^*

To solve this equation, a series solution must be obtained. A general series for :math:`\psi` is:

.. math::
	\psi(x^*,z^*) = \sum_{n=0}^\infty x^{*n} f_n(z^*)

Noting the far-field condition is an odd function in :math:`x^*`:

.. math::
	\lim_{z^*\to\infty} \frac{\partial \psi}{\partial z^*} = U_{bdy}(x^*) = u_1 x^* + u_3 x^{*3} + u_5 x^{*5} + \dots

And so the streamfunction must also be an odd function of :math:`x^*`. Using the odd expansion of the streamfunction and substituting into the streamfunction momentum equation:

.. math::
	(\hbox{DE}_1)x + (\hbox{DE}_3)x^3 + (\hbox{DE}_5)x^5 + \mathcal{O}(x^7) = 0
	
Where each of the quantities in brackets are ordinary differential equations in :math:`f_i(z^*)`. To write them explicitly:

.. math::
	\hbox{DE1}: \quad& (f_1')^2 - f_1 (f_1'') - \nu f_1''' - 4\frac{U_0^2}{R_0^2} = 0 \\
	\hbox{DE3}:\quad& 4 f_1' f_3' - f_1 f_3'' - 3 f_3 f_1'' - \nu f_3''' + \frac{8}{3} \frac{U_0^2}{R_0^4} = 0 \\
	\hbox{DE5}:\quad& 6 f_1' f_5' + 3 (f_3')^2 - f_1 f_5'' - 5 f_5 f_1'' - 3 f_3 f_3'' - \nu f_5''' - \frac{8}{15} \frac{U_0^2}{R_0^6} = 0
	
Where primed quantities denote the derivative with respect to :math:`z^*`. The initial differential equation is the most difficult due to the nonlinearity. It must be treated asymptotically and an approximate solution must be acquired before solving the simpler differential equations (DE3, DE5, etc.).

It should be noted here that these equations may be used to derive a natural scale for the boundary layer thickness. In the middle of the boundary layer, each term of Prandtl's equations are balanced, and so must be the terms in DE1. If :math:`\delta` represents this natural scale for boundary layer thickness, use a scaled vertical component, :math:`\eta=z^*/\delta`, in order, the terms are scaled as:

.. math::
	\frac{F^2}{\delta^2},\frac{F^2}{\delta^2},\frac{\nu F}{\delta^3},4\frac{U_0^2}{R_0^2}
	
where :math:`F` is the natural scaling for :math:`f_1`. This leads to the termwise balance:

.. math::
	F \sim \nu/\delta, \quad R_0^2 \nu^2/4U_0^2 \sim \delta^4  \\
	\Rightarrow \quad& \delta \sim \sqrt{ \frac{R_0 \nu}{2 U_0}} \\
	\Rightarrow \quad& F \sim \sqrt{\frac{2U_0 \nu}{R_0}}
	
For numerical simulations, values of 

.. math::
	R_0=2.5cm,U_0=1cm\cdot s^{-1},\nu=10^{-6} m^2 \cdot s^{-1}

are used, yielding a boundary thickness of :math:`\delta \sim 1.12mm`.

The boundary and far-field conditions are important to determine for :math:`f_n`. Explicitly:

.. math::
	\hbox{BCs}: \quad& f_n(0) = 0, \quad f_n'(0) = 0 \\
	\hbox{FFCs}: \quad& \lim_{z^* \to \infty} f_n'(z^*) = \frac{2U_0}{n!R_0^n}, \quad n = 2j + 1 \quad \hbox{for $j=0\dots\infty$} 

Solving :math:`f_1`
~~~~~~~~~~~~~~~~~~~~

DE1 must be treated approximately. Because this analysis is concerned with separation processes, series solutions in :math:`z^*` will be sufficiently accurate. The series solution to DE1 reads:

.. math::
	f_1(z^*) \approx \frac{A_1}{2} z^{*2} - \frac{2}{3} \frac{U_0^2}{R_0^2 \nu} z^{*3} \quad \hbox{for} \quad z^* \ll \delta
	
In order to solve for :math:`A_1`, this will have to be matched to the outer solution. The outer solution is obtained by considering the far field condition. Second-order and higher derivatives of :math:`f_n` vanish as :math:`z^*\to\infty` and so high order derivatives are ignored. This leaves a solution of the form:

.. math::
	f_1(z^*) \approx \frac{2U_0}{R_0}z^* + B_1, \quad \hbox{for} \quad z^* \gg \delta
	
The inner and outer solutions are matched as :math:`z^* \to \delta`. By making the matched solution continuous and smooth, the values of :math:`A_1` and :math:`B_1` may be solved:

.. math::
	A_1 &= 3 \sqrt{\frac{2}{\nu}} \frac{U_0^{3/2}}{R_0^{3/2}}, \\
	B_1 &= -\frac{5}{12} \sqrt{\frac{2}{\nu}} \frac{\nu U_0^{1/2}}{R_0^{1/2}}