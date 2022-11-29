# Path Tracing

## Rendering Equation

By "14.4 The Light Transport Equation" of [PBR Book](https://www.pbr-book.org/3ed-2018/Light_Transport_I_Surface_Reflection/The_Light_Transport_Equation), the **Rendering Equation** is also called the **LTE** (**Light Transport Equation**).  

And by "Light transport and the rendering equation" of [CS 348B - Computer Graphics: Image Synthesis Techniques](http://www-graphics.stanford.edu/courses/cs348b-96/transport/transport.html) and "Global Illumination and Rendering Equation" of [CS 294-13 Advanced Computer Graphics](https://inst.eecs.berkeley.edu/~cs294-13/fa09/), the LTE (Light Transport Equation) is actually the [Fredholm Integral Equation](https://en.wikipedia.org/wiki/Fredholm_integral_equation) of which the solution is the [Liouville–Neumann Series](https://en.wikipedia.org/wiki/Liouville%E2%80%93Neumann_series). And thus, the solution of the LTE can be written as the recursive form $\text{L} = \text{E} + \text{K}\text{E} + {\text{K}}^2\text{E} + {\text{K}}^3\text{E} + \ldots$.  

Actually, by [OSL](https://github.com/AcademySoftwareFoundation/OpenShadingLanguage), light and surface are the same thing since light is merely the surface which is emissive.  
