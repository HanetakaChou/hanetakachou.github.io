# IK (Inverse Kinematics)  

## 1\. Reaching IK  

end effector  

position control  

### 1-1\. Two Joints IK  

```cpp  
extern void ik_two_joints_solve(float const in_ball_and_socket_joint_gain, DirectX::XMFLOAT3 const &in_hinge_joint_axis_local_space, float const in_cosine_max_hinge_joint_angle, float const in_cosine_min_hinge_joint_angle, float const in_hinge_joint_gain, DirectX::XMFLOAT3 const &in_target_position_model_space, DirectX::XMFLOAT4X4 const &in_end_effector_transform_local_space, DirectX::XMFLOAT4X4 *const inout_joints_local_space, DirectX::XMFLOAT4X4 *const inout_joints_model_space)
{
    constexpr uint32_t const ball_and_socket_joint_index = 0U;
    constexpr uint32_t const hinge_joint_index = 1U;
    constexpr uint32_t const end_effector_parent_joint_index = 1U;

    constexpr float const INTERNAL_SCALE_EPSILON = 9E-5F;
    constexpr float const INTERNAL_TRANSLATION_EPSILON = 7E-5F;

    DirectX::XMMATRIX ball_and_socket_parent_transform_model_space;
    {
        DirectX::XMVECTOR unused_determinant;
        ball_and_socket_parent_transform_model_space = DirectX::XMMatrixMultiply(DirectX::XMMatrixInverse(&unused_determinant, DirectX::XMLoadFloat4x4(&inout_joints_local_space[ball_and_socket_joint_index])), DirectX::XMLoadFloat4x4(&inout_joints_model_space[ball_and_socket_joint_index]));
    }

    DirectX::XMVECTOR ball_and_socket_joint_model_space_translation;
    DirectX::XMVECTOR ball_and_socket_joint_model_space_rotation;
    {
        DirectX::XMMATRIX ball_and_socket_joint_transform_model_space = DirectX::XMLoadFloat4x4(&inout_joints_model_space[ball_and_socket_joint_index]);

        DirectX::XMVECTOR ball_and_socket_joint_model_space_scale;
        bool directx_xm_matrix_decompose = DirectX::XMMatrixDecompose(&ball_and_socket_joint_model_space_scale, &ball_and_socket_joint_model_space_rotation, &ball_and_socket_joint_model_space_translation, ball_and_socket_joint_transform_model_space);
        assert(directx_xm_matrix_decompose);

        assert(DirectX::XMVector3EqualInt(DirectX::XMVectorTrueInt(), DirectX::XMVectorLess(DirectX::XMVectorAbs(DirectX::XMVectorSubtract(ball_and_socket_joint_model_space_scale, DirectX::XMVectorSplatOne())), DirectX::XMVectorReplicate(INTERNAL_SCALE_EPSILON))));
    }

    DirectX::XMVECTOR from_ball_and_socket_joint_to_target_model_space_translation = DirectX::XMVectorSubtract(DirectX::XMLoadFloat3(&in_target_position_model_space), ball_and_socket_joint_model_space_translation);

    {
        DirectX::XMVECTOR hinge_joint_model_space_translation;
        DirectX::XMVECTOR hinge_joint_model_space_rotation;
        DirectX::XMVECTOR hinge_joint_axis_model_space;
        {
            DirectX::XMMATRIX hinge_joint_transform_model_space = DirectX::XMLoadFloat4x4(&inout_joints_model_space[hinge_joint_index]);

            DirectX::XMVECTOR hinge_joint_model_space_scale;
            bool directx_xm_matrix_decompose = DirectX::XMMatrixDecompose(&hinge_joint_model_space_scale, &hinge_joint_model_space_rotation, &hinge_joint_model_space_translation, hinge_joint_transform_model_space);
            assert(directx_xm_matrix_decompose);

            assert(DirectX::XMVector3EqualInt(DirectX::XMVectorTrueInt(), DirectX::XMVectorLess(DirectX::XMVectorAbs(DirectX::XMVectorSubtract(hinge_joint_model_space_scale, DirectX::XMVectorSplatOne())), DirectX::XMVectorReplicate(INTERNAL_SCALE_EPSILON))));

            DirectX::XMVECTOR hinge_joint_axis_local_space = DirectX::XMLoadFloat3(&in_hinge_joint_axis_local_space);

            hinge_joint_axis_model_space = DirectX::XMVector3Normalize(DirectX::XMVector3TransformNormal(hinge_joint_axis_local_space, hinge_joint_transform_model_space));
        }

        DirectX::XMVECTOR different_hinge_joint_model_space_rotation;
        {
            DirectX::XMVECTOR end_effector_model_space_translation;
            {
                DirectX::XMMATRIX end_effector_transform_model_space = DirectX::XMMatrixMultiply(DirectX::XMLoadFloat4x4(&in_end_effector_transform_local_space), DirectX::XMLoadFloat4x4(&inout_joints_model_space[end_effector_parent_joint_index]));

                DirectX::XMVECTOR end_effector_model_space_scale;
                DirectX::XMVECTOR end_effector_model_space_rotation;
                bool directx_xm_matrix_decompose = DirectX::XMMatrixDecompose(&end_effector_model_space_scale, &end_effector_model_space_rotation, &end_effector_model_space_translation, end_effector_transform_model_space);
                assert(directx_xm_matrix_decompose);

                assert(DirectX::XMVector3EqualInt(DirectX::XMVectorTrueInt(), DirectX::XMVectorLess(DirectX::XMVectorAbs(DirectX::XMVectorSubtract(end_effector_model_space_scale, DirectX::XMVectorSplatOne())), DirectX::XMVectorReplicate(INTERNAL_SCALE_EPSILON))));
            }

            DirectX::XMVECTOR v1 = DirectX::XMVectorSubtract(ball_and_socket_joint_model_space_translation, hinge_joint_model_space_translation);

            DirectX::XMVECTOR v1_in_normal = DirectX::XMVectorScale(hinge_joint_axis_model_space, DirectX::XMVectorGetX(DirectX::XMVector3Dot(v1, hinge_joint_axis_model_space)));

            DirectX::XMVECTOR v1_in_plane = DirectX::XMVectorSubtract(v1, v1_in_normal);

            float v1_in_plane_length_square = DirectX::XMVectorGetX(DirectX::XMVector3Dot(v1_in_plane, v1_in_plane));

            float v1_in_plane_length = internal_sqrt(v1_in_plane_length_square);

            DirectX::XMVECTOR v2 = DirectX::XMVectorSubtract(end_effector_model_space_translation, hinge_joint_model_space_translation);

            DirectX::XMVECTOR v2_in_normal = DirectX::XMVectorScale(hinge_joint_axis_model_space, DirectX::XMVectorGetX(DirectX::XMVector3Dot(v2, hinge_joint_axis_model_space)));

            DirectX::XMVECTOR v2_in_plane = DirectX::XMVectorSubtract(v2, v2_in_normal);

            float v2_in_plane_length_square = DirectX::XMVectorGetX(DirectX::XMVector3Dot(v2_in_plane, v2_in_plane));

            float v2_in_plane_length = internal_sqrt(v2_in_plane_length_square);

            DirectX::XMVECTOR h_in_normal = DirectX::XMVectorSubtract(v2_in_normal, v1_in_normal);

            float h_in_normal_length_square = DirectX::XMVectorGetX(DirectX::XMVector3Dot(h_in_normal, h_in_normal));

            float d_length_square = DirectX::XMVectorGetX(DirectX::XMVector3Dot(from_ball_and_socket_joint_to_target_model_space_translation, from_ball_and_socket_joint_to_target_model_space_translation));

            float d_in_plane_length_square = d_length_square - h_in_normal_length_square;

            float cos_v1_v2_in_plane = (v1_in_plane_length_square + v2_in_plane_length_square - d_in_plane_length_square) * 0.5F / (v1_in_plane_length * v2_in_plane_length);

            assert(in_cosine_max_hinge_joint_angle < in_cosine_min_hinge_joint_angle);
            assert(in_cosine_max_hinge_joint_angle >= -1.0F);
            assert(in_cosine_max_hinge_joint_angle <= 1.0F);
            assert(in_cosine_min_hinge_joint_angle >= -1.0F);
            assert(in_cosine_min_hinge_joint_angle <= 1.0F);
            float cos_updated = std::min(std::max(in_cosine_max_hinge_joint_angle, cos_v1_v2_in_plane), in_cosine_min_hinge_joint_angle);

            float cos_current = DirectX::XMVectorGetX(DirectX::XMVector3Dot(v1_in_plane, v2_in_plane)) / (v1_in_plane_length * v2_in_plane_length);

            assert(DirectX::XMVectorGetX(DirectX::XMVector3Dot(DirectX::XMVector3Normalize(DirectX::XMVector3Cross(v1_in_plane, v2_in_plane)), hinge_joint_axis_model_space)) > (1.0F - 1E-6F));

            float cos_different;
            float sin_different;
            {
                float const cos_b = cos_updated;
                float const cos_a = cos_current;

                float sin_b_sqr = 1.0F - cos_b * cos_b;
                float sin_a_sqr = 1.0F - cos_a * cos_a;

                float sin_b = internal_sqrt(sin_b_sqr);
                float sin_a = internal_sqrt(sin_a_sqr);

                float cos_b_a = cos_b * cos_a + sin_b * sin_a;
                float sin_b_a = sin_b * cos_a - sin_a * cos_b;

                cos_different = cos_b_a;
                sin_different = sin_b_a;
            }

            assert(in_hinge_joint_gain >= 0.0F);
            assert(in_hinge_joint_gain <= 1.0F);
            different_hinge_joint_model_space_rotation = internal_compute_rotation_axis_damped(hinge_joint_axis_model_space, cos_different, sin_different, in_hinge_joint_gain);
        }

        DirectX::XMVECTOR updated_hinge_joint_model_space_rotation = DirectX::XMQuaternionNormalize(DirectX::XMQuaternionMultiply(hinge_joint_model_space_rotation, different_hinge_joint_model_space_rotation));

        DirectX::XMMATRIX updated_hinge_joint_model_space_transform = DirectX::XMMatrixMultiply(DirectX::XMMatrixRotationQuaternion(updated_hinge_joint_model_space_rotation), DirectX::XMMatrixTranslationFromVector(hinge_joint_model_space_translation));

        DirectX::XMStoreFloat4x4(&inout_joints_model_space[hinge_joint_index], updated_hinge_joint_model_space_transform);

        DirectX::XMVECTOR hinge_joint_local_space_translation;
        {
            DirectX::XMVECTOR hinge_joint_local_space_scale;
            DirectX::XMVECTOR hinge_joint_local_space_rotation;
            bool directx_xm_matrix_decompose = DirectX::XMMatrixDecompose(&hinge_joint_local_space_scale, &hinge_joint_local_space_rotation, &hinge_joint_local_space_translation, DirectX::XMLoadFloat4x4(&inout_joints_local_space[hinge_joint_index]));
            assert(directx_xm_matrix_decompose);

            assert(DirectX::XMVector3EqualInt(DirectX::XMVectorTrueInt(), DirectX::XMVectorLess(DirectX::XMVectorAbs(DirectX::XMVectorSubtract(hinge_joint_local_space_scale, DirectX::XMVectorSplatOne())), DirectX::XMVectorReplicate(INTERNAL_SCALE_EPSILON))));
        }

        DirectX::XMVECTOR updated_hinge_joint_local_space_rotation;
        {
            DirectX::XMMATRIX ball_and_socket_joint_transform_model_space = DirectX::XMLoadFloat4x4(&inout_joints_model_space[ball_and_socket_joint_index]);

            DirectX::XMVECTOR unused_determinant;
            DirectX::XMMATRIX unused_updated_hinge_joint_local_space_transform = DirectX::XMMatrixMultiply(updated_hinge_joint_model_space_transform, DirectX::XMMatrixInverse(&unused_determinant, ball_and_socket_joint_transform_model_space));

            DirectX::XMVECTOR updated_hinge_joint_local_space_scale;
            DirectX::XMVECTOR updated_hinge_joint_local_space_translation;
            bool directx_xm_matrix_decompose = DirectX::XMMatrixDecompose(&updated_hinge_joint_local_space_scale, &updated_hinge_joint_local_space_rotation, &updated_hinge_joint_local_space_translation, unused_updated_hinge_joint_local_space_transform);
            assert(directx_xm_matrix_decompose);

            assert(DirectX::XMVector3EqualInt(DirectX::XMVectorTrueInt(), DirectX::XMVectorLess(DirectX::XMVectorAbs(DirectX::XMVectorSubtract(updated_hinge_joint_local_space_scale, DirectX::XMVectorSplatOne())), DirectX::XMVectorReplicate(INTERNAL_SCALE_EPSILON))));

            constexpr float const INTERNAL_TRANSLATION_EPSILON = 7E-5F;
            assert(DirectX::XMVector3EqualInt(DirectX::XMVectorTrueInt(), DirectX::XMVectorLess(DirectX::XMVectorAbs(DirectX::XMVectorSubtract(updated_hinge_joint_local_space_translation, hinge_joint_local_space_translation)), DirectX::XMVectorReplicate(INTERNAL_TRANSLATION_EPSILON))));
        }

        DirectX::XMMATRIX updated_hinge_joint_local_space_transform = DirectX::XMMatrixMultiply(DirectX::XMMatrixRotationQuaternion(updated_hinge_joint_local_space_rotation), DirectX::XMMatrixTranslationFromVector(hinge_joint_local_space_translation));

        DirectX::XMStoreFloat4x4(&inout_joints_local_space[hinge_joint_index], updated_hinge_joint_local_space_transform);
    }

    {
        DirectX::XMVECTOR from_end_effector_to_target_model_space_rotation;
        {
            DirectX::XMVECTOR end_effector_model_space_translation;
            {
                DirectX::XMMATRIX end_effector_transform_model_space = DirectX::XMMatrixMultiply(DirectX::XMLoadFloat4x4(&in_end_effector_transform_local_space), DirectX::XMLoadFloat4x4(&inout_joints_model_space[end_effector_parent_joint_index]));

                DirectX::XMVECTOR end_effector_model_space_scale;
                DirectX::XMVECTOR end_effector_model_space_rotation;
                bool directx_xm_matrix_decompose = DirectX::XMMatrixDecompose(&end_effector_model_space_scale, &end_effector_model_space_rotation, &end_effector_model_space_translation, end_effector_transform_model_space);
                assert(directx_xm_matrix_decompose);

                assert(DirectX::XMVector3EqualInt(DirectX::XMVectorTrueInt(), DirectX::XMVectorLess(DirectX::XMVectorAbs(DirectX::XMVectorSubtract(end_effector_model_space_scale, DirectX::XMVectorSplatOne())), DirectX::XMVectorReplicate(INTERNAL_SCALE_EPSILON))));
            }

            DirectX::XMVECTOR end_effector_model_space_direction = DirectX::XMVector3Normalize(DirectX::XMVectorSubtract(end_effector_model_space_translation, ball_and_socket_joint_model_space_translation));

            DirectX::XMVECTOR target_model_space_direction = DirectX::XMVector3Normalize(DirectX::XMVectorSubtract(DirectX::XMLoadFloat3(&in_target_position_model_space), ball_and_socket_joint_model_space_translation));

            assert(in_ball_and_socket_joint_gain >= 0.0F);
            assert(in_ball_and_socket_joint_gain <= 1.0F);
            from_end_effector_to_target_model_space_rotation = internal_compute_shortest_rotation_damped(end_effector_model_space_direction, target_model_space_direction, in_ball_and_socket_joint_gain);
        }

        DirectX::XMVECTOR updated_ball_and_socket_joint_model_space_rotation = DirectX::XMQuaternionNormalize(DirectX::XMQuaternionMultiply(ball_and_socket_joint_model_space_rotation, from_end_effector_to_target_model_space_rotation));

        DirectX::XMMATRIX updated_ball_and_socket_joint_model_space_transform = DirectX::XMMatrixMultiply(DirectX::XMMatrixRotationQuaternion(updated_ball_and_socket_joint_model_space_rotation), DirectX::XMMatrixTranslationFromVector(ball_and_socket_joint_model_space_translation));

        DirectX::XMStoreFloat4x4(&inout_joints_model_space[ball_and_socket_joint_index], updated_ball_and_socket_joint_model_space_transform);

        DirectX::XMVECTOR ball_and_socket_joint_local_space_translation;
        {
            DirectX::XMVECTOR ball_and_socket_joint_local_space_scale;
            DirectX::XMVECTOR ball_and_socket_joint_local_space_rotation;
            bool directx_xm_matrix_decompose = DirectX::XMMatrixDecompose(&ball_and_socket_joint_local_space_scale, &ball_and_socket_joint_local_space_rotation, &ball_and_socket_joint_local_space_translation, DirectX::XMLoadFloat4x4(&inout_joints_local_space[ball_and_socket_joint_index]));
            assert(directx_xm_matrix_decompose);

            assert(DirectX::XMVector3EqualInt(DirectX::XMVectorTrueInt(), DirectX::XMVectorLess(DirectX::XMVectorAbs(DirectX::XMVectorSubtract(ball_and_socket_joint_local_space_scale, DirectX::XMVectorSplatOne())), DirectX::XMVectorReplicate(INTERNAL_SCALE_EPSILON))));
        }

        DirectX::XMVECTOR updated_ball_and_socket_joint_local_space_rotation;
        {
            DirectX::XMVECTOR unused_determinant;
            DirectX::XMMATRIX unused_updated_ball_and_socket_joint_local_space_transform = DirectX::XMMatrixMultiply(updated_ball_and_socket_joint_model_space_transform, DirectX::XMMatrixInverse(&unused_determinant, ball_and_socket_parent_transform_model_space));

            DirectX::XMVECTOR updated_ball_and_socket_joint_local_space_scale;
            DirectX::XMVECTOR updated_ball_and_socket_joint_local_space_translation;
            bool directx_xm_matrix_decompose = DirectX::XMMatrixDecompose(&updated_ball_and_socket_joint_local_space_scale, &updated_ball_and_socket_joint_local_space_rotation, &updated_ball_and_socket_joint_local_space_translation, unused_updated_ball_and_socket_joint_local_space_transform);
            assert(directx_xm_matrix_decompose);

            assert(DirectX::XMVector3EqualInt(DirectX::XMVectorTrueInt(), DirectX::XMVectorLess(DirectX::XMVectorAbs(DirectX::XMVectorSubtract(updated_ball_and_socket_joint_local_space_scale, DirectX::XMVectorSplatOne())), DirectX::XMVectorReplicate(INTERNAL_SCALE_EPSILON))));

            assert(DirectX::XMVector3EqualInt(DirectX::XMVectorTrueInt(), DirectX::XMVectorLess(DirectX::XMVectorAbs(DirectX::XMVectorSubtract(updated_ball_and_socket_joint_local_space_translation, ball_and_socket_joint_local_space_translation)), DirectX::XMVectorReplicate(INTERNAL_TRANSLATION_EPSILON))));
        }

        DirectX::XMMATRIX updated_current_joint_local_space_transform = DirectX::XMMatrixMultiply(DirectX::XMMatrixRotationQuaternion(updated_ball_and_socket_joint_local_space_rotation), DirectX::XMMatrixTranslationFromVector(ball_and_socket_joint_local_space_translation));

        DirectX::XMStoreFloat4x4(&inout_joints_local_space[ball_and_socket_joint_index], updated_current_joint_local_space_transform);

        DirectX::XMStoreFloat4x4(&inout_joints_model_space[hinge_joint_index], DirectX::XMMatrixMultiply(DirectX::XMLoadFloat4x4(&inout_joints_local_space[hinge_joint_index]), DirectX::XMLoadFloat4x4(&inout_joints_model_space[ball_and_socket_joint_index])));
    }
}
```  

### 1-2\. Three Joints IK  

### 1-3\. CCD (Cyclical Coordinate Descent) IK  

```cpp
extern void ik_ccd_solve(uint32_t const in_iteration, float const in_gain, DirectX::XMFLOAT3 const &in_target_position_model_space, DirectX::XMFLOAT4X4 const &in_end_effector_transform_local_space, uint32_t const in_joint_count, DirectX::XMFLOAT4X4 *const inout_joints_local_space, DirectX::XMFLOAT4X4 *const inout_joints_model_space)
{
    DirectX::XMFLOAT4X4 in_base_parent_transform_model_space;
    assert(in_joint_count >= 1U);
    {
        DirectX::XMVECTOR unused_determinant;
        DirectX::XMStoreFloat4x4(&in_base_parent_transform_model_space, DirectX::XMMatrixMultiply(DirectX::XMMatrixInverse(&unused_determinant, DirectX::XMLoadFloat4x4(&inout_joints_local_space[0])), DirectX::XMLoadFloat4x4(&inout_joints_model_space[0])));
    }

    for (uint32_t iteration_index = 0U; iteration_index < in_iteration; ++iteration_index)
    {
        internal_ik_ccd_solve_iteration(in_gain, in_target_position_model_space, in_end_effector_transform_local_space, in_base_parent_transform_model_space, in_joint_count, inout_joints_local_space, inout_joints_model_space);
    }
}
```  

```cpp  
static inline void internal_ik_ccd_solve_iteration(float const in_gain, DirectX::XMFLOAT3 const &in_target_position_model_space, DirectX::XMFLOAT4X4 const &in_end_effector_transform_local_space, DirectX::XMFLOAT4X4 const &in_base_parent_transform_model_space, uint32_t const in_joint_count, DirectX::XMFLOAT4X4 *const inout_joints_local_space, DirectX::XMFLOAT4X4 *const inout_joints_model_space)
{
    for (uint32_t current_joint_chain_index_plus_1 = in_joint_count; current_joint_chain_index_plus_1 >= 1U; --current_joint_chain_index_plus_1)
    {
        uint32_t const current_joint_chain_index = current_joint_chain_index_plus_1 - 1U;

        DirectX::XMVECTOR current_joint_model_space_rotation;
        DirectX::XMVECTOR current_joint_model_space_translation;
        {
            DirectX::XMVECTOR current_joint_model_space_scale;
            bool directx_xm_matrix_decompose = DirectX::XMMatrixDecompose(&current_joint_model_space_scale, &current_joint_model_space_rotation, &current_joint_model_space_translation, DirectX::XMLoadFloat4x4(&inout_joints_model_space[current_joint_chain_index]));
            assert(directx_xm_matrix_decompose);

            constexpr float const INTERNAL_SCALE_EPSILON = 7E-5F;
            assert(DirectX::XMVector3EqualInt(DirectX::XMVectorTrueInt(), DirectX::XMVectorLess(DirectX::XMVectorAbs(DirectX::XMVectorSubtract(current_joint_model_space_scale, DirectX::XMVectorSplatOne())), DirectX::XMVectorReplicate(INTERNAL_SCALE_EPSILON))));
        }

        DirectX::XMVECTOR from_end_effector_to_target_model_space_rotation;
        {
            DirectX::XMVECTOR end_effector_model_space_translation;
            {
                uint32_t const end_effector_parent_chain_index = in_joint_count - 1U;

                DirectX::XMMATRIX in_end_effector_transform_model_space = DirectX::XMMatrixMultiply(DirectX::XMLoadFloat4x4(&in_end_effector_transform_local_space), DirectX::XMLoadFloat4x4(&inout_joints_model_space[end_effector_parent_chain_index]));

                DirectX::XMVECTOR end_effector_model_space_scale;
                DirectX::XMVECTOR end_effector_model_space_rotation;
                bool directx_xm_matrix_decompose = DirectX::XMMatrixDecompose(&end_effector_model_space_scale, &end_effector_model_space_rotation, &end_effector_model_space_translation, in_end_effector_transform_model_space);
                assert(directx_xm_matrix_decompose);

                constexpr float const INTERNAL_SCALE_EPSILON = 7E-5F;
                assert(DirectX::XMVector3EqualInt(DirectX::XMVectorTrueInt(), DirectX::XMVectorLess(DirectX::XMVectorAbs(DirectX::XMVectorSubtract(end_effector_model_space_scale, DirectX::XMVectorSplatOne())), DirectX::XMVectorReplicate(INTERNAL_SCALE_EPSILON))));
            }

            DirectX::XMVECTOR end_effector_model_space_direction = DirectX::XMVector3Normalize(DirectX::XMVectorSubtract(end_effector_model_space_translation, current_joint_model_space_translation));

            DirectX::XMVECTOR target_model_space_direction = DirectX::XMVector3Normalize(DirectX::XMVectorSubtract(DirectX::XMLoadFloat3(&in_target_position_model_space), current_joint_model_space_translation));

            from_end_effector_to_target_model_space_rotation = internal_compute_shortest_rotation_damped(end_effector_model_space_direction, target_model_space_direction, in_gain);
        }

        DirectX::XMVECTOR updated_current_joint_model_space_rotation = DirectX::XMQuaternionNormalize(DirectX::XMQuaternionMultiply(current_joint_model_space_rotation, from_end_effector_to_target_model_space_rotation));

        DirectX::XMMATRIX updated_current_joint_model_space_transform = DirectX::XMMatrixMultiply(DirectX::XMMatrixRotationQuaternion(updated_current_joint_model_space_rotation), DirectX::XMMatrixTranslationFromVector(current_joint_model_space_translation));

        DirectX::XMStoreFloat4x4(&inout_joints_model_space[current_joint_chain_index], updated_current_joint_model_space_transform);

        DirectX::XMVECTOR current_joint_local_space_translation;
        {
            DirectX::XMVECTOR current_joint_local_space_scale;
            DirectX::XMVECTOR current_joint_local_space_rotation;
            bool directx_xm_matrix_decompose = DirectX::XMMatrixDecompose(&current_joint_local_space_scale, &current_joint_local_space_rotation, &current_joint_local_space_translation, DirectX::XMLoadFloat4x4(&inout_joints_local_space[current_joint_chain_index]));
            assert(directx_xm_matrix_decompose);

            constexpr float const INTERNAL_SCALE_EPSILON = 7E-5F;
            assert(DirectX::XMVector3EqualInt(DirectX::XMVectorTrueInt(), DirectX::XMVectorLess(DirectX::XMVectorAbs(DirectX::XMVectorSubtract(current_joint_local_space_scale, DirectX::XMVectorSplatOne())), DirectX::XMVectorReplicate(INTERNAL_SCALE_EPSILON))));
        }

        DirectX::XMVECTOR updated_current_joint_local_space_rotation;
        {
            DirectX::XMMATRIX current_parent_joint_model_space = (current_joint_chain_index >= 1U) ? DirectX::XMLoadFloat4x4(&inout_joints_model_space[current_joint_chain_index - 1U]) : DirectX::XMLoadFloat4x4(&in_base_parent_transform_model_space);

            DirectX::XMVECTOR unused_determinant;

            DirectX::XMMATRIX unused_updated_current_joint_local_space_transform = DirectX::XMMatrixMultiply(updated_current_joint_model_space_transform, DirectX::XMMatrixInverse(&unused_determinant, current_parent_joint_model_space));

            DirectX::XMVECTOR updated_current_joint_local_space_scale;
            DirectX::XMVECTOR updated_current_joint_local_space_translation;
            bool directx_xm_matrix_decompose = DirectX::XMMatrixDecompose(&updated_current_joint_local_space_scale, &updated_current_joint_local_space_rotation, &updated_current_joint_local_space_translation, unused_updated_current_joint_local_space_transform);
            assert(directx_xm_matrix_decompose);

            constexpr float const INTERNAL_SCALE_EPSILON = 7E-5F;
            assert(DirectX::XMVector3EqualInt(DirectX::XMVectorTrueInt(), DirectX::XMVectorLess(DirectX::XMVectorAbs(DirectX::XMVectorSubtract(updated_current_joint_local_space_scale, DirectX::XMVectorSplatOne())), DirectX::XMVectorReplicate(INTERNAL_SCALE_EPSILON))));

            constexpr float const INTERNAL_TRANSLATION_EPSILON = 7E-5F;
            assert(DirectX::XMVector3EqualInt(DirectX::XMVectorTrueInt(), DirectX::XMVectorLess(DirectX::XMVectorAbs(DirectX::XMVectorSubtract(updated_current_joint_local_space_translation, current_joint_local_space_translation)), DirectX::XMVectorReplicate(INTERNAL_SCALE_EPSILON))));
        }

        DirectX::XMMATRIX updated_current_joint_local_space_transform = DirectX::XMMatrixMultiply(DirectX::XMMatrixRotationQuaternion(updated_current_joint_local_space_rotation), DirectX::XMMatrixTranslationFromVector(current_joint_local_space_translation));

        DirectX::XMStoreFloat4x4(&inout_joints_local_space[current_joint_chain_index], updated_current_joint_local_space_transform);

        for (uint32_t child_joint_chain_index_plus_1 = (current_joint_chain_index_plus_1 + 1U); child_joint_chain_index_plus_1 <= in_joint_count; ++child_joint_chain_index_plus_1)
        {
            uint32_t const parent_joint_chain_index = child_joint_chain_index_plus_1 - 1U - 1U;
            uint32_t const child_joint_chain_index = child_joint_chain_index_plus_1 - 1U;
            DirectX::XMStoreFloat4x4(&inout_joints_model_space[child_joint_chain_index], DirectX::XMMatrixMultiply(DirectX::XMLoadFloat4x4(&inout_joints_local_space[child_joint_chain_index]), DirectX::XMLoadFloat4x4(&inout_joints_model_space[parent_joint_chain_index])));
        }
    }
}
```  

### 1-4\. FABIK  

### 1-5\. Biped Foot IK  

sample animation -> ray cast ground  

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

