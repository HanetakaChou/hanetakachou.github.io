# IK (Inverse Kinematics)  

## Quadruped Foot IK  

### Optimal Plane  

Linear Regression  

OLS(Ordinary Least Squares)  

Normal Equations  

```cpp
DirectX::XMFLOAT4 inline optimal_plane(DirectX::XMFLOAT4 p0, DirectX::XMFLOAT4 p1, DirectX::XMFLOAT4 p2, DirectX::XMFLOAT4 p3)
{
	// Ax + By + Cz + D = 0 => (A/C)x + (B/C)y + (D/C) = -z

	DirectX::XMFLOAT4A targets(
		-p0.z, -p1.z, -p2.z, -p3.z);

	DirectX::XMFLOAT4X4A features(
		p0.x, p1.x, p2.x, p3.x,
		p0.y, p1.y, p2.y, p3.y,
		1.0F, 1.0F, 1.0F, 1.0F,
		0.0F, 0.0F, 0.0F, 0.0F);

	DirectX::XMVECTOR simd_y = DirectX::XMLoadFloat4A(&targets);

	DirectX::XMMATRIX simd_X = DirectX::XMLoadFloat4x4A(&features);

	DirectX::XMFLOAT4X4A XT_mul_X;
	DirectX::XMStoreFloat4x4A(&XT_mul_X, DirectX::XMMatrixMultiply(simd_X, DirectX::XMMatrixTranspose(simd_X)));
	XT_mul_X.m[3][3] = 1.0F;

	DirectX::XMMATRIX simd_XT_mul_X = DirectX::XMLoadFloat4x4A(&XT_mul_X);

	DirectX::XMVECTOR simd_determinant;
	DirectX::XMMATRIX simd_XT_mul_X_inv = DirectX::XMMatrixInverse(&simd_determinant, simd_XT_mul_X);

	DirectX::XMVECTOR simd_XT_mul_y = DirectX::XMVector4Transform(simd_y, DirectX::XMMatrixTranspose(simd_features));

	DirectX::XMVECTOR simd_beta = DirectX::XMVector3TransformNormal(simd_XT_mul_y, simd_XT_mul_X_inv);

    // | (A/C) (B/C) (D/C) |  
    DirectX::XMFLOAT3 coefficients;
	DirectX::XMStoreFloat3(&coefficients, simd_beta);

	DirectX::XMFLOAT4 plane(coefficients.x, coefficients.y, 1.0F, coefficients.z);
	DirectX::XMVECTOR simd_plane = DirectX::XMLoadFloat4(&plane);

	DirectX::XMVECTOR simd_normalized_plane = DirectX::XMPlaneNormalize(simd_plane);

	DirectX::XMFLOAT4 normalized_plane;
	DirectX::XMStoreFloat4(&normalized_plane, simd_normalized_plane);
	return normalized_plane;
}
```

