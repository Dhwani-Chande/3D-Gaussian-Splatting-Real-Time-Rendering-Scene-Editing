# Paper 1 — 3D Gaussian Splatting

**Paper:** Kerbl et al., *3D Gaussian Splatting for Real-Time Radiance Field Rendering*, SIGGRAPH 2023
**Official repo:** https://github.com/graphdeco-inria/gaussian-splatting

---

## Setup

```bash
git clone https://github.com/graphdeco-inria/gaussian-splatting --recursive
cd gaussian-splatting
conda env create --file environment.yml
conda activate gaussian_splatting
```

> Requires NVIDIA GPU with CUDA 11.8. Experiments were run on Google Colab Pro (T4 GPU, High RAM).

---

## Training

```bash
python train.py -s <path_to_dataset>
```

Key output: a `point_cloud/` directory containing the trained `.ply` Gaussian model.

---

## Rendering

```bash
python render.py -m <path_to_trained_model>
```

---

## Evaluation

```bash
python metrics.py -m <path_to_trained_model>
```

Reports PSNR, SSIM, and LPIPS on the test split.

---

## Folder Contents

```
paper1_3dgs/
├── README.md           # This file
├── notebooks/
│   └── 3DGS_Final_v2.ipynb   # Full training + rendering pipeline (covers Papers 1 & 2)
└── src/
    ├── train.py
    └── render.py
```

---

## Notes

- Adaptive density control is the core training mechanism — Gaussians are added where gradients are large and pruned when opacity falls below threshold.
- The tile-based rasterizer is compiled as a CUDA extension — GPU is required.
- Pre-trained models are available from the official repo if you want to skip training.
