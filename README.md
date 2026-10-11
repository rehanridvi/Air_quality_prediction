# 🧠 Alzheimer Disease Classification

End-to-end machine learning pipeline to classify Alzheimer's disease from patient data — covering EDA → preprocessing → feature scaling → dataset splitting → 3-model training → confusion-matrix evaluation.
# Dataset link: 
https://www.kaggle.com/datasets/tahmidmir/air-quality-index-of-bangladesh-dataset

# Kaggle Link: 
https://www.kaggle.com/code/sacklinenaienridvi/air-quality-project-cse427/edit

**🏆 Best Model: Decision Tree — 87.44% Accuracy**

---

## 📈 Results

| Model | Accuracy |
|---|---|
| **Decision Tree** ✅ | **87.44%** |
| Logistic Regression | 84.03% |
| K-Nearest Neighbours (KNN) | 73.48% |

Evaluated on a 30% held-out test split. **Decision Tree wins** on accuracy, while **Logistic Regression** remains a strong contender for probabilistic classification. **KNN lags** — likely due to overfitting/underfitting on the scaled feature space.

Confusion matrices were generated for all three models to expose misclassification patterns beyond raw accuracy.

---

## 📊 Dataset

- **Source:** [Alzheimer's Disease Dataset (Kaggle)](https://www.kaggle.com/datasets/rabieelkharoua/alzheimers-disease-dataset/data)
- **Size:** 2,149 data points · 35 features
- **Task:** Binary classification — predicting Alzheimer's diagnosis
- **Class balance:** Imbalanced (classes do not have equal instance counts)

| Feature Type | Count | Examples |
|---|---|---|
| Categorical | 18 | Gender, Ethnicity, EducationLevel, Smoking, FamilyHistoryAlzheimers, Depression, Hypertension, MemoryComplaints, BehavioralProblems, Forgetfulness, Diagnosis (target) |
| Quantitative | 17 | Age, BMI, AlcoholConsumption, PhysicalActivity, DietQuality, SleepQuality, SystolicBP, CholesterolTotal/LDL/HDL, MMSE, FunctionalAssessment, ADL, PatientID, DoctorInCharge |

---

## 🧹 Data Preprocessing

- **Null values handled:** 5,075 total nulls — highest in `DoctorInCharge` and `PatientID`
  - **Solution:** Both columns dropped (no predictive value from null-heavy administrative/ID fields)
- **Categorical encoding:** Label encoding applied
  - Gender → Male: 0, Female: 1
  - Ethnicity → Caucasian: 0, African American: 1, Asian: 2, Other: 3
  - Education → None: 0, High School: 1, Bachelor's: 2, Higher: 3
- **Feature scaling:** Applied to quantitative features
- **Final cleaned records:** 2,149 (all rows retained after column drops)

---

## ✂️ Dataset Splitting

- **Train/Test:** 70% training (≈1,504 rows) / 30% testing (≈645 rows)

---

## 🔄 Pipeline
alzheimers_disease_data.csv
→ Data Exploration + Correlation with labels
→ Preprocessing (null handling, label encoding)
→ Feature Scaling
→ 70/30 Train-Test Split
→ Model Training: Logistic Regression | Decision Tree | KNN
→ Model Selection (accuracy comparison)
→ Confusion Matrix Analysis
→ Conclusion


---

## 💡 Key Takeaways

1. **Decision Tree is the top performer** (87.44%) — most reliable classifier for this dataset.
2. **Logistic Regression is a strong runner-up** (84.03%) — better suited for probabilistic risk scoring.
3. **KNN underperforms** (73.48%) — scaling sensitivity and class imbalance likely hurt performance.
4. **Preprocessing mattered** — dropping high-null administrative columns and label-encoding categoricals was essential before training.

---

## 🛠️ Stack

**Python** · **scikit-learn** · Logistic Regression · Decision Tree · KNN · Pandas · Matplotlib


