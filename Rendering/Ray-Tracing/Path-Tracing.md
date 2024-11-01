# Path Tracing  

## Throughput

## Delta Distribution  

["14.4.5 Delta Distributions in the Integrand"](https://pbr-book.org/3ed-2018/Light_Transport_I_Surface_Reflection/The_Light_Transport_Equation#DeltaDistributionsintheIntegrand) of "PBR Book V3"  
["13.1.5 Delta Distributions in the Integrand"](https://pbr-book.org/4ed/Light_Transport_I_Surface_Reflection/The_Light_Transport_Equation#DeltaDistributionsintheIntegrand) of "PBR Book V4"

## Texture Sampling and Antialiasing  

### Ray Differentials  

ray differentials -> mipmap Level   
"10.1 Texture Sampling and Antialiasing" of "PBR Book V4"  
"10.1 Sampling and Antialiasing" of "PBR Book V3"  

### Specular Antialiasing  

Toksvig   
normal variance  
the NDF of the average normal and the average roughness (separately) is NOT the average NDF  
[NormalCurvatureToRoughness](https://github.com/EpicGames/UnrealEngine/blob/4.27/Engine/Shaders/Private/BasePassPixelShader.usf#L67) of "Unreal Engine"  
[TextureNormalVariance](https://github.com/Unity-Technologies/Graphics/blob/v10.8.1/com.unity.render-pipelines.core/ShaderLibrary/CommonMaterial.hlsl#L214) of "Unity3D"  
"7.8.1 Mipmapping BRDF and Normal Maps" of "Real-Time Rendering Third Edition"  
"9.13.1 Filtering Normals and Normal Distributions" of "Real-Time Rendering Fourth Edition"  
