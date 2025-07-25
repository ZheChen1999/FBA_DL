# Automated Detection of Radiolucent Foreign Body Aspiration on Chest CT Using Deep Learning

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY--4.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

**[📘 Paper (npj Digital Medicine, under revision)](https://github.com/ZheChen1999/FBA_DL)**

Radiolucent foreign body aspiration (FBA) remains challenging to detect using conventional CT interpretation. We propose a deep learning framework combining 3D airway segmentation with multi-view classification that achieves superior performance over expert radiologists, especially in recall and F1 score.

---

## 🔍 Overview

- **Segmentation**: Using MedpSeg (an advanced 3D U-Net), trained with expert-in-the-loop refinement.
- **Classification**: ResNet-18 model on 12-view 2D projections of the segmented airway.
- **Evaluation**: Validated on 3 independent hospital cohorts from Wuhan, China.
- **Comparison**: Outperformed expert radiologists in radiolucent FBA detection.

---

## 📊 Performance Summary

| Dataset                     | Accuracy | Precision | Recall | F1 Score |
|-----------------------------|----------|-----------|--------|----------|
| Internal Modeling (n=268)   | 94.4%    | 84.2%     | 78.0%  | 81.0%    |
| External Validation (n=103) | 90.3%    | 76.2%     | 76.2%  | 76.2%    |
| Independent Evaluation (n=70)| **90.0%** | **76.9%** | **71.4%** | **74.1%** |
| Expert Radiologists         | 87.1%    | 100%      | 35.7%  | 52.6%    |

---

## 📁 Repository Structure

FBA_DL/
├── segmentation/ # MedpSeg model code and evaluation scripts
├── classification/ # ResNet-18 classifier
├── preprocessing/ # CT normalization, clipping, view generation
├── utils/ # Helper functions and evaluation metrics
├── configs/ # Hyperparameters and training settings
├── demo/ # Example cases and visualization tools
└── README.md # Documentation


---

## ⚙️ Installation

Requires **Python 3.8+**, **PyTorch 1.10+**
- git clone https://github.com/ZheChen1999/FBA_DL.git
- cd FBA_DL
- pip install -r requirements.txt

## 🚀 Quick Start
### 1. Preprocess CT scans
- python preprocessing/preprocess_ct.py --input ./data/ct_raw/ --output ./data/processed/

python preprocessing/preprocess_ct.py --input ./data/ct_raw/ --output ./data/processed/
### 2. Run airway segmentation
- python segmentation/run_medpseg.py --input ./data/processed/ --output ./data/airway_masks/

### 3. Generate 12-view projection images
- python preprocessing/generate_views.py --input ./data/airway_masks/ --output ./data/snapshots/

### 4. Train classification model
python classification/train_resnet18.py --data ./data/snapshots/ --epochs 100

## 🧠 Technical Highlights
- **Airway segmentation**: MedpSeg (Dice: 87.5%) with iterative radiologist corrections
- **Classification model**: ResNet-18 on multi-view snapshots

- **Training strategies**: focal loss, stratified mini-batches, targeted augmentation

- **Validation**: 5-fold cross-validation + held-out external and evaluation cohorts

- **Hardware**: Dual RTX A5000 GPUs

##🏥 Clinical Workflow
Initial CXR for suspected FBA
CT scan if radiolucent FBA suspected
AI-assisted airway segmentation and classification
Highlight cases for bronchoscopy → reduce missed diagnosis

## 📘 Citation
@article{liu2025fba,
  title={Automated Detection of Radiolucent Foreign Body Aspiration on Chest CT Using Deep Learning},
  author={Liu, Xiaofan and Chen, Zhe and Tang, Zhiyong and Yang, Xun and Jiang, Yan and et al.},
  journal={npj Digital Medicine},
  year={2025},
  note={Under review}
}

## 📜 License
This repository is made available under the Creative Commons Attribution 4.0 International (CC BY 4.0) license.

## 🔗 Related Links
🧠 Project page: https://github.com/ZheChen1999/FBA_DL
📄 Full manuscript (preprint link if available)
📈 Supplementary data: see docs/ or contact authors
