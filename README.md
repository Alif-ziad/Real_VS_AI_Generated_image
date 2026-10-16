<div align="center">

# Real vs AI-Generated Image Classification
### Preprocessing and Image-Classification Experiment Workspace

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=flat-square&logo=jupyter&logoColor=white)
![Pillow](https://img.shields.io/badge/Pillow-image%20processing-6e7681?style=flat-square)
![Status](https://img.shields.io/badge/status-experiment%20workspace-d29922?style=flat-square)

</div>

A computer-vision experiment repository for preparing image data and training a classifier to distinguish **real images from AI-generated images**. The repository contains the preprocessing notebook, training notebook, and a packaged processed-data artifact.

## Repository contents

```text
.
├── README.md
├── cvpr-realsynthx-(preprocessing).ipynb
├── Training.ipynb
└── Real And AI images(processed).rar
```

| Artifact | Role |
|---|---|
| `cvpr-realsynthx-(preprocessing).ipynb` | Dataset inspection, class splitting, RGB conversion, resizing, verification, and balanced-subset preparation |
| `Training.ipynb` | Model-training experiment notebook |
| `Real And AI images(processed).rar` | Packaged processed-image artifact (~89.5 MB in the repository) |

## Verified preprocessing workflow

The preprocessing notebook performs the following operations:

1. Reads separate **real** and **fake** image directories.
2. Shuffles filenames independently by class.
3. Creates train/validation/test directories.
4. Splits the full data using an approximately **80% / 10% / 10%** ratio.
5. Converts supported images to **RGB**.
6. Resizes processed images to **128 × 128** pixels.
7. Verifies resulting image size/mode consistency.
8. Creates a compressed processed-data artifact.
9. Provides an additional balanced **12,500-image subset** workflow.

## Full processed dataset counts

The executed preprocessing notebook reports **19,680 images** in the source population used by that workflow:

| Split | Real | AI-generated / Fake | Total |
|---|---:|---:|---:|
| Train | 7,780 | 7,963 | 15,743 |
| Validation | 972 | 995 | 1,967 |
| Test | 974 | 996 | 1,970 |
| **Total** | **9,726** | **9,954** | **19,680** |

The class discovery step records the mapping:

```text
fake → 0
real → 1
```

## Balanced subset workflow

The preprocessing notebook also builds a smaller balanced dataset containing **12,500 images**:

| Split | Fake | Real | Total |
|---|---:|---:|---:|
| Train | 5,000 | 5,000 | 10,000 |
| Validation | 625 | 625 | 1,250 |
| Test | 625 | 625 | 1,250 |
| **Total** | **6,250** | **6,250** | **12,500** |

This provides a controlled 1:1 class distribution for experiments that require balanced classes.

## Data preparation details

The preprocessing notebook verifies that processed files are:

- **128 × 128** pixels
- **RGB** images
- Organized under train/validation/test directories
- Separated into `real` and `fake` class directories

The notebook was written around Google Drive/Colab-style paths. To reproduce the preprocessing elsewhere, update the source/output paths to match your local or mounted dataset location.

## Training status and reporting

`Training.ipynb` contains the training workflow. This README intentionally does **not** publish a model architecture or final accuracy until the executed training outputs, exact configuration, and final evaluation artifact are separately frozen and documented. That avoids presenting exploratory notebook output as a verified final benchmark.

For a stronger reproducible release, the next training-documentation step should record:

- Exact model architecture/checkpoint
- Framework/library versions
- Random seeds
- Train/validation transforms
- Loss and optimizer configuration
- Epoch/batch settings
- Final validation/test metrics
- Confusion matrix and per-class metrics
- Saved-model/checkpoint identity

## Reproducibility notes

- The preprocessing notebook copies images into split directories; it does not treat the GitHub repository itself as the canonical raw-dataset source.
- The large `.rar` artifact is convenient for preservation but is not ideal for source-control review.
- A future cleaned release should keep code, documentation and compact results on GitHub while placing large datasets/model artifacts on a dataset/model host or release storage.
- Dataset licensing/provenance should be documented explicitly before redistributing the processed image archive as a formal public dataset.

## Project status

**Experiment workspace / academic computer-vision project.** The data-preparation pipeline is documented from executed notebook evidence. Final training-performance claims remain intentionally separate until the training configuration and results are frozen and reproducibly summarized.

## Author

**MD Alif Ziad Sarkar**  
BSc in Computer Science and Engineering, American International University-Bangladesh (AIUB)
