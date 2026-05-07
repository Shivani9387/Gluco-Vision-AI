# Gluco Vision AI
A non-invasive deep learning system for predicting diabetic retinopathy severity and estimating fasting blood glucose levels from retinal fundus images.
## Overview
Gluco Vision AI was built to explore whether retinal imaging alone can provide meaningful insight into a patient's diabetic condition — without a single blood draw. The system combines image preprocessing, lesion segmentation, DR grading, and glucose regression into one end-to-end pipeline.
The motivation is straightforward: the retina is the only part of the human body where blood vessels can be directly observed non-invasively. Changes in these vessels correlate strongly with systemic conditions like diabetes. This project attempts to quantify that relationship using modern deep learning.
## Datasets
**FGADR** — Retinal fundus images with pixel-level annotations for six lesion types:
- Microaneurysms
- Hemorrhages
- Hard Exudates
- Soft Exudates
- Neovascularization
- IRMA
**NHANES** — Population health survey data used to model the relationship between HbA1c and fasting blood glucose levels.
## Pipeline
### 1. Image Preprocessing
Raw fundus images are cleaned and normalized before entering the model. This includes black border removal, Ben Graham illumination correction, CLAHE contrast enhancement, and resizing to 512×512.
### 2. Lesion Segmentation
A U-Net with an EfficientNet-B4 encoder performs pixel-level detection of retinal lesions. The segmentation output is a multi-class mask covering all six lesion categories.
### 3. DR Severity Classification
A ResNet-50 model takes a 4-channel input — the original RGB image concatenated with the lesion mask — and classifies diabetic retinopathy severity on a scale from Grade 0 (no DR) to Grade 4 (proliferative DR).
### 4. HbA1c Mapping
The predicted DR grade is mapped to a corresponding HbA1c range using UKPDS lookup tables (UKPDS BMJ, 2000). This bridges the gap between clinical DR grading and metabolic indicators.
### 5. Blood Glucose Prediction
Regression models trained on the NHANES dataset estimate fasting blood glucose in mg/dL. Lasso Regression outperformed other approaches and was selected as the final model.
## Models
| Component | Architecture |
|---|---|
| Lesion Segmentation | U-Net + EfficientNet-B4 |
| DR Classification | ResNet-50 (4-channel input) |
| Glucose Prediction | Lasso Regression (best), also evaluated CART, Random Forest, ADA Formula |
## Results
| Task | Metric | Value |
|---|---|---|
| Lesion Segmentation | mIoU | 0.1116 |
| DR Classification | Validation Accuracy | 88.09% |
| Glucose Prediction (Lasso) | MAE | 10.48 mg/dL |
| Glucose Prediction (Lasso) | R² Score | 0.6283 |
The segmentation mIoU reflects the difficulty of the task — retinal lesions are small, sparse, and class-imbalanced. The DR classifier and glucose regression results are more clinically promising.
## Limitations
- Segmentation performance is constrained by dataset size and class imbalance
- Glucose prediction relies on population-level HbA1c-glucose correlations, which vary across individuals
- The system has not been evaluated on external clinical datasets
## Future Work
- Deploy as a real-time web or mobile application
- Integrate Explainable AI (XAI) to make predictions interpretable for clinicians
- Improve segmentation with newer architectures and larger datasets
- Extend detection to other retinal diseases beyond diabetic retinopathy
- Support longitudinal monitoring for continuous patient tracking
- Explore direct integration with hospital health record systems
## References

- UKPDS Group. *Intensive blood-glucose control with sulphonylureas or insulin.* BMJ, 2000.
- American Diabetes Association. *Translating the A1C assay into estimated average glucose values.* Diabetes Care, 2008.
- FGADR Dataset: Fine-Grained Annotated Diabetic Retinopathy
- NHANES: National Health and Nutrition Examination Survey
