# IK (Inverse Kinematics)  

## Biped Foot IK  

sample animation -> 

## Quadruped Foot IK  

### Linear Regression    

optimal plane  

OLS(Ordinary Least Squares)  

Normal Equations  

// Assume +Z Up  
// Ax + By + Cz + D = 0 => z = (-(A/C))x + (-(B/C))y + (-(D/C))  

```cpp
DirectX::XMFLOAT4 inline plane_train(DirectX::XMFLOAT3 p0, DirectX::XMFLOAT3 p1, DirectX::XMFLOAT3 p2, DirectX::XMFLOAT3 p3)
{
    DirectX::XMFLOAT4A targets(
        p0.z, p1.z, p2.z, p3.z);

    DirectX::XMFLOAT4X4A features(
        p0.x, p1.x, p2.x, p3.x,
        p0.y, p1.y, p2.y, p3.y,
        1.0F, 1.0F, 1.0F, 1.0F,
        0.0F, 0.0F, 0.0F, 0.0F);

    DirectX::XMVECTOR simd_targets = DirectX::XMLoadFloat4A(&targets);

    DirectX::XMMATRIX simd_features = DirectX::XMLoadFloat4x4A(&features);

    DirectX::XMFLOAT4X4A XT_mul_X;
    DirectX::XMStoreFloat4x4A(&XT_mul_X, DirectX::XMMatrixMultiply(simd_features, DirectX::XMMatrixTranspose(simd_features)));
    XT_mul_X.m[3][3] = 1.0F;

    DirectX::XMMATRIX simd_XT_mul_X = DirectX::XMLoadFloat4x4A(&XT_mul_X);

    DirectX::XMVECTOR simd_determinant;
    DirectX::XMMATRIX simd_XT_mul_X_inv = DirectX::XMMatrixInverse(&simd_determinant, simd_XT_mul_X);

    DirectX::XMVECTOR simd_XT_mul_y = DirectX::XMVector4Transform(simd_targets, DirectX::XMMatrixTranspose(simd_features));

    DirectX::XMVECTOR simd_beta = DirectX::XMVector3TransformNormal(simd_XT_mul_y, simd_XT_mul_X_inv);

    DirectX::XMFLOAT3 coefficients;
    DirectX::XMStoreFloat3(&coefficients, simd_beta);

    DirectX::XMFLOAT4 plane(-coefficients.x, -coefficients.y, 1.0F, -coefficients.z);
    DirectX::XMVECTOR simd_plane = DirectX::XMLoadFloat4(&plane);

    DirectX::XMVECTOR simd_normalized_plane = DirectX::XMPlaneNormalize(simd_plane);

    DirectX::XMFLOAT4 normalized_plane;
    DirectX::XMStoreFloat4(&normalized_plane, simd_normalized_plane);
    return normalized_plane;
}
```

```cpp
float inline plane_inference(DirectX::XMFLOAT4 normalized_plane, DirectX::XMFLOAT2 p_xy)
{
    DirectX::XMFLOAT3A coefficients(-(normalized_plane.x / normalized_plane.z), -(normalized_plane.y / normalized_plane.z), -(normalized_plane.w / normalized_plane.z));

    DirectX::XMVECTOR simd_beta = DirectX::XMLoadFloat3A(&coefficients);

    DirectX::XMFLOAT3A target_and_intercept(p_xy.x, p_xy.y, 1.0F);
    DirectX::XMVECTOR simd_target = DirectX::XMLoadFloat3A(&target_and_intercept);

    float prediction = DirectX::XMVectorGetX(DirectX::XMVector3Dot(simd_beta, simd_target));
    return prediction;
}
```

