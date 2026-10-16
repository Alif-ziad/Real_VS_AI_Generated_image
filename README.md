# Real vs AI-Generated Image Classification

An academic computer-vision experiment using **PyTorch** to classify real and AI-generated images. A custom four-layer CNN is trained first as a baseline, then with image augmentation and dropout.

## What's included

| File | Purpose |
| --- | --- |
| [Preprocessing notebook](cvpr-realsynthx-%28preprocessing%29.ipynb) | Inspect RealSynthX, create stratified splits, and export 224 × 224 RGB JPEGs. |
| [Training notebook](Training.ipynb) | Train the CNN, compare learning curves, and inspect filters, feature maps, confusion matrices, and predictions. |
| [Processed images](Real%20And%20AI%20images%28processed%29.rar) | Approximately 89.5 MB archive containing the train, validation, and test folders. |

The processed archive contains **3,820 images**, balanced at 1,910 per class: `AI_Generated` and `Real_Scene`. Its 70/15/15 split contains **2,674 training, 573 validation, and 573 test images**, matching the preprocessing notebook's saved counts.

## Training

The CNN has four convolution/pooling blocks and a two-layer classification head. Both rounds use Adam and cross-entropy loss with batches of 32:

- **Baseline:** 10 epochs, without augmentation or dropout.
- **Augmented:** 30 epochs, with horizontal flips, small rotations, color jitter, and dropout of 0.8.

Each round saves its best validation checkpoint to `best_model.pth`; the second round overwrites that filename. No trained checkpoint is included in the repository.

## Run

1. Use Jupyter, Colab, or Kaggle with these packages available:

   ```text
   torch torchvision numpy matplotlib scikit-learn seaborn pillow pandas tqdm
   ```

2. Extract the included RAR into the notebook's working directory, preserving `{train,val,test}/{AI_Generated,Real_Scene}` inside the extracted folder. Run `Training.ipynb` in order. It uses CUDA when available, otherwise CPU. If no split folders are found, it attempts to download `alifziad/real-and-ai-generated-images` through `kagglehub`.
3. To regenerate processed images from the raw RealSynthX data, use the preprocessing notebook. Update its Kaggle-specific `DATASET_ROOT` and `OUTPUT_ROOT` paths, and start with an empty output directory.

## Limitations

- The final cell labels validation results as "test" results; it does **not** evaluate the separate test folder. Saved outputs are inconsistent, so they should not be treated as a verified final benchmark.
- The archive contains **45 exact-duplicate groups spanning splits**, creating potential evaluation leakage. Results do not establish performance on unseen image sources or generators.
- Library versions are not pinned. Preprocessing uses seed 42, but its unsorted file listing can change the exact split.

## Credits

Repository maintainer: **MD Alif Ziad Sarkar** (AIUB). The tracked project files contain no additional contributor roster.
