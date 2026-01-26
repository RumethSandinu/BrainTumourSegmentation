# Brain Tumour Segmentation (Recent) — nnU-Net v2 (BraTS2020)

## 📋 Overview

This folder contains the **recent (deep learning)** approach used in the project: training and evaluating **nnU-Net v2** on the **BraTS2020** brain tumour segmentation dataset.

nnU-Net is a self-configuring medical segmentation framework that automatically determines preprocessing, architecture configuration, and training schedule for a given dataset.

## 📌 Notebook

- `recent - nn-UNetv2.ipynb`

## 🔗 External dependency: nnU-Net v2

This implementation **relies on the official nnU-Net repository** and its tooling.
The nnU-Net source code is **not included** in this repository.

- **Official repo**: `https://github.com/MIC-DKFZ/nnUNet`

In our development environment, we used a local clone of nnU-Net v2 (outside this repo). If you’re reproducing locally, **clone and install nnU-Net** and then run our notebook.

## 🧠 Dataset

The notebook targets **BraTS2020**:
- **Modalities**: FLAIR, T1, T1CE, T2
- **Classes**: Background, Edema, Non-enhancing tumour, Enhancing tumour

The notebook is written for a Kaggle environment and uses a dataset layout similar to:
- `/kaggle/input/brats20-dataset-training-validation/...`
- `/kaggle/input/BraTS2020_TrainingData/MICCAI_BraTS2020_TrainingData`

## 🏗️ What the notebook does

Key steps implemented in the notebook:

- **Environment setup**
  - uses PyTorch
  - uses a local nnU-Net v2 codebase (cloned from the official repository)

- **Build nnU-Net dataset structure**
  - creates `Dataset001_BraTS2020` under:
    - `nnUNet_raw`
    - `nnUNet_preprocessed`
    - `nnUNet_results`
  - creates `imagesTr/` and `labelsTr/` (and links BraTS cases)
  - generates `dataset.json`

- **Label remapping (BraTS → nnU-Net)**
  - BraTS labels are `{0, 1, 2, 4}`
  - nnU-Net requires consecutive `{0, 1, 2, 3}`
  - remaps **4 → 3** in label maps

- **Preprocessing**
  - runs:
    - `nnUNetv2_plan_and_preprocess -d 1 --verify_dataset_integrity`

- **Training**
  - trains 3D full-resolution configuration (fold 0):
    - `nnUNetv2_train 1 3d_fullres 0`
  - includes a validation run:
    - `nnUNetv2_train 1 3d_fullres 0 --val --npz`

- **Prediction / inference**
  - prepares a predictions folder and uses the trained model folder under:
    - `nnUNet_results/Dataset001_BraTS2020/.../3d_fullres`
  - runs inference via the nnU-Net predictor utilities

## ▶️ How to run

### Option A: Run in Kaggle (recommended)

1. Upload/import the BraTS2020 dataset to Kaggle.
2. Open `recent - nn-UNetv2.ipynb`.
3. Run cells in order.

### Option B: Run locally (recommended for GitHub reproduction)

You’ll need:
- Python + PyTorch + CUDA (recommended)
- **nnU-Net v2 cloned from the official repo and installed**
- BraTS2020 dataset available locally (NIfTI `.nii`)

#### 1) Clone and install nnU-Net v2

```bash
git clone https://github.com/MIC-DKFZ/nnUNet.git
cd nnUNet
pip install -e .
```

This should make commands like `nnUNetv2_plan_and_preprocess` / `nnUNetv2_train` available.

#### 2) Run our notebook

Open `recent - nn-UNetv2.ipynb` and adapt dataset paths for your machine.

The notebook expects the nnU-Net environment variables to be set (it sets them inside the notebook as well):
- `nnUNet_raw`
- `nnUNet_preprocessed`
- `nnUNet_results`

## 🧰 Dependencies

- `torch`
- `torchvision`
- `nnunetv2`
- `nibabel`
- `numpy`
- `scipy`

## 📚 References

- nnU-Net repository: `https://github.com/MIC-DKFZ/nnUNet` ([MIC-DKFZ/nnUNet](https://github.com/MIC-DKFZ/nnUNet))
- ISENSEE, F. et al., 2024. *nnU-Net Revisited: A Call for Rigorous Validation in 3D Medical Image Segmentation*. In: M.G. LINGURARU et al., eds. *Medical Image Computing and Computer Assisted Intervention – MICCAI 2024*. Cham: Springer Nature Switzerland. pp. 488–498.
