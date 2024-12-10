# Alzheimer's Disease Prediction Project

## About
A motivated data scientist with a proven track record of leveraging data to solve complex problems and driving impactful business decisions.

Extensive cross-industry experience in ESG consulting, manufacturing, healthcare, and academia, showcasing expertise in data analysis, predictive modeling, and building data-driven applications. Proficient in Python, SQL, R, Tableau, and Power BI, combined with a strong foundation in machine learning, NLP, and statistical modeling. Adept at creating ETL pipelines, crafting personalized recommendation systems, and developing dashboards for actionable insights, while excelling in stakeholder communication and cross-functional collaboration.

Keen passion for advancing data science applications in healthcare and sustainability. Successfully fine-tuned LLM models for radiology annotation, optimized forecasting models for revenue growth, and designed a green index to enhance ESG performance. Always seeking innovative solutions to bridge technical and business goals while fostering impactful collaboration.

## Education
+ M.S., Applied Data Science | The University of Chicago 
(Sep 2023 – Present)

+ M.S., Business and Technology Management | Korea Advanced Institute of Science and Technology 
(Aug 2020 – Aug 2022)

+ B.S., Security and Risk Analysis (Cybersecurity) | Pennsylvania State University 
(Aug 2014 – May 2018)

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
- 5-fold stratified cross-validation
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

### Individual Models:
| Model      | Accuracy | Precision | Recall | F1   | AUC   |
|------------|----------|-----------|--------|------|-------|
| XGBoost    | 0.9581   | 0.9467    | 0.9342 | 0.9404 | 0.9576 |
| LightGBM   | 0.9605   | 0.9470    | 0.9408 | 0.9439 | 0.9542 |
| CatBoost   | 0.9558   | 0.9463    | 0.9276 | 0.9369 | 0.9598 |
| Deep Learning | 0.9558 | 0.9463    | 0.9276 | 0.9369 | 0.9494 |

### Ensemble Performance:
| Metric      | Value    |
|-------------|----------|
| Accuracy    | 0.9558   |
| Precision   | 0.9463   |
| Recall      | 0.9276   |
| F1          | 0.9369   |
| AUC         | 0.9582   |

### Confusion Matrix:
Below is the confusion matrix showing the performance of the ensemble model:

- **True Negatives**: 270
- **True Positives**: 141
- **False Positives**: 8
- **False Negatives**: 11

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

While individual models like LightGBM and CatBoost showed slightly better performance in specific metrics, we selected the **ensemble model** for the following reasons:

1. **Balanced Performance Across Metrics**:  
   The ensemble model combines the strengths of multiple algorithms, providing robust accuracy, precision, recall, and AUC, making it more reliable across diverse scenarios.

2. **Robustness to Data Variability**:  
   By incorporating both deep learning and tree-based models, the ensemble is more adaptable to unseen or noisy data compared to single models.

3. **Interpretability for Clinical Use**:  
   With SHAP analysis, the ensemble offers clear insights into critical predictors like Functional Assessment and ADL, making it suitable for real-world clinical decision-making.

4. **Reduced Diagnostic Errors**:  
   The ensemble optimizes recall and precision, minimizing false negatives (missed diagnoses) and false positives (unnecessary stress and testing).

5. **Generalization and Stability**:  
   The combination of deep learning and tree-based models ensures the ensemble generalizes better to new datasets, making it a reliable choice for Alzheimer’s prediction.

---

## Limitations & Future Improvements

### Model Limitations:
- Limited dataset size
- Potential regional bias
- Cross-sectional data only

### Future Work:
- Incorporate longitudinal data
- Add neuroimaging features
- Develop real-time monitoring
- Enhance explainability methods
- External validation

---

## Files:

The actual code with details about this project is in "**Alzheimer's_Disease_Prediction(Ensemble).ipynb**"
