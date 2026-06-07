# 3D Gaussian Splatting: Real-Time Rendering & Scene Editing

**Team:** Dhwani Chande · Trong Gia Hung Nguyen · Nishita Konduru

---

## Overview

This project compares three Gaussian Splatting methods for novel view synthesis and 3D scene understanding:

| # | Paper | Venue | Key Contribution |
|---|-------|-------|-----------------|
| 1 | [3D Gaussian Splatting](https://arxiv.org/abs/2308.04079) — Kerbl et al. | SIGGRAPH 2023 | Foundational real-time radiance field rendering via explicit 3D Gaussians |
| 2 | [Mip-Splatting](https://arxiv.org/abs/2311.16493) — Yu et al. | CVPR 2024 | Anti-aliasing for 3DGS using 3D smoothing + 2D Mip filters |
| 3 | [Gaussian Grouping](https://arxiv.org/abs/2312.00732) — Ye et al. | ECCV 2024 | Per-Gaussian identity encoding for segmentation, editing, and removal |

All three methods share a common backbone, making them well-suited for direct comparison. Each paper makes a different design trade-off: rendering speed (3DGS), rendering quality (Mip-Splatting), and semantic understanding (Gaussian Grouping).

---

## Repository Structure

```
3D-Gaussian-Splatting-Real-Time-Rendering-Scene-Editing/
├── paper1_3dgs/              # 3D Gaussian Splatting experiments
├── paper2_mip_splatting/     # Mip-Splatting experiments
├── paper3_gaussian_grouping/ # Gaussian Grouping experiments
├── own_data/                 # Self-captured data and COLMAP scripts
├── results/                  # Rendered outputs organized by method and scene
│   ├── paper1_3dgs/
│   │   ├── garden/
│   │   └── my_scene/
│   ├── paper2_mip_splatting/
│   │   ├── garden/
│   │   └── my_scene/
│   ├── paper3_gaussian_grouping/
│   └── comparisons/
└── report/                   # Final PDF report
```

---

## Methods

### Paper 1 — 3D Gaussian Splatting (3DGS)
Represents a scene as a set of explicit 3D Gaussians, each with learnable position, covariance, opacity, and spherical harmonic color. Training uses differentiable tile-based rasterization and adaptive density control to add/remove Gaussians. Achieves real-time rendering (>100 FPS) at quality competitive with NeRF-based methods, while training in minutes rather than hours.

### Paper 2 — Mip-Splatting
Addresses a core limitation of vanilla 3DGS: aliasing artifacts when rendering at resolutions or camera distances not seen during training. Introduces a 3D smoothing filter to constrain Gaussian size relative to the camera's sampling rate, and a 2D Mip filter to replace the heuristic dilation used during rasterization. Controlled by a single `--antialiasing` flag at train/render time.

### Paper 3 — Gaussian Grouping
Extends 3DGS with a learnable identity encoding per Gaussian, supervised by 2D segmentation masks from the Segment Anything Model (SAM). This lifts SAM's 2D knowledge into 3D, enabling open-world object segmentation, removal, inpainting, recoloring, and scene recomposition without retraining the renderer.

---

## Compute Environment

All CUDA-dependent experiments were run on **Google Colab Pro** (T4 GPU, High RAM runtime).

| Tool | Notes |
|------|-------|
| Python 3.8 | via Conda |
| PyTorch | CUDA 11.8 build |
| COLMAP | Structure-from-Motion for own-data pipeline |
| SAM (ViT-H) | Gaussian Grouping only |

---

## Results Summary

Evaluated on the MipNeRF360 garden scene:

| Method | PSNR ↑ | SSIM ↑ | LPIPS ↓ |
|--------|--------|--------|---------|
| 3DGS (7k iter) | 21.13 | 0.7016 | 0.2439 |
| Mip-Splatting (7k iter) | 28.09 | 0.8957 | 0.0877 |


---

## Contributions

| Member | Contributions |
|--------|--------------|
| Dhwani Chande | Papers 1 & 2 implementation, own-data capture and pipeline, Mip-Splatting report section |
| Trong Gia Hung Nguyen | Paper 3 (Gaussian Grouping) implementation |
| Nishita Konduru | Report writing |

---

## References

- Kerbl et al., *3D Gaussian Splatting for Real-Time Radiance Field Rendering*, SIGGRAPH 2023
- Yu et al., *Mip-Splatting: Alias-free 3D Gaussian Splatting*, CVPR 2024
- Ye et al., *Gaussian Grouping: Segment and Edit Anything in 3D Scenes*, ECCV 2024
