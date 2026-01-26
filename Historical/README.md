# Brain Tumour Segmentation (Historical) — Adaptive Region Growing

## 📋 Overview

This folder contains the **historical (classical)** approach used in the project: **adaptive region growing** for brain tumour segmentation on **BraTS2020** MRI scans.

The notebook implements:
- Loading **BraTS2020** NIfTI volumes (`.nii`) using `nibabel`
- Selecting a **seed point** (brightest pixel after thresholding)
- Performing **region growing** with a threshold constraint
- Searching for an **optimal threshold** using an objective function:

**Heuristic function:**
$$h = \alpha G_s + \beta \sigma_s^2$$

Where:
- $G_s = \frac{1}{\bar{g}_s}$ : Reciprocal of mean gradient along boundary (smoothness term)
- $\sigma_s^2$ : Variance inside the segmented region (homogeneity term)
- $\alpha, \beta$ : Weight coefficients



## 📌 Notebook

- `hitorical - adaptive region growing.ipynb`

## 🧠 Dataset

Designed around **BraTS2020** (multi-modal MRI: FLAIR, T1, T1CE, T2 + segmentation mask).

In the notebook the dataset is expected as a local folder:
- `TRAIN_DATASET_PATH = '../../BraTS20/'`
- Example case:
  - `BraTS20_Training_001/BraTS20_Training_001_flair.nii`
  - `BraTS20_Training_001/BraTS20_Training_001_seg.nii`

If your dataset is elsewhere, update `TRAIN_DATASET_PATH` accordingly.

## ▶️ How to run

1. Open the notebook:
   - Jupyter: `jupyter notebook`
   - VS Code: open the `.ipynb` directly
2. Update dataset path variables.
3. Run cells top-to-bottom.

## 🔍 What you’ll see

- Visualisation of MRI modalities and ground-truth mask
- Seed selection output (seed coordinates + intensity)
- Adaptive threshold search output (initial $T_0$, best $T^*$)
- Segmentation mask visualisations
- Runtime measurements for filtering + segmentation

## 🧰 Dependencies

The notebook uses common scientific Python tooling:
- `numpy`, `pandas`
- `matplotlib`, `seaborn`
- `nibabel` (NIfTI loading)
- `opencv-python` (`cv2`)
- `scipy`
- `tqdm`
- `scikit-image`

## 📚 References

- Reference implementation inspiration: `https://github.com/Trev-Egan/Brain_Tumour_Segmentation.git`
- ADAMS, R. and BISCHOF, L., 1994. *Seeded region growing*. IEEE Transactions on Pattern Analysis and Machine Intelligence, 16(6), pp. 641–647.


