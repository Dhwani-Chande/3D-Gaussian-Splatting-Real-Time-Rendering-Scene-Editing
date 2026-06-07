# Paper 3 — Gaussian Grouping

**Paper:** Ye et al., *Gaussian Grouping: Segment and Edit Anything in 3D Scenes*, ECCV 2024
**Official repo:** https://github.com/lkeab/gaussian-grouping

---

## Setup

```bash
git clone https://github.com/lkeab/gaussian-grouping --recursive
cd gaussian-grouping
conda env create --file environment.yml
conda activate gaussian_grouping

# Install SAM
pip install git+https://github.com/facebookresearch/segment-anything.git

# Download SAM ViT-H weights
wget https://dl.fbaipublicfiles.com/segment_anything/sam_vit_h_4b8939.pth
```

> SAM model loading spikes memory significantly. High RAM runtime on Colab Pro is recommended.

---

## Pipeline Overview

**Stage 1 — Generate 2D identity masks**
SAM is run on each training frame to produce per-object segmentation masks used as supervision.

**Stage 2 — Train with identity encoding**
Each Gaussian learns a low-dimensional identity feature vector. The identity loss encourages Gaussians belonging to the same object to cluster together in feature space.

---

## Training

```bash
python train.py -s <path_to_dataset> \
    --sam_ckpt <path_to_sam_vit_h.pth> \
    --feature_dim 16
```

---

## Editing

```bash
# Segmentation
python render.py -m <path_to_model> --task segment --object_id <id>

# Object removal + inpainting
python render.py -m <path_to_model> --task remove --object_id <id>

# Recoloring
python render.py -m <path_to_model> --task recolor --object_id <id> --color <hex>
```

---

## Folder Contents

```
paper3_gaussian_grouping/
├── README.md           # This file
└── notebooks/
    └── GaussianGrouping_Final.ipynb   # Full pipeline notebook
```

---

## Notes

- SAM is used only at training time — not at inference, so rendering stays fast.
- Identity encoding dimension of 16 works well for most scenes.
- Inpainting after removal uses 2D diffusion-based infill; results are scene-dependent.
