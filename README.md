# 🧠 SAM vs MedSAM1: Zero-Shot Medical Image Segmentation

This project evaluates the Segment Anything Model (SAM) and its domain-adapted variant MedSAM1 on two key medical imaging datasets — LIDC-IDRI (lung CT nodules) and RSNA BraTS (brain tumor MRI). The goal is to assess their zero-shot segmentation performance using bounding box prompts and visualize where medical-specific fine-tuning improves segmentation outcomes.

## 🚀 Project Highlights
- 🔬 Medical Focus: Benchmark SAM and MedSAM1 on lung CT and brain MRI data.
- 🎯 Zero-Shot Evaluation: No fine-tuning — only bounding boxes as prompts.
- 📊 Rich Evaluation: Dice Score, IoU, HD95, inference time.
- 🧠 Domain Transfer Study: Showcases clear performance gain from domain-specific adaptation (MedSAM1).
- 📸 Qualitative Visuals: Detailed side-by-side visualizations and heatmaps of predictions.

## 📁 Dataset Overview
| Dataset |	Modality | Segmentation Target | Preprocessing |
|---------|---------|---------|---------|
| LIDC-IDRI |	CT | Lung Nodules | PNG slices with nodule masks |
|RSNA BraTS | T1CE MRI| Enhancing Tumor Region | NIfTI → Axial PNG slices |
- Ground truth for LIDC aggregated from 4 radiologists.
- BraTS data extracted from official 2021 competition dataset.

## 🔧 Data Preprocessing
Medical imaging data often comes in specialized formats (like DICOM and NIfTI) and requires intensive preprocessing before it can be used with SAM-based models trained on natural images. A significant portion of the project effort was spent on this stage:

### ✅ LIDC-IDRI (Lung CT):
- DICOM to PNG Conversion: Slices were extracted from 3D CT volumes and converted to 2D grayscale PNGs.
- Annotation Aggregation: Used pylidc to extract lung nodules annotated by multiple radiologists. These annotations were combined using:
  - Intersection of multiple radiologist segmentations
  - Largest connected component selection
- Normalization: Pixel intensities were rescaled to 0–255 and normalized to match natural image input range.
- Prompt Boxes: Bounding boxes were generated programmatically around the nodules as input prompts for SAM and MedSAM1.

### RSNA BraTS (Brain Tumor MRI):
- NIfTI Slicing: Axial slices were extracted from T1CE modality using nibabel.
- Label Selection: From the segmentation labels, only the Enhancing Tumor (ET) region was used (label=4).
- Mask Processing:
  - Binarization of ET mask
  - Slices with no ET region were excluded
- Resizing and Padding: All slices were resized/padded to fit 1024×1024 resolution required by SAM and MedSAM1.
- Prompt Generation: Bounding boxes tightly enclosing the ET region were created.

This preprocessing pipeline ensured that the model inputs — both image and mask — were clean, aligned, and matched the modality assumptions of the zero-shot SAM-based models.
