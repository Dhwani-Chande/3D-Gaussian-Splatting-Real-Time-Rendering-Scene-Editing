# Paper 2 — Mip-Splatting

**Paper:** Yu et al., *Mip-Splatting: Alias-free 3D Gaussian Splatting*, CVPR 2024 (Best Student Paper)
**Official repo:** https://github.com/autonomousvision/mip-splatting

---

## Setup

```bash
git clone https://github.com/autonomousvision/mip-splatting --recursive
cd mip-splatting
conda env create --file environment.yml
conda activate gaussian_splatting

pip install submodules/diff-gaussian-rasterization
pip install submodules/simple-knn
```

> Do not mix this rasterizer with the vanilla 3DGS install — they are incompatible.

---

## Training

```bash
# Mip-Splatting
python train.py -s <path_to_dataset> --antialiasing

# Vanilla 3DGS baseline for comparison
python train.py -s <path_to_dataset>
```

The only difference is the `--antialiasing` flag.

---

## Rendering

```bash
python render.py -m <path_to_trained_model> --antialiasing

# Render at a different scale than training to test aliasing robustness
python render.py -m <path_to_trained_model> --antialiasing --resolution 4
```

---

## Evaluation

```bash
python metrics.py -m <path_to_trained_model>
```

---

## Folder Contents

```
paper2_mip_splatting/
├── README.md           # This file
└── notebooks/
    └── 3DGS_Final_v2.ipynb   # Full training + rendering pipeline (covers Papers 1 & 2)
```

---

## Notes

- The 3D smoothing filter constrains each Gaussian's minimum size to the pixel footprint at training distance.
- The 2D Mip filter replaces the dilation heuristic in the vanilla 3DGS rasterizer.
- The quality gap over 3DGS widens significantly at unseen resolution scales.
