Real-Time Rendering Fourth Edition / 13.6 Billboarding  

Vertex Position //quad in XOY  
(-1.0, 1.0, 0.0f)  
(1.0, 1.0, 0.0f)  
(-1.0, -1.0, 0.0f)  
(1.0, -1.0, 0.0f)

RightDirection + UpDirection => Rotation
AnchorPosition => Translation

Position = RightDirection * Position.x + UpDirection * Position.y + AnchorPosition

calculate RightDirection/UpDirection/AnchorPosition

//in asotropic NDF
//modified Gram-Schmidt process

FrontDirection->n //normal

1\.world-oriented  
keep FrontDirection fixed and deduce UpDirection  
// same for LH/RH  
// maybe not normalized after cross  
RightDirection = normalize(Cross(UpDirection, FrontDirection))  
UpDirection = normalize(Cross(FrontDirection, RightDirection))

//1-1\. screen-aligned  

//1-2\. viewplane-aligned  
FrontDirection is fixed to EyeDirection of ViewTransform  

1-3\. viewpoint-oriented //Spherical Symmetry  
FrontDirection = EyePosition - AnchorLocation  

2\. axial 
keep UpDirection fixed and deduce UpDirection  
RightDirection = normalize(Cross(UpDirection, FrontDirection))  
FrontDirection = Cross(RightDirection, UpDirection) 

2-1\. viewpoint-oriented // Circular Symmetry
