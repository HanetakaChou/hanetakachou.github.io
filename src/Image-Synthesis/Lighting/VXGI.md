# VXGI (Voxel Global Illumintaion)  

## Photon Mapping  

By \[Jensen 1996\] and "16.2.2 Photon Mapping" of [PBRT-V3](https://pbr-book.org/3ed-2018/Light_Transport_III_Bidirectional_Methods/Stochastic_Progressive_Photon_Mapping#PhotonMapping), the **photon mapping** is composed of two-pass: the **photon pass** and the **rendering pass**. In the first pass (photon pass), the paths are traced from the light sources and the lighting of the interaction points on the surface are recorded as the photons. In the second pass (rendering pass), the paths are traced from the camera and the nearby photons of the interaction points are used to estimate the lighting.  

![](VXGI-1.png)  
![](VXGI-2.png)  

By "Progressive Photon Mapping" of [PBRT-V3](https://pbr-book.org/3ed-2018/Light_Transport_III_Bidirectional_Methods/Stochastic_Progressive_Photon_Mapping#x2-ProgressivePhotonMapping), the approach, that only the interaction points after the diffuse bounce are recorded as the photons in the photon pass, is also called the **final gathering**.  

![](VXGI-3.png)  

By \[Crassin 2011 B\], the idea of VXGI is to use the voxel cone tracing to perform the final gathering. The VXGI is composed of three pass: light injection pass, filtering pass and voxel cone tracing pass. In the first pass (light injection pass), the photons are organized in the voxels. In the second pass (filtering pass), TODO. In the third pass (voxel cone tracing pass), the voxel cone tracing is used to perform the final gathering.  

![](VXGI-4.png)  

## Voxel Cone Tracing  

## Reference  

\[Jensen 1996\] [Henrik Wann Jensen. "Global Illumination using Photon Maps." EGSR 1996.](http://graphics.ucsd.edu/~henrik/papers/photon_map/)  
\[Crassin 2011 A\] [Cyril Crassin. "GigaVoxels: A Voxel-Based Rendering Pipeline For Efficient Exploration Of Large And Detailed Scenes." PhD Thesis 2011.](http://gigavoxels.inrialpes.fr/index.html)  
\[Crassin 2011 B\] [Cyril Crassin, Fabrice Neyret, Miguel Sainz, Simon Green, Elmar Eisemann. "Interactive Indirect Illumination Using Voxel Cone Tracing." SIGGRAPH 2011.](https://research.nvidia.com/publication/interactive-indirect-illumination-using-voxel-cone-tracing) 