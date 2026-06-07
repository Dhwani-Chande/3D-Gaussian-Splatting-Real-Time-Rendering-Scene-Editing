# Results

Rendered outputs from all three methods, organized by method and scene.

---

## Folder Structure

```
results/
├── paper1_3dgs/
│   ├── garden/                  # MipNeRF360 benchmark scene
│   └── my_scene/                # Own captured desk scene
├── paper2_mip_splatting/
│   ├── garden/                  # MipNeRF360 benchmark scene
│   └── my_scene/                # Own captured desk scene
├── paper3_gaussian_grouping/    # Gaussian Grouping outputs
└── comparisons/                 # Side-by-side renders across methods
```

---

## Quantitative Results

Evaluated on the MipNeRF360 garden scene:

| Method | PSNR ↑ | SSIM ↑ | LPIPS ↓ |
|--------|--------|--------|---------|
| 3DGS (7k iter) | 21.13 | 0.7016 | 0.2439 |
| Mip-Splatting (7k iter) | 28.09 | 0.8957 | 0.0877 |

---

## Qualitative Results

`garden/` — renders on the MipNeRF360 benchmark, used for quantitative comparison.

`my_scene/` — renders on a self-captured desk scene, processed via iPhone video → COLMAP → training pipeline.

`comparisons/` — side-by-side renders between 3DGS and Mip-Splatting at multiple resolution scales, highlighting aliasing behavior differences.
