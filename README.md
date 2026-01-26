# Brain Tumour Segmentation (Historical → Mid → Recent)

This project contains **three implementations** of brain tumour segmentation, showing the progression from **classical image processing** to **unsupervised clustering** and finally to a **state-of-the-art deep learning pipeline**.

All three versions are based on the **BraTS2020** dataset (multi-modal MRI).

## 📁 Implementations

- **Historical — Adaptive Region Growing** (`historical/`)
  - Classical segmentation using seed selection + region growing
  - Adaptive threshold selection via an objective function
  - Notebook: `historical/hitorical - adaptive region growing.ipynb`

- **Mid — K-Means Segmentation** (`middle/`)
  - Unsupervised clustering (KMeans) for tumour segmentation (primarily FLAIR)
  - Includes evaluation metrics (Dice / IoU / NSD)
  - Notebook: `middle/mid - k-means.ipynb`

- **Recent — nnU-Net v2** (`recent/`)
  - Deep learning segmentation using nnU-Net v2 on BraTS2020
  - Includes dataset conversion, label remapping, preprocessing, training, and prediction
  - Notebook: `recent/recent - nn-UNetv2.ipynb`

## 🧠 Dataset

The notebooks are written with **BraTS2020** (NIfTI `.nii` volumes).


