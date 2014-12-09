Calculate numerical diffusivity
============================

This module has functions to calculate the numerical diffusivity experienced by a tracer, associated to a specific configuration of the MITgcm. In particular, it was developed to calculate the equivalent diffusivity $\kappa$, defined (here) as $\kappa = \kappa_{pres}+\kappa_{num}$, where $\kappa_{pres}$ 
is the prescibed or explicit tracer diffusivity one imposes on the model and $k_{num}$ is the additional diffusivity due to numerical truncation errors. Note that there are two $\kappa_{pres}$ and therefore two $\kappa$, one for the horizontal dimensions and one for the vertical one.

These calculations try to reproduce the method used by [1] Abernathy et al. 2010, [2] Hill et al. 2011, and [3] Leibensperger and Plumb, 2013 to determine the numerical diffusivity MITgcm Southern Ocean configurations [1,2] and a baroclinic flow simulation simulation [3].


The idea is that from the evolution equation for the variance of the tracer concentration in the model output

\begin{equation}
\frac{1}{2}\frac{\partial{\overline{q^{2}}}}{\partial{t}}=-\kappa_{h} \overline{|\nabla_h q|^2}-\kappa_{v} \overline{(\frac{\partial{q}}{\partial {z}})^{2}}
\end{equation}

one can fit by a least squares regression, suitable values of $\kappa_h$ and $\kappa_v$ that satisfy the equation.

Calculate the volume of the domain (function: CalcDomVolume)
-------------------------------
The volume of a tracer cell (remember we have an Arakawa C grid, so this changes depending on which kind of cell we are thinking about) is given by

$V(i,j,k)=depth \times area = (hfacC(i,j,k)\times dRf(k)) \times rA(i,j) = (hfacC(i,j,k)\times dRf(k)) \times dXg(i,j) \times dYg(i,j)$,

where hfacC is the fraction of the cell that is open (not occupied with land). So, the total volume of the domain is 

$\sum\limits_{i=1}^{nx}{\sum\limits_{j=1}^{ny}{\sum\limits_{k=1}^{nz}{(hfacC(i,j,k)\times dRf(k)) \times rA(i,j)}}}$


1st Term: The volume-weighted average of the squared concentration (function: CalcVariance, CalcTimeDer)
-------------------------------------------------------------
The first term in the variance evolution equation is $\frac{1}{2}\frac{\partial{\overline{q^{2}}}}{\partial{t}}$. Note that we care about the time derivative of the variance, so that the mean concentration that usually appears in the definition of variance will not play a role here, since it is constant in time (we are not putting in or letting out any tracer). 

We are going to calculate $\overline{q^2}$, the volume-weighted average of the squared concentration, and then the time derivative of that using a centered difference scheme.



2nd Term: The volume-weighted average of the squared horizontal gradient (function: CalcAvgHorGrad)
------------------------------------------------------------------
The second term in the variance evolution equation is $-\kappa_{h} \overline{|\nabla_h q|^2}$. Next, we calculate the square of the horizontal gradient $|\nabla_h q|^2=(\frac{\partial{q}}{\partial{x}})^2+(\frac{\partial{q}}{\partial{y}})^2$.

Spatial derivatives are approximated using a centered-difference scheme.


3rd Term: The volume-weighted average of the squared vertical derivative (function: CalcAvgVerGrad)
------------------------------------------------------------------
The third term in the variance evolution equation is $-\kappa_{v} \overline{(\frac{\partial{q}}{\partial{z}})^2}$. Next, we calculate the square of the vertical gradient $(\frac{\partial{q}}{\partial{z}})^2$.

The vertical derivative is approximated using a centered-difference scheme.