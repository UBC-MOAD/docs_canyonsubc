Literature Review, Flow Separation over a Sill
===================================

.. _cummins00:

PF Cummins (2000) "Stratified flow over topography: time-dependent comparisons between model solutions and observations"
-------------------------

Using the Princeton Ocean Model (POM), the author was able to simulate flow over an idealized model of the Knight Inlet. The results obtained using this model were then compared to data collected over the Inlet. The model does a poor job of resolving the flow separation in lee of the sill; in particular the model flow demonstrates an apparent overturning which is not evident in the data. This overturning results in a "high drag state" -- defined by Cummins to be the state of strong spatial acceleration of flow that is associated with a pressure drop across the sill. Essentially, this state causes an opposing force on the fluid due to the pressure gradient. High drag state is analogous to downslope windstorms in atmospheric dynamics.

High drag state is well known and is observed in the data, however, the overturning causes the drag state to be reached too early in the numerical simulations. This discrepency is likely due to the hypothesis put forward by Cummins; a poor representation of the boundary layer occurring in the lee of the sill.

*(a) The numerical model used and parameters used*

The author argues that the data obtained during the "Knight Inlet Experiment" suggests that the flow is largely 2D in the region during the ebb tide. By assuming 2D flow, the model simplifies significantly and resolution may be increased significantly.

The model uses a free surface, a nonlinear equation of state, suppresses rotational effects, Smagorinsky eddy viscosity, quadratic drag on the bottom boundary (using a drag coefficient derived from von Karman's law-of-the-wall). Additionally, a level 2.5 turbulence closure submodel is used to dissipate high wavenumber energy (Mellor and Yamada, 1982).

The author used 101 sigma levels for the cases presented and stated that increasing the vertical resolution to 201 sigma levels did not change the solutions significantly. Horizontal grid resolution around the sill was varied between 5m and 30m, with presented results of 10m horizontal resolution.

The tidal forcing is given as an influx condition on the left boundary (see figure 2 of paper). Maximum velocity acheived is ~62cm/s after 3.5h. The author focusses on the ebb-tide and states that consideration of the response to flood tide is beyond the scope of interest. 

*(b) Results*

The stratification is analytical and three layer, matching well with observations. Internal normal mode wave solutions for this stratification were calculated, and the phase speeds were reported for the first and second vertical internal modes.


.. _lamb00:

KG Lamb (2004), "On boundary-layer separation and internal wave generation at the Knight Inlet sill"
-----------------

