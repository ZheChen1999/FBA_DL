# Automated Detection of Radiolucent Foreign Body Aspiration on Chest CT Using Deep Learning

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY--4.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

**[📘 Paper (npj Digital Medicine, under revision)](https://github.com/ZheChen1999/FBA_DL)**

Radiolucent foreign body aspiration (FBA) is challenging to diagnose due to its subtle imaging characteristics on CT. We present a deep learning pipeline that integrates 3D airway segmentation with multi-view classification. Our model was validated across three independent hospital datasets and outperformed expert radiologists in key diagnostic metrics.

---

## 🔍 Overview

* **Segmentation**: MedpSeg, a high-precision 3D U-Net-based segmentation model.
* **Classification**: ResNet-18 applied to 12-view 2D projections of the airway tree.
* **Validation**: Multi-center datasets from three hospitals in Wuhan, China.
* **Comparison**: Model demonstrated higher recall and F1 score than radiologists.

---

## 📊 Performance Summary

| Dataset                       | Accuracy | Precision | Recall | F1 Score |
| ----------------------------- | -------- | --------- | ------ | -------- |
| Internal Modeling (n=268)     | 94.4%    | 84.2%     | 78.0%  | 81.0%    |
| External Validation (n=103)   | 90.3%    | 76.2%     | 76.2%  | 76.2%    |
| Independent Evaluation (n=70) | 90.0%    | 76.9%     | 71.4%  | 74.1%    |
| Expert Radiologists           | 87.1%    | 100%      | 35.7%  | 52.6%    |

---

## ⚙️ Installation

Requires **Python 3.8+**, **PyTorch 1.10+**

```bash
git clone https://github.com/ZheChen1999/FBA_DL.git
cd FBA_DL
pip install -r requirements.txt
```

---

## 🚀 Quick Start

### 1. Preprocess CT scans

```bash
python preprocessing/preprocess_ct.py --input ./data/ct_raw/ --output ./data/processed/
```

### 2. Run airway segmentation

```bash
python segmentation/run_medpseg.py --input ./data/processed/ --output ./data/airway_masks/
```

### 3. Generate 12-view projections

```bash
python preprocessing/generate_views.py --input ./data/airway_masks/ --output ./data/snapshots/
```

### 4. Train ResNet-18 classifier

```bash
python classification/train_resnet18.py --data ./data/snapshots/ --epochs 100
```

---

## 🧠 Technical Highlights

* **Airway segmentation**: 3D U-Net (MedpSeg) with expert-in-the-loop refinement
* **Snapshot generation**: Multi-angle 2D views of 3D segmented airway
* **Classification**: ResNet-18 with Focal Loss and data augmentation
* **Training strategy**: 5-fold cross-validation, early stopping
* **Hardware**: Dual RTX A5000 GPUs, NVIDIA RTX 3090 for segmentation

---

## 🏥 Clinical Workflow

1. Initial CXR (to rule out radiopaque FBA)
2. Chest CT if radiolucent FBA suspected
3. AI-assisted segmentation and classification
4. Use model results to prioritize bronchoscopy

---

## 📘 Citation

```bibtex
@article{liu2025fba,
  title={Automated Detection of Radiolucent Foreign Body Aspiration on Chest CT Using Deep Learning},
  author={Liu, Xiaofan and Chen, Zhe and Tang, Zhiyong and Yang, Xun and Jiang, Yan and et al.},
  journal={npj Digital Medicine},
  year={2025},
  note={Under review}
}
```

---

## 📂 Supplementary Materials

Detailed methodology, datasets, training protocols, and ablation studies are provided in the [Supplementary Materials](docs/Supplementary_Materials.md). Topics include:

* **Data Sources**: Multi-center cohorts from Wuhan hospitals + ATM22 dataset
* **MedpSeg Architecture**: 3D U-Net with expert-guided iterative training
* **ResNet-18 Classifier**: Multi-view CNN with snapshot-based classification
* **Evaluation**: AUC, precision, recall, F1, cross-validation, DeLong's test
* **Ablation Studies**: Contribution of each pipeline component
* **Backbone Comparisons**: DenseNet, ViT-B/16, Swin-T, etc.

---

## 📈 Additional Results

### Table S3: Backbone Architecture Comparison in Independent Evaluation Cohort

| Backbone        | TP         | FN       | TN         | FP       | Accuracy | Precision | Recall | F1 Score |
| --------------- | ---------- | -------- | ---------- | -------- | -------- | --------- | ------ | -------- |
| ResNet-18       | 10 (14.3%) | 4 (5.7%) | 53 (75.7%) | 3 (4.3%) | 90.0%    | 76.9%     | 71.4%  | 74.1%    |
| EfficientNet-B0 | 9 (12.9%)  | 5 (7.1%) | 53 (75.7%) | 3 (4.3%) | 88.6%    | 75.0%     | 64.3%  | 69.2%    |
| DenseNet-121    | 9 (12.9%)  | 5 (7.1%) | 52 (74.3%) | 4 (5.7%) | 87.1%    | 69.2%     | 64.3%  | 66.7%    |
| ViT-B/16        | 8 (11.4%)  | 6 (8.6%) | 52 (74.3%) | 4 (5.7%) | 85.7%    | 66.7%     | 57.1%  | 61.5%    |
| Swin-T (tiny)   | 9 (12.9%)  | 5 (7.1%) | 51 (72.9%) | 5 (7.1%) | 85.7%    | 64.3%     | 64.3%  | 64.3%    |

*Interpretation*: The full pipeline achieved the highest performance across all evaluation metrics, validating the importance of each module. These findings suggest that structural modeling and comprehensive spatial coverage are critical for detecting subtle FBA-related changes.

---

### Table S4: Age-based Subgroup Performance in Independent Evaluation Cohort

| Age Group         | TP        | FN       | TN         | FP       | Accuracy | Precision | Recall | F1 Score |
| ----------------- | --------- | -------- | ---------- | -------- | -------- | --------- | ------ | -------- |
| < 40 years (n=12) | 3 (25.0%) | 1 (8.3%) | 7 (58.3%)  | 1 (8.3%) | 83.3%    | 75.0%     | 75.0%  | 75.0%    |
| ≥ 40 years (n=58) | 7 (12.1%) | 3 (5.2%) | 46 (79.3%) | 2 (3.4%) | 91.4%    | 77.8%     | 70.0%  | 73.7%    |

*All P values were calculated using Fisher’s exact test.*

---

### Table S5: Ablation Study in Independent Evaluation Cohort

| Variant                  | TP         | FN       | TN         | FP         | Accuracy | Precision | Recall | F1 Score |
| ------------------------ | ---------- | -------- | ---------- | ---------- | -------- | --------- | ------ | -------- |
| Baseline (Raw CT Only)   | 8 (11.4%)  | 6 (8.6%) | 43 (61.4%) | 13 (18.6%) | 72.9%    | 38.1%     | 57.1%  | 45.7%    |
| + With Segmentation Mask | 9 (12.9%)  | 5 (7.1%) | 45 (64.3%) | 11 (15.7%) | 77.1%    | 45.0%     | 64.3%  | 52.9%    |
| + Fewer Views (6 Views)  | 9 (12.9%)  | 5 (7.1%) | 47 (67.1%) | 9 (12.9%)  | 80.0%    | 50.0%     | 64.3%  | 56.3%    |
| + With Data Augmentation | 10 (14.3%) | 4 (5.7%) | 49 (70.0%) | 7 (10.0%)  | 84.3%    | 58.8%     | 71.4%  | 64.5%    |
| Full Pipeline (12 Views) | 10 (14.3%) | 4 (5.7%) | 53 (75.7%) | 3 (4.3%)   | 90.0%    | 76.9%     | 71.4%  | 74.1%    |

*Interpretation*: The full pipeline achieved the highest performance across all evaluation metrics, validating the importance of each module. These findings suggest that structural modeling and comprehensive spatial coverage are critical for detecting subtle FBA-related changes.

---

## 📜 License

This project is licensed under the Creative Commons Attribution 4.0 International (CC BY 4.0).

---


## 🔗 Related Links

* 🧠 Project page: [https://github.com/ZheChen1999/FBA\_DL](https://github.com/ZheChen1999/FBA_DL)
* 📄 Full manuscript (preprint link if available)
* 📈 Supplementary tables and figures available in `docs/`

---

> For detailed replication instructions, data access requests, or collaboration inquiries, please contact the corresponding authors.
