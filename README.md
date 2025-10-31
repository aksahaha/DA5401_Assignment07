# DA5401_Assignment07


Abhishek Kumar : DA25C002
# 🛰️ DA5401 A7: Multi-Class Model Selection using ROC and Precision-Recall Curves

## 🎯 Objective
This project focuses on **multi-class model selection** using the **UCI Landsat Satellite dataset**, which involves classifying different land cover types based on satellite image data.  
The primary goal is to **compare multiple classification models** using **Receiver Operating Characteristic (ROC)** and **Precision-Recall Curves (PRC)** to determine which model performs best — not just by accuracy, but across **different thresholds and class distributions**.

---

## 📚 Dataset
- **Name:** UCI Landsat Satellite Dataset  
- **Source:** [UCI Machine Learning Repository – Statlog (Landsat Satellite)](https://archive.ics.uci.edu/dataset/146/statlog+landsat+satellite)  
- **Classes:** 6 primary land cover types (excluding "all types present")  
- **Features:** 36 continuous attributes per sample  
- **Task:** Multi-class classification  

---

## 🧠 Models Used
A total of **six primary models** (plus two bonus models) are implemented to represent a wide performance spectrum — from poor baselines to advanced learners.

| Model | Library | Expected Performance |
|:--|:--|:--|
| KNeighborsClassifier | `sklearn.neighbors` | Moderate/Good |
| DecisionTreeClassifier | `sklearn.tree` | Moderate |
| DummyClassifier (Prior) | `sklearn.dummy` | Baseline (may show AUC ≈ 0.5 or < 0.5) |
| LogisticRegression | `sklearn.linear_model` | Good baseline |
| GaussianNB | `sklearn.naive_bayes` | Poor/Varies |
| SVC (probability=True) | `sklearn.svm` | Good/High |
| **Bonus:** RandomForestClassifier | `sklearn.ensemble` | Strong performance |
| **Bonus:** XGBoostClassifier | `xgboost` | Strong performance |
| **Extra:** Misconfigured Perceptron | `sklearn.linear_model` | AUC < 0.5 (intentionally poor) |

---

## ⚙️ Implementation Workflow

### **Part A: Data Preparation and Baseline**
1. Load and standardize the dataset using `StandardScaler`.  
2. Split into training (80%) and testing (20%) sets.  
3. Train all six classifiers on the training data.  
4. Evaluate **Accuracy** and **Weighted F1-Score** for each model.

### **Part B: ROC Curve Analysis**
1. Use **One-vs-Rest (OvR)** strategy to compute ROC for all classes.  
2. Generate a **Macro-averaged ROC curve** for each model.  
3. Identify:
   - The **best model** (highest Macro-Averaged AUC).  
   - The **worst model** (AUC ≤ 0.5) and explain its behavior.  

### **Part C: Precision-Recall Curve (PRC) Analysis**
1. Compute **Macro- and Weighted-Average PRC** using OvR.  
2. Plot all models on a single PRC chart.  
3. Identify:
   - The **model with the highest Average Precision (AP)**.  
   - The **worst-performing model** and explain why its curve drops sharply.

### **Part D: Comprehensive Model Comparison**
1. Compare rankings across **Accuracy**, **F1-Score**, **ROC-AUC**, and **PRC-AP**.  
2. Discuss trade-offs between ROC and PRC insights.  
3. Recommend the **best model** considering balanced performance and interpretability.

---

## 📊 Key Findings
- **Best Performing Model:** `SVC`  
  - Highest ROC-AUC (≈ 0.985)  
  - Strong PRC-AP and balanced F1-score  
  - Excellent performance across thresholds  

- **Worst Performing Model:** `DummyClassifier (Constant Strategy)`  
  - Accuracy ≈ 0.23, ROC-AUC = 0.50  
  - Performs like random guessing (no learning).  

- **Intentionally Poor Model:** `Misconfigured Perceptron`  
  - ROC-AUC ≈ 0.48 (< 0.5), showing systematic misclassification.  

---

## 🧩 Insights and Learning Outcomes
- ROC Curves are effective for **evaluating class separability**, but can overstate performance under imbalance.  
- PRC is **more reliable for imbalanced data**, focusing on positive-class performance.  
- A model can have **high ROC-AUC but poor PRC-AP** if it struggles with precision when recall increases.  
- Intentional model misconfiguration helps visualize **worse-than-random** classifiers and their inverted ROC behavior.

---

## 🪄 Tools & Libraries
- `scikit-learn` for model training, metrics, and visualization  
- `matplotlib` for ROC and PRC plots  
- `numpy` and `pandas` for data manipulation  
- `xgboost` for advanced ensemble modeling  

---

