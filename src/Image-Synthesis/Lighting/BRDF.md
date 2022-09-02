## Half Vector

The half vector H is the microsurface normal $\displaystyle \omega_m$ in the formulation while the normal N is the geometric normal $\displaystyle \omega_g$ in the formulation.  

According to the "9.8 BRDF Models for Surface Reflection" of [Real-Time Rendering Fourth Edition](https://www.realtimerendering.com/), \[Hammon 2017\] proposed a method to calculate the NdotH and LdotH without the knowledge of the half vector H itself.

```GLSL
    // |L + V|^2 = L^2 + V^2 + 2L·V = 1 + 1 + 2L·V
    // N·H = N·((L + V)/(|L + V|)) = (N·L + N·V)/(|L + V|)
    // L·H = L·((L + V)/(|L + V|)) = (L^2 + L·V)/(|L + V|)
    // V·H = V·((L + V)/(|L + V|)) = (L·V + V^2)/(|L + V|)
    // 2L·H = 2V·H = L·H + V·H = (L^2 + L·V + L·V + V^2)/(|L + V|) = (|L + V|^2)/(|L + V|) = |L + V| = 1 + 1 + 2L·V
    // ⇒ L·H = 0.5 * |L + V| = (0.5 * |L + V|^2)/(|L + V|) =(0.5 * (1 + 1 + 2L·V))/(|L + V|) = 1/(|L + V|) + (L·V)/(|L + V|)
    // UE: [Init](https://github.com/EpicGames/UnrealEngine/blob/4.27/Engine/Shaders/Private/BRDF.ush#L31)
    // U3D: [GetBSDFAngle](https://github.com/Unity-Technologies/Graphics/blob/v10.8.0/com.unity.render-pipelines.core/ShaderLibrary/CommonLighting.hlsl#L361)
    highp float invLenH = inversesqrt(2.0 + 2.0 * NdotL);
    highp float NdotH = clamp((NdotL + NdotV) * invLenH, 0.0, 1.0);
    highp float LdotH = clamp(invLenH * VdotL + invLenH, 0.0, 1.0);
```

The **NdotH** and the **LdotH** are calculated by [GetBSDFAngle](https://github.com/Unity-Technologies/Graphics/blob/v10.8.0/com.unity.render-pipelines.core/ShaderLibrary/CommonLighting.hlsl#L361) in Unity3D and [Init](https://github.com/EpicGames/UnrealEngine/blob/4.27/Engine/Shaders/Private/BRDF.ush#L31) in UE4.  


## Specular AA

"Real-Time Rendering Fourth Edition \ Equation 9.76"  
[TextureNormalVariance](https://github.com/Unity-Technologies/Graphics/blob/v10.8.0/com.unity.render-pipelines.core/ShaderLibrary/CommonMaterial.hlsl#L214) by U3D  

## Trowbridge-Reitz  

### NDF  

According to the "9.8.1 Normal Distribution Functions" of [Real-Time Rendering Fourth Edition](https://www.realtimerendering.com/), the **GGX** should technically be called the **Trowbridge-Reitz** which is also adopted by the "8.4 Microfacet Models" of [PBR Book](https://pbr-book.org/).  

### G  

\[Heitz 2014\] 

## References  

\[Heitz 2014\] [Eric Heitz. "Understanding the Masking-Shadowing Function in Microfacet-Based BRDFs." JCGT 2014.](https://jcgt.org/published/0003/02/03/)  
\[Hammon 2017\] [Earl Hammon. "PBR Diffuse Lighting for GGX+Smith Microsurfaces." GDC 2017.](https://www.gdcvault.com/play/1024478/PBR-Diffuse-Lighting-for-GGX)  

