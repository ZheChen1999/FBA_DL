# A Deep Learning Approach for Detecting Radiolucent Foreign Body Aspiration in Chest CT Scans

## Overview
This repository contains the implementation of a deep learning model designed to detect radiolucent foreign body aspiration (FBA) in chest CT scans. Radiolucent FBAs, which are often invisible on conventional radiographs, pose significant diagnostic challenges. Our approach combines airway segmentation with a classification model, providing a robust, efficient, and accurate solution for identifying these challenging cases.

## Key Features
- **Airway Segmentation**: Utilizes the MedpSeg deep learning framework for precise airway segmentation.
- **Classification Model**: Employs a fine-tuned ResNet-based convolutional neural network (CNN) for multi-view classification of CT images.
- **High Accuracy**: Achieves 94.45% accuracy in internal modeling and 90.05% in external validation for radiolucent FBA detection.
- **Open Source**: Full implementation is available to ensure transparency and reproducibility.

## Performance Metrics
| Metric                  | Internal Modeling | External Validation |
|-------------------------|-------------------|---------------------|
| **Accuracy**            | 94.45%            | 90.05%              |
| **Sensitivity**         | 87.38%            | 86.31%              |
| **Specificity**         | 97.24%            | 89.15%              |
| **Positive Predictive Value** | 77.58%       | 69.95%              |
| **Negative Predictive Value** | 98.85%       | 94.97%              |

## Methodology
1. **Dataset**: Includes 292 patients for training (58 FBA, 234 non-FBA) and 111 patients for validation (30 FBA, 81 non-FBA).
2. **Airway Segmentation**: Utilizes the MedpSeg model, validated against manual annotations for accuracy using Dice Similarity Coefficient (DSC) and other metrics.
3. **Classification**: Features multi-view CT snapshot extraction and fine-tuned ResNet CNN for classification.
4. **Implementation**: Built using PyTorch, optimized using the Adam optimizer.

## Installation
1. Clone the repository:
   ```bash
   git clone https://github.com/ZheChen1999/FBA_DL.git
   cd FBA_DL
   ```
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

## Usage
### Training
To train the segmentation model:
```bash
python scripts/train_segmentation.py
```
To train the classification model:
```bash
python scripts/train_classification.py
```

### Evaluation
Evaluate the trained model:
```bash
python scripts/evaluate.py
```

## Results
- Internal cohort: Accuracy of 94.45%, sensitivity of 87.38%, and specificity of 97.24%.
- External validation: Accuracy of 90.05%, sensitivity of 86.31%, and specificity of 89.15%.

## License
This project is licensed under the [MIT License](LICENSE).

## Acknowledgments
- Funding by the National Key Research and Development Program of China (2022YFC2303800) and National Science Foundation of China (62073149).
- Data provided by The Central Hospital of Wuhan and Renmin Hospital of Wuhan University.

## Contact
For questions or collaborations, please contact me or pull request.

---
Visit the [GitHub repository](https://github.com/ZheChen1999/FBA_DL) for the complete code and dataset access.
