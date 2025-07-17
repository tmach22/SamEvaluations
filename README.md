🧠 SAM vs MedSAM1: Zero-Shot Medical Image Segmentation
This project evaluates the Segment Anything Model (SAM) and its domain-adapted variant MedSAM1 on two key medical imaging datasets — LIDC-IDRI (lung CT nodules) and RSNA BraTS (brain tumor MRI). The goal is to assess their zero-shot segmentation performance using bounding box prompts and visualize where medical-specific fine-tuning improves segmentation outcomes.

🚀 Project Highlights
- 🔬 Medical Focus: Benchmark SAM and MedSAM1 on lung CT and brain MRI data.
- 🎯 Zero-Shot Evaluation: No fine-tuning — only bounding boxes as prompts.
- 📊 Rich Evaluation: Dice Score, IoU, HD95, inference time.
- 🧠 Domain Transfer Study: Showcases clear performance gain from domain-specific adaptation (MedSAM1).
- 📸 Qualitative Visuals: Detailed side-by-side visualizations and heatmaps of predictions.

📁 Dataset Overview
| Dataset |	Modality | Segmentation Target | Preprocessing |
|---------|---------|---------|---------|
| LIDC-IDRI |	CT | Lung Nodules | PNG slices with nodule masks |
|RSNA BraTS | T1CE MRI| Enhancing Tumor Region | NIfTI → Axial PNG slices |
- Ground truth for LIDC aggregated from 4 radiologists.
- BraTS data extracted from official 2021 competition dataset.
