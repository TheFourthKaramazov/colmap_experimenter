# COLMAP Experimenter

A step-by-step Python CLI wrapper for running COLMAP with per-stage timing, automatic stats collection, and support for both single-scene and batch processing.

## Requirements

- Python 3.7+
- COLMAP installed and available on the command line
- Python packages:
  - numpy

## Installation

```bash
pip install numpy
```

If Colmap is not installed: [COLMAP official installation guide](https://colmap.github.io/install.html)

## Usage 

### Single Scene

```bash
python colmap_experimenter.py \
  --images         /path/to/scene/images \
  --workspace      /results/scene \
  --matcher        exhaustive \
  --patchmatch     high \
  --gpu            true \
  --single_camera  false
```

### Batch

```bash
python colmap_experimenter.py \
  --dataset_root   /data/multiscene \
  --workspace      /results/all_scenes \
  --matcher        exhaustive \
  --patchmatch     high \
  --gpu            true \
  --single_camera  false
```

### Arguments

    --images
    Folder with images for one scene.

    --dataset_root
    Parent folder of multiple scene subfolders.

    --workspace
    Output root directory. A subfolder will be created for each scene.

    --matcher
    Feature matcher: sequential, exhaustive (default), or vocab_tree.

    --overlap
    Used for sequential matcher (default: 5).

    --patchmatch
    fast or high (default: high, enables geometric consistency).

    --gpu
    Use GPU for feature matching and extraction (true by default).

    --single_camera
    If true, forces shared intrinsics for all images (useful when all images have same resolution).

    --threads
    Number of CPU threads to use (defaults to all available).

### Outputs (per scene)

    database.db – COLMAP database with features and matches

    sparse/ – sparse reconstruction results

    dense/undist/fused.ply – dense fused point cloud

    timings.csv – per-stage timing in seconds

    Console output – reconstruction stats including registered image count and mean reprojection error
