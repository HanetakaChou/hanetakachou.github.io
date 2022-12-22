## HiZ  

The Z buffer is splitted into serveral tiles and the HiZ(Hierarchical Z) buffer can be considered as an outline of a tile inside the Z buffer.  

The HiZ buffer consists of a "z_tile_nearest" value and a "z_tile_farthest" value. And the "z_tile_nearest" is exactly the nearest Z value of the corresponding tile while the "z_tile_farthest" may be equal or farther than the farthest Z value of the corresponding tile due to the fact that there is currently no efficient method to keep the "z_tile_farthest" equal to the farthest Z value of the tile.   

The aim of the HiZ buffer is to skip the full z buffer test to improve the performance and there are three potential outcomes of the HiZ test: fail("z_tile_farthest" nearer than "z_tri_nearest"), pass("z_tri_farthest" nearer than "z_tile_nearest") and ambiguous(neither fail or pass). Evidently, both "fail" and "pass" outcomes skip the full z buffer test and the ambiguous outcome should be decreased to improve the performance.

And the "z_tile_nearest" can be efficiently updated as "z_tile_nearest = nearest(z_tri_nearest, z_tile_nearest)". However, the "z_tile_farthest" can NOT be efficiently updated as "z_tile_farthest = nearest(z_tri_farthest, z_tile_farthest)" even if the outcome is "pass" since the "z_tri_farthest" and "z_tile_farthest" may be not at the same sample of the Z buffer. Acutally, the "z_tile_farthest" can only be efficiently updated when the tile is completely overlapped by the triangle. Hence, the "fail" outcome is conservative since the "z_tile_farthest" may be farther than the farthest Z value of the corresponding tile. Thus, the slower delayed "feedback update", which is to be removed by 1\.\[Andersson 2015\], is currently required to make the "z_tile_farthest" more precise.  

The main idea of "1\.\[Andersson 2015\]" is to use the "tile_selection_mask" to split the tile into two layers. Each layer has its own "z_layer_farthest" and the "z_tile_farthest" is replaced. And the HiZ test is performed based on the layer rather than the tile.  

Evidently, for a single sample, there is no "ambiguous" outcome, only "pass" or "fail". A tile is considered as "ambiguous" only when it contains both the "pass" and "fail" samples. In my opinion, since the size of the layer is smaller than the tile, the potential that the layer contains both the "pass" and "fail" samples decreases. Thus, the "ambiguous" outcome, which is NOT friendly for the performance, is decreased. And the layer is more likely to be completely overlapped by the triangle than the tile. Hence, the "z_layer_farthest" is more likely to be efficiently updated than the "z_tile_farthest".  

The underlying assumption of the "two" layers is that the same layer is expected to represent the same surface. For example, the Z buffer may represent a "roof" before the "sky". And ideally, the "tile_selection_mask" should make sure that one layer represents the "roof" and the other layer represents the "sky". Thus, even if the "z_layer_farthest" is conservatively updated as "z_layer_farthest = farthest(z_tri_farthest, z_layer_farthest)" for each layer, the precision is acceptable since both "z_tri_farthest" and "z_layer_farthest" represent the same surface.  

```cpp
masked_coarse_depth_test()
{
    tri_pass_mask = nearer(z_tri_nearerest, z_layer_nearerest);

    tri_fail_mask0 = farther_or_equal(z_tri_farthest, z_layer0_farthest) ? tri_rast_mask & ˜tile_selection_mask : 0;
    tri_fail_mask1 = farther_or_equal(z_tri_farthest, z_layer1_farthest) ? tri_rast_mask & tile_selection_mask : 0;  
    tri_fail_mask = tri_fail_mask0 | tri_fail_mask1;

    return {tri_pass_mask, tri_fail_mask};
}
```

```cpp
masked_hiz_update()
{
    // The "z_tile_nearest" can always be efficiently updated
    // z_tile_nearest = nearest(z_tri_nearest, z_tile_nearest)

    tri_non_fail_mask0 = nearer(z_tri_farthest, z_layer0_farthest) ? tri_rast_mask & ˜tile_selection_mask : 0;
    tri_non_fail_mask1 = nearer(z_tri_farthest, z_layer1_farthest) ? tri_rast_mask & tile_selection_mask : 0;
    tri_mask = tri_non_fail_mask0 | tri_non_fail_mask1;

    // Since the size of the layer is smaller than the tile, the layer is more likely to be completely overlapped by the triangle than the tile, and thus the "z_layer_farthest" is more likely to be efficiently updated than the "z_tile_farthest".  
    layer0_mask = ˜tile_selection_mask & ˜tri_mask;
    layer1_mask = tile_selection_mask & ˜tri_mask;

    if(0 != tri_mask)
    {
        // Layer0 is completely overlapped by the triangle and thus can be efficiently updated.
        if(0 == layer0_mask)
        {
            z_layer0_farthest = z_tri_farthest;
            tile_selection_mask = ˜tri_mask;
        }
        // Layer0 is completely overlapped by the triangle and thus can be efficiently updated.
        else if(1 == layer1_mask)
        {
            z_layer1_farthest = z_tri_farthest;
            tile_selection_mask = tri_mask;   
        }
        // The shortest distance is used to determine which merge operation is performed.
        else
        {
            // distance-based heuristic merge
            // ... 
        }
    }
}
```

## MOC  
TODO

1\.\[Andersson 2015\] [Magnus Andersson, Jon Hasselgren, Tomas Akenine-Moller. "Masked Depth Culling for Graphics Hardware." SIGGRAPH 2015.](https://fileadmin.cs.lth.se/graphics/research/papers/2015/ZMM/)  
