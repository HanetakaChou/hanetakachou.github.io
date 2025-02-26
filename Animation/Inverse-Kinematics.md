# IK (Inverse Kinematics)  

## 1\. Reaching IK  

end effector  

position control  

### 1-1\. Two Joints IK  

### 1-2\. Three Joints IK  

### 1-3\. CCD (Cyclical Coordinate Descent) IK  

```cpp  
static inline void XM_CALLCONV internal_ik_ccd_solver_iteration(float const in_gain,  DirectX::XMVECTOR in_target_position_model_space, uint32_t const in_chain_joint_count, DirectX::XMMATRIX *const inout_pose_model_space)
{
    // NOTE: the model space of all children of the end effector should also be marked as invalid

    assert(in_chain_joint_count >= 2);

    for (uint32_t current_joint_chain_index_plus_2 = in_chain_joint_count; current_joint_chain_index_plus_2 >= 2U; --current_joint_chain_index_plus_2)
    {
        DirectX::XMVECTOR end_effector_model_space_translation;
        {
            uint32_t const end_effector_chain_index = in_chain_joint_count - 1U;

            DirectX::XMVECTOR end_effector_model_space_scale;
            DirectX::XMVECTOR end_effector_model_space_rotation;
            bool directx_xm_matrix_decompose = DirectX::XMMatrixDecompose(&end_effector_model_space_scale, &end_effector_model_space_rotation, &end_effector_model_space_translation, inout_pose_model_space[end_effector_chain_index]);
            assert(directx_xm_matrix_decompose);

            constexpr float const INTERNAL_SCALE_EPSILON = 7E-5F;
            assert(DirectX::XMVector3EqualInt(DirectX::XMVectorTrueInt(), DirectX::XMVectorLess(DirectX::XMVectorAbs(DirectX::XMVectorSubtract(end_effector_model_space_scale, DirectX::XMVectorSplatOne())), DirectX::XMVectorReplicate(INTERNAL_SCALE_EPSILON))));
        }

        uint32_t const current_joint_chain_index = current_joint_chain_index_plus_2 - 2U;

        DirectX::XMVECTOR current_joint_model_space_rotation;
        DirectX::XMVECTOR current_joint_model_space_translation;
        {
            DirectX::XMVECTOR current_joint_model_space_scale;
            bool directx_xm_matrix_decompose = DirectX::XMMatrixDecompose(&current_joint_model_space_scale, &current_joint_model_space_rotation, &current_joint_model_space_translation, inout_pose_model_space[current_joint_chain_index]);
            assert(directx_xm_matrix_decompose);

            constexpr float const INTERNAL_SCALE_EPSILON = 7E-5F;
            assert(DirectX::XMVector3EqualInt(DirectX::XMVectorTrueInt(), DirectX::XMVectorLess(DirectX::XMVectorAbs(DirectX::XMVectorSubtract(current_joint_model_space_scale, DirectX::XMVectorSplatOne())), DirectX::XMVectorReplicate(INTERNAL_SCALE_EPSILON))));
        }

        DirectX::XMVECTOR current_model_space_direction = DirectX::XMVector3Normalize(DirectX::XMVectorSubtract(end_effector_model_space_translation, current_joint_model_space_translation));

        DirectX::XMVECTOR target_model_space_direction = DirectX::XMVector3Normalize(DirectX::XMVectorSubtract(in_target_position_model_space, current_joint_model_space_translation));

        DirectX::XMVECTOR from_current_to_target_model_space_rotation = internal_compute_shortest_rotation_damped(current_model_space_direction, target_model_space_direction, in_gain);

        for (uint32_t child_joint_chain_index_plus_2 = (in_chain_joint_count + 1U); child_joint_chain_index_plus_2 >= (current_joint_chain_index_plus_2 + 1U); --child_joint_chain_index_plus_2)
        {
            uint32_t const parent_joint_chain_index = child_joint_chain_index_plus_2 - 2U - 1U;
            uint32_t const child_joint_chain_index = child_joint_chain_index_plus_2 - 2U;
            DirectX::XMVECTOR unused_determinant;
            DirectX::XMMATRIX child_joint_local_space = DirectX::XMMatrixMultiply(inout_pose_model_space[child_joint_chain_index], DirectX::XMMatrixInverse(&unused_determinant, inout_pose_model_space[parent_joint_chain_index]));
            // store temp local space matrix
            inout_pose_model_space[child_joint_chain_index] = child_joint_local_space;
        }

        DirectX::XMVECTOR updated_current_joint_model_space_rotation = DirectX::XMQuaternionNormalize(DirectX::XMQuaternionMultiply(current_joint_model_space_rotation, from_current_to_target_model_space_rotation));

        inout_pose_model_space[current_joint_chain_index] = DirectX::XMMatrixMultiply(DirectX::XMMatrixRotationQuaternion(updated_current_joint_model_space_rotation), DirectX::XMMatrixTranslationFromVector(current_joint_model_space_translation));

        for (uint32_t child_joint_chain_index_plus_2 = (current_joint_chain_index_plus_2 + 1U); child_joint_chain_index_plus_2 < (in_chain_joint_count + 2U); ++child_joint_chain_index_plus_2)
        {
            uint32_t const parent_joint_chain_index = child_joint_chain_index_plus_2 - 2U - 1U;
            uint32_t const child_joint_chain_index = child_joint_chain_index_plus_2 - 2U;
            DirectX::XMMATRIX child_joint_local_space = inout_pose_model_space[child_joint_chain_index];
            inout_pose_model_space[child_joint_chain_index] = DirectX::XMMatrixMultiply(child_joint_local_space, inout_pose_model_space[parent_joint_chain_index]);
        }
    }
}
```  

```cpp  
static inline DirectX::XMVECTOR XM_CALLCONV internal_compute_shortest_rotation_damped(DirectX::XMVECTOR from, DirectX::XMVECTOR to, float gain)
{
    constexpr float const one = 1.0F;
    constexpr float const half = 0.5F;
    constexpr float const zero = 0.0F;
    constexpr float const epsilon = 1E-6F;
    constexpr float const nearly_one = one - epsilon;

    // cos(theta)
    float const dot_product = DirectX::XMVectorGetX(DirectX::XMVector3Dot(from, to));

    float const damped_dot = one - gain + gain * dot_product;

    float const cos_theta_div_2_square = (damped_dot + one) * half;

    if (cos_theta_div_2_square > zero && dot_product >= -nearly_one && dot_product <= nearly_one)
    {
        // cos(theta/2) = sqrt((1+cos(theta))/2)
        float cos_theta_div_2 = std::sqrt(cos_theta_div_2_square);

        // sin(theta)
        DirectX::XMVECTOR cross = DirectX::XMVector3Cross(from, to);

        // sin(theta/2) = sin(theta)/(2*cos(theta/2))
        DirectX::XMVECTOR sin_theta_div_2 = DirectX::XMVectorScale(cross, ((gain * half) / cos_theta_div_2));

        return DirectX::XMQuaternionNormalize(DirectX::XMVectorSetW(sin_theta_div_2, cos_theta_div_2));
    }
    else if (cos_theta_div_2_square > zero && dot_product > nearly_one)
    {
        return DirectX::XMQuaternionIdentity();
    }
    else
    {
        return DirectX::XMVectorSetW(DirectX::XMVector3Normalize(internal_calculate_perpendicular_vector(from)), 0.0F);
    }
}
```  

```cpp  
static inline DirectX::XMVECTOR XM_CALLCONV internal_calculate_perpendicular_vector(DirectX::XMVECTOR simd_in_v)
{
    int min = 0;
    int ok1 = 1;
    int ok2 = 2;

    float in_v[3];
    DirectX::XMStoreFloat3(reinterpret_cast<DirectX::XMFLOAT3 *>(&in_v[0]), simd_in_v);

    float a0 = in_v[0];
    float a1 = in_v[1];
    float a2 = in_v[2];

    if (a1 < a0)
    {
        ok1 = 0;
        min = 1;
        a0 = a1;
    }

    if (a2 < a0)
    {
        ok2 = min;
        min = 2;
    }

    float out_v[3] = {0.0F, 0.0F, 0.0F};
    out_v[ok1] = in_v[ok2];
    out_v[ok2] = -in_v[ok1];
    return DirectX::XMLoadFloat3(reinterpret_cast<DirectX::XMFLOAT3 *>(&out_v[0]));
}
```  

### 1-4\. FABIK  

### 1-5\. Biped Foot IK  

sample animation ->  

### 1-6\. Quadruped Foot IK  

#### 1-6-1\. Linear Regression    

optimal plane  

OLS(Ordinary Least Squares)  

Normal Equations  

// Assume +Z Up  
// Ax + By + Cz + D = 0 => z = (-(A/C))x + (-(B/C))y + (-(D/C))  

```cpp
DirectX::XMFLOAT4 inline plane_train(DirectX::XMFLOAT3 const& p0, DirectX::XMFLOAT3 const& p1, DirectX::XMFLOAT3 const& p2, DirectX::XMFLOAT3 const& p3)
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
float inline plane_inference(DirectX::XMFLOAT4 const& normalized_plane, DirectX::XMFLOAT2 const& p_xy)
{
    DirectX::XMFLOAT3A coefficients(-(normalized_plane.x / normalized_plane.z), -(normalized_plane.y / normalized_plane.z), -(normalized_plane.w / normalized_plane.z));

    DirectX::XMVECTOR simd_beta = DirectX::XMLoadFloat3A(&coefficients);

    DirectX::XMFLOAT3A target_and_intercept(p_xy.x, p_xy.y, 1.0F);
    DirectX::XMVECTOR simd_target = DirectX::XMLoadFloat3A(&target_and_intercept);

    float prediction = DirectX::XMVectorGetX(DirectX::XMVector3Dot(simd_beta, simd_target));
    return prediction;
}
```

## 2\. Look At IK  

end effector  

orientation control  

