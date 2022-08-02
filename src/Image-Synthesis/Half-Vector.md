Real-Time Rendering Fourth Edition: "Hammon also shows a method to optimize the BRDF implementation by calculating **n·h** and **l·h** without calculating the vector **h** itself."  

The **n·h** and the **l·h** are calculated by [GetBSDFAngle](https://github.com/Unity-Technologies/Graphics/blob/v10.8.0/com.unity.render-pipelines.core/ShaderLibrary/CommonLighting.hlsl#L361) in Unity3D and [Init](https://github.com/EpicGames/UnrealEngine/blob/4.27/Engine/Shaders/Private/BRDF.ush#L31) in UE4.  
