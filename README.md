# Gluco-Vision-AI
Gluco Vision AI is a deep learning system that analyzes retinal fundus images to predict diabetic retinopathy severity and estimate blood glucose levels. It uses lesion segmentation, DR classification, and HbA1c-based regression modeling to provide a non-invasive and interpretable diabetes monitoring approach.
Project Objective
Gluco Vision AI is a fully automated and non-invasive deep learning system developed to predict diabetic retinopathy severity and estimate fasting blood glucose levels using retinal fundus images. The project aims to reduce dependency on invasive blood tests by combining retinal image preprocessing, lesion segmentation, DR classification, and glucose prediction into a single AI-powered pipeline.
Dataset Used
FGADR Dataset
Used for retinal lesion segmentation and diabetic retinopathy severity classification. The dataset contains annotated retinal fundus images with lesions such as:
Microaneurysms
Hemorrhages
Hard Exudates
Soft Exudates
Neovascularization
IRMA
NHANES Dataset
Used for blood glucose prediction by learning the relationship between HbA1c values and fasting blood glucose levels.
Methodology
The proposed system follows a five-stage pipeline:
1. Image Preprocessing
   Black border removal
   Ben Graham illumination correction
   CLAHE contrast enhancement
   Image resizing to 512×512
2. Lesion Segmentation
   U-Net with EfficientNet-B4 encoder
   Detects retinal lesions at pixel level
3. DR Severity Classification
   ResNet-50 CNN model
   Uses RGB image + lesion mask as 4-channel input
   Predicts DR severity from Grade 0 to Grade 4
4. HbA1c Mapping & Feature Engineering
   DR grade mapped to HbA1c ranges using UKPDS lookup tables
   Feature vector generation for regression analysis
5. Blood Glucose Prediction
   Regression models trained on NHANES dataset
   Final fasting blood glucose estimated in mg/dL using the best-performing model
Models Used
Deep Learning Models
U-Net + EfficientNet-B4
ResNet-50 CNN
Regression Models
ADA Formula
Lasso Regression
CART Decision Tree
Random Forest Regressor
Lasso Regression achieved the best performance and was selected as the final glucose prediction model.
Results / Accuracy
Lesion Segmentation
Best mIoU: 0.1116
DR Classification
Validation Accuracy: 88.09%
Blood Glucose Prediction
Best Model: Lasso Regression
MAE: 10.48 mg/dL
R² Score: 0.6283
The proposed system demonstrates the feasibility of non-invasive diabetes severity prediction using retinal fundus imaging.
Future Scope
Integration with hospital healthcare systems
Using larger and more diverse retinal datasets
Improving segmentation accuracy with advanced architectures
Continuous patient monitoring and longitudinal analysis
Integration of Explainable AI (XAI) for better clinical interpretability
Extending the system to detect additional retinal diseases beyond diabetic retinopathy
