# ReSTIR (Reservoir-based SpatioTemporal Importance Resampling)  

## LTE (Light Transport Equation)

By "Global Illumination and Rendering Equation" of [CS 294-13 Advanced Computer Graphics](https://inst.eecs.berkeley.edu//~cs294-13/fa09/), the LTE (Light Transport Equation) is actually the [Fredholm Integral Equation](https://en.wikipedia.org/wiki/Fredholm_integral_equation) of which the solution is the [Liouville–Neumann Series](https://en.wikipedia.org/wiki/Liouville%E2%80%93Neumann_series). And thus, the LTE can be written as the recursive form $\text{L} = \text{E} + \text{K}\text{E} + {\text{K}}^2\text{E} + {\text{K}}^3\text{E} + \ldots$.  

Actually, by [OSL](https://github.com/AcademySoftwareFoundation/OpenShadingLanguage), light and surface are the same thing since light is merely the surface which is emissive.  
