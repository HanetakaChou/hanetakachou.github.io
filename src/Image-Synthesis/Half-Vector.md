### **N·H** and **L·H**

```c++
// Real-Time Rendering Fourth Edition: "Hammon also shows a method to optimize the BRDF implementation by calculating **n·h** and **l·h** without calculating the vector **h** itself."  

// We assume that N, V, L are normalized.

// |L + V|^2 = L^2 + V^2 + 2L·V = 1 + 1 + 2L·V
float rcpLen_LV = rsqrt(2.0 + 2 * NdotV);

// N·H = N·((L + V)/(|L + V|)) = (N·L + N·V)/(|L + V|)
float NdotH = saturate((NdotL + NdotV) * rcpLen_LV);

// L·H = L·((L + V)/(|L + V|)) = (L^2 + L·V)/(|L + V|)
// V·H = V·((L + V)/(|L + V|)) = (L·V + V^2)/(|L + V|)
// 2L·H = 2V·H = L·H + V·H = (L^2 + L·V + L·V + V^2)/(|L + V|) = (|L + V|^2)/(|L + V|) = |L + V| = 1 + 1 + 2L·V
// ⇒ L·H = 0.5 * |L + V| = (0.5 * |L + V|^2)/(|L + V|) =(0.5 * (1 + 1 + 2L·V))/(|L + V|) = 1/(|L + V|) + (L·V)/(|L + V|)
float LdotH = saturate(rcpLen_LV * LdotV + invLenLV);
```

The **N·H** and the **L·H** are calculated by [GetBSDFAngle](https://github.com/Unity-Technologies/Graphics/blob/v10.8.0/com.unity.render-pipelines.core/ShaderLibrary/CommonLighting.hlsl#L361) in Unity3D and [Init](https://github.com/EpicGames/UnrealEngine/blob/4.27/Engine/Shaders/Private/BRDF.ush#L31) in UE4.  
