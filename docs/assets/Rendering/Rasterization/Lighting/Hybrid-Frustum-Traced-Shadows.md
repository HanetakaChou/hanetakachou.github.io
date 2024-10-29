# HFTS (Hybrid Frustum Traced Shadows)  

IZB (Irregular Z-Buffers)  

[NVIDIA ShadowWorks](https://developer.nvidia.com/shadowworks)  

Real Time Rendering //
"With a tile/edge intersection test in place, it is possible to hierarchically traverse a triangle."
"Both OCR and UCR can be implemented using tiled traversal by shrinking the tile size to one pixel."

OCR(Overestimated Conservative Rasterization) //Outer-Conservative Rasterization //API中的CR
UCR(Underestimated Conservative Rasterization) //Inner-Conservative Rasterization

Implement 32 MSAA By Software —— "Since samples can lie anywhere within a texel, conservative rasterization is required"

To Solve "Perspecrive Aliasing" //One Pixel In Eye-Space Match Large Volume In View Space In the Distance

//To Do List:

//Q: How Shoud We Do If One Pixel In Eye-Space Match More Than One Pixel In Light-Space?  
//A: Calculate A Threshould Distance?

## References  
\[Wyman 2015\] [Chris Wyman, Rama Hoetzlein, Aaron Lefohn. "Frustum-Traced Raster Shadows: Revisiting Irregular Z-Buffers." I3D 2015.](https://research.nvidia.com/publication/frustum-traced-raster-shadows-revisiting-irregular-z-buffers)  
\[Story 2015 A\] [Jon Story. "Hybrid Ray Traced Shadows". NVIDIA Developer 2015](https://developer.nvidia.com/content/hybrid-ray-traced-shadows)  
\[Story 2015 B\] [Jon Story. "Hybrid Ray Traced Shadows". GDC 2015.](http://developer.download.nvidia.com/assets/events/GDC15/hybrid_ray_traced_GDC_2015.pdf)  
\[Story 2016 A\] [Jon Story. "Hybrid Frustum Traced Shadows". NVIDIA Developer 2016](https://developer.nvidia.com/hybrid-frustum-traced-shadows-0)  
\[Story 2016 B\] [Jon Story. "Advanced Geometrically Correct Shadows for Modern Game Engines". GDC 2016.](http://developer.download.nvidia.com/gameworks/events/GDC2016/jstory_hfts.pdf)  
