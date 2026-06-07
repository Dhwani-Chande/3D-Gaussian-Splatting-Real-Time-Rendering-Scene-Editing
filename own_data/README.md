# Own Data — Capture & Processing

Self-captured data and COLMAP scripts used to evaluate all three methods beyond standard benchmarks.

**Scene:** Desk scene — MacBook, water bottle, earphones
**Capture device:** iPhone (video.MOV)
**Pipeline:** iPhone video → frame extraction → COLMAP → Gaussian Splatting training

---

## Folder Structure

```
own_data/
├── README.md               # This file
└── my_scene/
    ├── run-colmap-photometric.sh   # COLMAP photometric pipeline script
    └── run-colmap-geometric.sh     # COLMAP geometric pipeline script
```

> Raw video, extracted frames, and COLMAP outputs are excluded from this repo due to size (video.MOV is 570MB, image folders contain thousands of files).

---

## Processing Pipeline

### Step 1 — Extract frames

```bash
ffmpeg -i video.MOV -vf fps=2 images/%04d.jpg
```

### Step 2 — Run COLMAP

```bash
bash run-colmap-geometric.sh
# or
bash run-colmap-photometric.sh
```

These scripts run COLMAP feature extraction, matching, and sparse reconstruction, producing a folder structure ready for Gaussian Splatting training.

### Step 3 — Train

```bash
# 3DGS
python train.py -s own_data/my_scene

# Mip-Splatting
python train.py -s own_data/my_scene --antialiasing
```

---

## Capture Tips

- Walk slowly around the object in a circular path (30–60 seconds)
- Keep the object centered throughout
- Even lighting — avoid harsh shadows
- ~70% overlap between consecutive frames
- Avoid reflective/transparent surfaces and moving objects
