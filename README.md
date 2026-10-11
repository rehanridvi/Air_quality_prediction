# 🌫️ Air Quality Index (AQI) Classification — Bangladesh

End-to-end machine learning pipeline to predict **Air Quality Index categories** across 16 locations in Bangladesh, using meterological and temporal data. Covers data cleaning → feature engineering → EDA → 8-model training (ML + deep learning) → credit-standard evaluation → confusion matrix analysis.

**🏆 Best Model: XGBoost — 74.11% Accuracy**

---

## 📈 Results

### Baseline Model Comparison (30% held-out test set — 154,297 samples)

| Model | Accuracy | MAE | MSE | Notes |
|---|---|---|---|---|
| **XGBoost** 🥇 | **0.7411** | **0.2891** | **0.3497** | Best on all metrics |
| Random Forest | 0.7568 | — | — | Baseline RF (100 trees, depth 20) |
| LightGBM | 0.7168 | 0.3180 | 0.3875 | Close runner-up |
| Neural Network | 0.7169 | 0.3182 | 0.3884 | 3-layer MLP + BatchNorm |
| Decision Tree | 0.7129 | 0.3232 | 0.3953 | Entropy criterion |
| KNN | 0.7101 | 0.3266 | 0.4002 | Distance-weighted, Manhattan |
| CatBoost | 0.7059 | 0.3294 | 0.4001 | Tuned depth 8 |
| AdaBoost | 0.6618 | 0.3844 | 0.4770 | Weakest performer |

Evaluated on a 20% held-out test split from 944,182 total records. **XGBoost wins decisively on continuous error metrics (MAE/MSE)** while Random Forest and XGBoost are neck-and-neck on raw accuracy — confirming that **tree-based ensembles dominate this feature space**, but the neural network and LightGBM remain strong contenders.

### Per-Class Performance (XGBoost)

| Class | Precision | Recall | F1-score | Support |
|---|---|---|---|---|
| 0 (Good) | 0.79 | 0.82 | 0.81 | 69,987 |
| 1 (Moderate) | 0.70 | 0.68 | 0.69 | 57,664 |
| 2 (Unhealthy) | 0.69 | 0.67 | 0.68 | 26,646 |

---

## 📊 Dataset

- **Source:** [Air Quality Index of Bangladesh (Kaggle)](https://www.kaggle.com/datasets) — `air_quality_index_dataset.xlsx`
- **Size:** 944,182 records across 16 monitoring stations
- **Task:** Multiclass classification — **Good / Moderate / Unhealthy** (3 classes, based on PM2.5 thresholds)
- **Class distribution:** Imbalanced — Good: 350,697 · Moderate: 287,490 · Unhealthy: 133,298
- **Locations:** Rajshahi, BARC, Gazipur, Darussalam, Agrabad Chittagong, Barishal, Khulna, Sylhet, TV st-Chittagong, Narayonganj, Sangsad, Rangpur, Cumilla, Mymansingh, Narsingdi, Savar

### Raw Features (23 columns)

| Group | Features |
|---|---|
| Temporal | Date, Time, Location |
| Pollutants | SO2, NO, NO2, NOX, CO, CO 8hr, O3, O3 8hr, PM2.5, PM10 |
| Weather | Wind Speed, Wind Dir, Temperature, RH, Solar Rad, BP, Rain, V Wind Speed |

---

## 🧹 Data Cleaning

- **Columns dropped (16):** `Unnamed: 20`, `Unnamed: 21`, `Rain`, `V Wind Speed`, `CO 8hr`, `O3 8hr`, `CO`, `NO`, `NO2`, `NOX`, `SO2`, `O3`, `PM10`, `Solar Rad`, `BP`, `Wind Dir` — high null rates (some >85%) made them unusable
- **Datetime handling:** Date + Time merged into a single `Datetime` column; original columns dropped
- **Numeric parsing:** Comma-to-dot replacement applied to `PM2.5`, `Temperature`, `RH`, `Wind Speed`, then coerced to float
- **Missing value strategy:**
  - Location-wise median imputation for `PM2.5`, `Temperature`, `RH`, `Wind Speed`
  - Global median fallback for remaining gaps
- **Final cleaned features (6):** `Temperature`, `RH`, `Wind Speed`, `Hour`, `Day`, `Month`

---

## 🏷️ Feature Engineering

- **AQI category** derived from PM2.5 thresholds:
  - `PM2.5 ≤ 50` → **Good** (label 0)
  - `50 < PM2.5 ≤ 100` → **Moderate** (label 1)
  - `PM2.5 > 100` → **Unhealthy** (label 2)
- **Temporal features extracted:** Hour, Day, Month, Weekday
- **Label encoding** applied to AQI categories
- **Correlation heatmap** revealed temperature and RH as strongest predictors

---

## 🔄 Pipeline
# 🌫️ Air Quality Index (AQI) Classification — Bangladesh

End-to-end machine learning pipeline to predict **Air Quality Index categories** across 16 locations in Bangladesh, using meterological and temporal data. Covers data cleaning → feature engineering → EDA → 8-model training (ML + deep learning) → credit-standard evaluation → confusion matrix analysis.

**🏆 Best Model: XGBoost — 74.11% Accuracy**

---

## 📈 Results

### Baseline Model Comparison (30% held-out test set — 154,297 samples)

| Model | Accuracy | MAE | MSE | Notes |
|---|---|---|---|---|
| **XGBoost** 🥇 | **0.7411** | **0.2891** | **0.3497** | Best on all metrics |
| Random Forest | 0.7568 | — | — | Baseline RF (100 trees, depth 20) |
| LightGBM | 0.7168 | 0.3180 | 0.3875 | Close runner-up |
| Neural Network | 0.7169 | 0.3182 | 0.3884 | 3-layer MLP + BatchNorm |
| Decision Tree | 0.7129 | 0.3232 | 0.3953 | Entropy criterion |
| KNN | 0.7101 | 0.3266 | 0.4002 | Distance-weighted, Manhattan |
| CatBoost | 0.7059 | 0.3294 | 0.4001 | Tuned depth 8 |
| AdaBoost | 0.6618 | 0.3844 | 0.4770 | Weakest performer |

Evaluated on a 20% held-out test split from 944,182 total records. **XGBoost wins decisively on continuous error metrics (MAE/MSE)** while Random Forest and XGBoost are neck-and-neck on raw accuracy — confirming that **tree-based ensembles dominate this feature space**, but the neural network and LightGBM remain strong contenders.

### Per-Class Performance (XGBoost)

| Class | Precision | Recall | F1-score | Support |
|---|---|---|---|---|
| 0 (Good) | 0.79 | 0.82 | 0.81 | 69,987 |
| 1 (Moderate) | 0.70 | 0.68 | 0.69 | 57,664 |
| 2 (Unhealthy) | 0.69 | 0.67 | 0.68 | 26,646 |

---

## 📊 Dataset

- **Source:** [Air Quality Index of Bangladesh (Kaggle)](https://www.kaggle.com/datasets) — `air_quality_index_dataset.xlsx`
- **Size:** 944,182 records across 16 monitoring stations
- **Task:** Multiclass classification — **Good / Moderate / Unhealthy** (3 classes, based on PM2.5 thresholds)
- **Class distribution:** Imbalanced — Good: 350,697 · Moderate: 287,490 · Unhealthy: 133,298
- **Locations:** Rajshahi, BARC, Gazipur, Darussalam, Agrabad Chittagong, Barishal, Khulna, Sylhet, TV st-Chittagong, Narayonganj, Sangsad, Rangpur, Cumilla, Mymansingh, Narsingdi, Savar

### Raw Features (23 columns)

| Group | Features |
|---|---|
| Temporal | Date, Time, Location |
| Pollutants | SO2, NO, NO2, NOX, CO, CO 8hr, O3, O3 8hr, PM2.5, PM10 |
| Weather | Wind Speed, Wind Dir, Temperature, RH, Solar Rad, BP, Rain, V Wind Speed |

---

## 🧹 Data Cleaning

- **Columns dropped (16):** `Unnamed: 20`, `Unnamed: 21`, `Rain`, `V Wind Speed`, `CO 8hr`, `O3 8hr`, `CO`, `NO`, `NO2`, `NOX`, `SO2`, `O3`, `PM10`, `Solar Rad`, `BP`, `Wind Dir` — high null rates (some >85%) made them unusable
- **Datetime handling:** Date + Time merged into a single `Datetime` column; original columns dropped
- **Numeric parsing:** Comma-to-dot replacement applied to `PM2.5`, `Temperature`, `RH`, `Wind Speed`, then coerced to float
- **Missing value strategy:**
  - Location-wise median imputation for `PM2.5`, `Temperature`, `RH`, `Wind Speed`
  - Global median fallback for remaining gaps
- **Final cleaned features (6):** `Temperature`, `RH`, `Wind Speed`, `Hour`, `Day`, `Month`

---

## 🏷️ Feature Engineering

- **AQI category** derived from PM2.5 thresholds:
  - `PM2.5 ≤ 50` → **Good** (label 0)
  - `50 < PM2.5 ≤ 100` → **Moderate** (label 1)
  - `PM2.5 > 100` → **Unhealthy** (label 2)
- **Temporal features extracted:** Hour, Day, Month, Weekday
- **Label encoding** applied to AQI categories
- **Correlation heatmap** revealed temperature and RH as strongest predictors

---

## 🔄 Pipeline
# 🌫️ Air Quality Index (AQI) Classification — Bangladesh

End-to-end machine learning pipeline to predict **Air Quality Index categories** across 16 locations in Bangladesh, using meterological and temporal data. Covers data cleaning → feature engineering → EDA → 8-model training (ML + deep learning) → credit-standard evaluation → confusion matrix analysis.

**🏆 Best Model: XGBoost — 74.11% Accuracy**

---

## 📈 Results

### Baseline Model Comparison (30% held-out test set — 154,297 samples)

| Model | Accuracy | MAE | MSE | Notes |
|---|---|---|---|---|
| **XGBoost** 🥇 | **0.7411** | **0.2891** | **0.3497** | Best on all metrics |
| Random Forest | 0.7568 | — | — | Baseline RF (100 trees, depth 20) |
| LightGBM | 0.7168 | 0.3180 | 0.3875 | Close runner-up |
| Neural Network | 0.7169 | 0.3182 | 0.3884 | 3-layer MLP + BatchNorm |
| Decision Tree | 0.7129 | 0.3232 | 0.3953 | Entropy criterion |
| KNN | 0.7101 | 0.3266 | 0.4002 | Distance-weighted, Manhattan |
| CatBoost | 0.7059 | 0.3294 | 0.4001 | Tuned depth 8 |
| AdaBoost | 0.6618 | 0.3844 | 0.4770 | Weakest performer |

Evaluated on a 20% held-out test split from 944,182 total records. **XGBoost wins decisively on continuous error metrics (MAE/MSE)** while Random Forest and XGBoost are neck-and-neck on raw accuracy — confirming that **tree-based ensembles dominate this feature space**, but the neural network and LightGBM remain strong contenders.

### Per-Class Performance (XGBoost)

| Class | Precision | Recall | F1-score | Support |
|---|---|---|---|---|
| 0 (Good) | 0.79 | 0.82 | 0.81 | 69,987 |
| 1 (Moderate) | 0.70 | 0.68 | 0.69 | 57,664 |
| 2 (Unhealthy) | 0.69 | 0.67 | 0.68 | 26,646 |

---

## 📊 Dataset

- **Source:** [Air Quality Index of Bangladesh (Kaggle)](https://www.kaggle.com/datasets) — `air_quality_index_dataset.xlsx`
- **Size:** 944,182 records across 16 monitoring stations
- **Task:** Multiclass classification — **Good / Moderate / Unhealthy** (3 classes, based on PM2.5 thresholds)
- **Class distribution:** Imbalanced — Good: 350,697 · Moderate: 287,490 · Unhealthy: 133,298
- **Locations:** Rajshahi, BARC, Gazipur, Darussalam, Agrabad Chittagong, Barishal, Khulna, Sylhet, TV st-Chittagong, Narayonganj, Sangsad, Rangpur, Cumilla, Mymansingh, Narsingdi, Savar

### Raw Features (23 columns)

| Group | Features |
|---|---|
| Temporal | Date, Time, Location |
| Pollutants | SO2, NO, NO2, NOX, CO, CO 8hr, O3, O3 8hr, PM2.5, PM10 |
| Weather | Wind Speed, Wind Dir, Temperature, RH, Solar Rad, BP, Rain, V Wind Speed |

---

## 🧹 Data Cleaning

- **Columns dropped (16):** `Unnamed: 20`, `Unnamed: 21`, `Rain`, `V Wind Speed`, `CO 8hr`, `O3 8hr`, `CO`, `NO`, `NO2`, `NOX`, `SO2`, `O3`, `PM10`, `Solar Rad`, `BP`, `Wind Dir` — high null rates (some >85%) made them unusable
- **Datetime handling:** Date + Time merged into a single `Datetime` column; original columns dropped
- **Numeric parsing:** Comma-to-dot replacement applied to `PM2.5`, `Temperature`, `RH`, `Wind Speed`, then coerced to float
- **Missing value strategy:**
  - Location-wise median imputation for `PM2.5`, `Temperature`, `RH`, `Wind Speed`
  - Global median fallback for remaining gaps
- **Final cleaned features (6):** `Temperature`, `RH`, `Wind Speed`, `Hour`, `Day`, `Month`

---

## 🏷️ Feature Engineering

- **AQI category** derived from PM2.5 thresholds:
  - `PM2.5 ≤ 50` → **Good** (label 0)
  - `50 < PM2.5 ≤ 100` → **Moderate** (label 1)
  - `PM2.5 > 100` → **Unhealthy** (label 2)
- **Temporal features extracted:** Hour, Day, Month, Weekday
- **Label encoding** applied to AQI categories
- **Correlation heatmap** revealed temperature and RH as strongest predictors

---

## 🔄 Pipeline
# 🌫️ Air Quality Index (AQI) Classification — Bangladesh

End-to-end machine learning pipeline to predict **Air Quality Index categories** across 16 locations in Bangladesh, using meterological and temporal data. Covers data cleaning → feature engineering → EDA → 8-model training (ML + deep learning) → credit-standard evaluation → confusion matrix analysis.

**🏆 Best Model: XGBoost — 74.11% Accuracy**

---

## 📈 Results

### Baseline Model Comparison (30% held-out test set — 154,297 samples)

| Model | Accuracy | MAE | MSE | Notes |
|---|---|---|---|---|
| **XGBoost** 🥇 | **0.7411** | **0.2891** | **0.3497** | Best on all metrics |
| Random Forest | 0.7568 | — | — | Baseline RF (100 trees, depth 20) |
| LightGBM | 0.7168 | 0.3180 | 0.3875 | Close runner-up |
| Neural Network | 0.7169 | 0.3182 | 0.3884 | 3-layer MLP + BatchNorm |
| Decision Tree | 0.7129 | 0.3232 | 0.3953 | Entropy criterion |
| KNN | 0.7101 | 0.3266 | 0.4002 | Distance-weighted, Manhattan |
| CatBoost | 0.7059 | 0.3294 | 0.4001 | Tuned depth 8 |
| AdaBoost | 0.6618 | 0.3844 | 0.4770 | Weakest performer |

Evaluated on a 20% held-out test split from 944,182 total records. **XGBoost wins decisively on continuous error metrics (MAE/MSE)** while Random Forest and XGBoost are neck-and-neck on raw accuracy — confirming that **tree-based ensembles dominate this feature space**, but the neural network and LightGBM remain strong contenders.

### Per-Class Performance (XGBoost)

| Class | Precision | Recall | F1-score | Support |
|---|---|---|---|---|
| 0 (Good) | 0.79 | 0.82 | 0.81 | 69,987 |
| 1 (Moderate) | 0.70 | 0.68 | 0.69 | 57,664 |
| 2 (Unhealthy) | 0.69 | 0.67 | 0.68 | 26,646 |

---

## 📊 Dataset

- **Source:** [Air Quality Index of Bangladesh (Kaggle)](https://www.kaggle.com/datasets) — `air_quality_index_dataset.xlsx`
- **Size:** 944,182 records across 16 monitoring stations
- **Task:** Multiclass classification — **Good / Moderate / Unhealthy** (3 classes, based on PM2.5 thresholds)
- **Class distribution:** Imbalanced — Good: 350,697 · Moderate: 287,490 · Unhealthy: 133,298
- **Locations:** Rajshahi, BARC, Gazipur, Darussalam, Agrabad Chittagong, Barishal, Khulna, Sylhet, TV st-Chittagong, Narayonganj, Sangsad, Rangpur, Cumilla, Mymansingh, Narsingdi, Savar

### Raw Features (23 columns)

| Group | Features |
|---|---|
| Temporal | Date, Time, Location |
| Pollutants | SO2, NO, NO2, NOX, CO, CO 8hr, O3, O3 8hr, PM2.5, PM10 |
| Weather | Wind Speed, Wind Dir, Temperature, RH, Solar Rad, BP, Rain, V Wind Speed |

---

## 🧹 Data Cleaning

- **Columns dropped (16):** `Unnamed: 20`, `Unnamed: 21`, `Rain`, `V Wind Speed`, `CO 8hr`, `O3 8hr`, `CO`, `NO`, `NO2`, `NOX`, `SO2`, `O3`, `PM10`, `Solar Rad`, `BP`, `Wind Dir` — high null rates (some >85%) made them unusable
- **Datetime handling:** Date + Time merged into a single `Datetime` column; original columns dropped
- **Numeric parsing:** Comma-to-dot replacement applied to `PM2.5`, `Temperature`, `RH`, `Wind Speed`, then coerced to float
- **Missing value strategy:**
  - Location-wise median imputation for `PM2.5`, `Temperature`, `RH`, `Wind Speed`
  - Global median fallback for remaining gaps
- **Final cleaned features (6):** `Temperature`, `RH`, `Wind Speed`, `Hour`, `Day`, `Month`

---

## 🏷️ Feature Engineering

- **AQI category** derived from PM2.5 thresholds:
  - `PM2.5 ≤ 50` → **Good** (label 0)
  - `50 < PM2.5 ≤ 100` → **Moderate** (label 1)
  - `PM2.5 > 100` → **Unhealthy** (label 2)
- **Temporal features extracted:** Hour, Day, Month, Weekday
- **Label encoding** applied to AQI categories
- **Correlation heatmap** revealed temperature and RH as strongest predictors

---

## 🔄 Pipeline
air_quality_index_dataset.xlsx
→ Multi-sheet concat + Location tagging (944,182 rows)
→ Column drop (16 low-value cols)
→ Datetime construction + Location-wise median imputation
→ AQI categorization + temporal feature extraction
→ Correlation analysis (EDA)
→ Label encoding + StandardScaler
→ 80/20 train-test split
→ Model Training:
Decision Tree | KNN | AdaBoost | XGBoost
LightGBM | CatBoost | Random Forest | Neural Network (Keras)
→ Confusion Matrix + MAE/MSE + Classification Report
→ Yearly trend validation (actual vs predicted)

---

## 🧠 Neural Network Architecture
Dense(256, ReLU) → BatchNormalization → Dropout(0.1)
Dense(128, ReLU) → BatchNormalization → Dropout(0.1)
Dense(64, ReLU)
Dense(3, Softmax)


- **Optimizer:** Adam (lr = 0.0005)
- **Loss:** Categorical cross-entropy
- **Callbacks:** EarlyStopping (patience=5), ReduceLROnPlateau (factor=0.5, patience=3)
- **Test Accuracy:** 71.69% after 39 epochs (best val_loss: 0.6329)

---

## 💡 Key Takeaways

1. **XGBoost dominates continuous error metrics** (MAE 0.289, MSE 0.350) — the most reliable classifier for AQI prediction.
2. **Random Forest achieves highest raw accuracy (75.68%)** but is less stable on ranking-sensitive metrics.
3. **Tree ensembles beat AdaBoost significantly** — AdaBoost's 66% accuracy suggests sequential weak learners struggle with this noisy, imbalanced data.
4. **Neural network performs on par with gradient boosting** (71.69%) — but with far more training overhead.
5. **Temporal + weather features are sufficient** — dropping 16 high-null pollutant columns did not harm performance, confirming PM2.5 is the dominant AQI signal.
6. **Yearly trend validation** shows predicted averages track actual AQI closely, indicating no temporal drift.

---

## 🛠️ Stack

**Python** · **scikit-learn** · **XGBoost** · **LightGBM** · **CatBoost** · **TensorFlow / Keras** · **Pandas** · **NumPy** · **Matplotlib** · **Seaborn**
