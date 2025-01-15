# Alzheimer's Disease Prediction Project

## Project Overview
A comprehensive machine learning project focused on early detection and prediction of Alzheimer's disease using an ensemble approach. This project demonstrates the effective combination of deep learning and tree-based models while maintaining clinical interpretability through SHAP analysis.

## Business Problem
Alzheimer's disease is a progressive neurodegenerative disorder affecting millions worldwide. Early detection is crucial for better treatment outcomes. This project aims to:
- Develop accurate predictive models for Alzheimer's disease
- Identify key contributing factors
- Provide interpretable predictions for clinical use

## Data and Features
**Source**: Clinical dataset containing Alzheimer's disease diagnostic information  
**Size**: 2,149 records with 35 features  
**Target Variable**: Binary classification of Alzheimer's diagnosis  

### Feature Categories:
#### Clinical Assessments
- MMSE (Mini-Mental State Examination)
- Functional Assessment
- ADL (Activities of Daily Living)
- Memory Complaints
- Behavioral Problems

#### Medical History
- Family History of Alzheimer's
- Cardiovascular Disease
- Depression
- Head Injury
- Hypertension
- Diabetes

#### Lifestyle Factors
- Physical Activity Levels
- Diet Quality
- Sleep Quality
- BMI
- Smoking Status
- Alcohol Consumption

#### Demographics
- Age
- Gender
- Ethnicity
- Education Level

---

## Preprocessing and Feature Engineering

### Data Cleaning
- Removed unnecessary identifiers
- No missing values handling required

### Feature Engineering
- One-hot encoding for categorical variables
- Robust scaling for numerical features
- Feature selection using XGBoost importance

---

## Validation Strategy
- Train/Validation/Test Split (60%/20%/20%)
- Stratified splitting to maintain class distribution
- Consistent random state (42) for reproducibility

---

## Model Architecture

### Ensemble Model Components:
#### Deep Learning (Weight = 0.3)
- **Architecture**:
  - Dense layers: 128 → 64 → 32 → 16
  - Batch Normalization
  - Dropout: 0.5 → 0.2
  - L2 Regularization (0.01)
- **Training**:
  - Optimizer: Adam (learning rate = 0.0005)
  - Loss: Binary Cross-entropy
  - Early Stopping & Learning Rate Reduction

#### Tree-based Models
- **XGBoost (Weight = 0.3)**:
  - 200 trees, max_depth=4
  - learning_rate=0.01
- **LightGBM (Weight = 0.2)**:
  - 200 trees, num_leaves=15
- **CatBoost (Weight = 0.2)**:
  - 200 iterations, depth=4

---

## Model Performance

### Individual Models (Validation Set):
| Model      | Accuracy | AUC    |
|------------|----------|--------|
| XGBoost    | 0.9488   | 0.9594 |
| LightGBM   | 0.9558   | 0.9588 |
| CatBoost   | 0.9581   | 0.9547 |
| Deep Learning | 0.8744 | 0.9300 |

### Individual Models (Test Set):
| Model      | Accuracy | AUC    |
|------------|----------|--------|
| XGBoost    | 0.9535   | 0.9447 |
| LightGBM   | 0.9558   | 0.9459 |
| CatBoost   | 0.9535   | 0.9480 |
| Deep Learning | 0.8860 | 0.9220 |

### Ensemble Performance:
| Set        | Accuracy | AUC    |
|------------|----------|--------|
| Validation | 0.9395   | 0.9563 |
| Test       | 0.9465   | 0.9474 |

---

## SHAP Analysis Insights

### Primary Predictors:
- **FunctionalAssessment** (SHAP -2.0 to 1.0):  
  Higher scores strongly indicate lower risk; most influential feature overall.
- **ADL** (SHAP -1.5 to 1.0):  
  Lower scores indicate higher risk; critical for daily function assessment.
- **MemoryComplaints** (SHAP -0.5 to 1.5):  
  Strong positive correlation with diagnosis; key early indicator.

### Secondary Factors:
- MMSE scores
- Behavioral Problems
- Diet Quality
- Age
- Sleep Quality

---

## Why We Chose the Ensemble Model

While individual tree-based models showed strong performance, we selected the **ensemble model** for the following reasons:

1. **Balanced Performance Across Metrics**:  
   The ensemble model provides robust accuracy and AUC scores across both validation and test sets, demonstrating reliable performance.

2. **Robustness to Data Variability**:  
   By incorporating both deep learning and tree-based models, the ensemble compensates for individual model weaknesses, particularly the lower performance of the deep learning model.

3. **Interpretability for Clinical Use**:  
   With SHAP analysis, the ensemble offers clear insights into critical predictors like Functional Assessment and ADL, making it suitable for real-world clinical decision-making.

4. **Reduced Diagnostic Errors**:  
   The ensemble maintains high accuracy while balancing between false positives and negatives, crucial for medical applications.

5. **Generalization and Stability**:  
   Similar performance between validation (93.95%) and test sets (94.65%) indicates good generalization capabilities.

---

## Limitations & Future Improvements

### Model Limitations:
- **Limited dataset size**
- Potential regional bias
- Cross-sectional data only
- Deep learning model underperformance

### Future Work:
- Incorporate longitudinal data
- Add neuroimaging features
- Develop real-time monitoring
- Enhance deep learning architecture
- External validation
- Experiment with different ensemble weights

---

## Files:

The actual code with details about this project is in "**Alzheimer's_Disease_Prediction(Ensemble).ipynb**"
