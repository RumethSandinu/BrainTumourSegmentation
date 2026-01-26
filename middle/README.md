# Brain Tumour Segmentation (Mid) — K-Means (Wu et al. inspired)

## 📋 Overview

This folder contains the **mid-stage** approach used in the project: an **unsupervised K-means segmentation** pipeline for brain tumour segmentation on **BraTS2020**.

The notebook focuses on using MRI intensity structure (primarily **FLAIR**) and clustering pixels/voxels into regions, then comparing the resulting binary tumour mask against BraTS ground truth.

## 📌 Notebook

- `mid - k-means.ipynb`

## 🧠 Dataset

The notebook is written to run on **Kaggle** paths (from the code):
- `/kaggle/input/BraTS2020_TrainingData/MICCAI_BraTS2020_TrainingData`
- `/kaggle/input/BraTS2020_ValidationData/MICCAI_BraTS2020_ValidationData`

It expects standard BraTS case naming:
- `BraTS20_Training_001_flair.nii`
- `BraTS20_Training_001_seg.nii`

To run locally, update the `TRAINING_ROOT` / `VALIDATION_ROOT` variables to your dataset location.

## 🧪 Method summary

High-level pipeline implemented in the notebook:
- Load NIfTI volumes (`nibabel`)
- Select modality (FLAIR is used for clustering)
- Create a brain/foreground mask
- Extract features and run **KMeans** (e.g., `n_clusters=3`)
- Reconstruct clustered labels into an image/volume mask
- Post-process segmentation (morphology / connected components as needed)

## 📏 Evaluation

The notebook includes evaluation against BraTS ground truth using:
- **Dice (DSC)**
- **IoU (Jaccard)**
- **NSD (Normalized Surface Dice)** with a tolerance

Ground truth is binarized as “tumour = any label > 0” for evaluation in the notebook.

## ▶️ How to run

1. Open `mid - k-means.ipynb` in Jupyter / VS Code / Kaggle.
2. Set dataset paths (`TRAINING_ROOT`, `VALIDATION_ROOT`) for your environment.
3. Run cells top-to-bottom to:
   - inspect sample cases
   - run K-means segmentation
   - visualise predictions vs ground truth
   - compute metrics

## 🧰 Dependencies

- `numpy`, `pandas`
- `matplotlib`, `seaborn`
- `nibabel`
- `scikit-learn`
- `scipy`
- `opencv-python`
- `tqdm`
- `scikit-image`

## 📚 References

- Reference implementation inspiration: `https://github.com/NikosMouzakitis/Brain-%20tumor-detection-using-Kmeans-and-%20histogram.git`
- Wu, Ming-Ni, Chia-Chen Lin, and Chin-Chen Chang. “Brain Tumor Detection Using Color-Based K-Means Clustering Segmentation.” *Third International Conference on Intelligent Information Hiding and Multimedia Signal Processing (IIH-MSP 2007)* 2 (November 2007): 245–50. `https://doi.org/10.1109/IIHMSP.2007.4457697`

