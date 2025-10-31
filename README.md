# DA5401_Assignment7_ED22B054

# Landsat Satellite Multi-Class Model Selection Assignment


## Problem Statement

Classify land cover types (6 classes) from satellite image data with high-dimensional features. The main focus is rigorous model selection using both ROC and PRC analysis, highlighting why accuracy is insufficient for multi-class or imbalanced situations.

***

## Assignment Overview (Structure)

### **A. Data Preparation & Baseline Metrics**

| Model         | Accuracy | Weighted F1 |
|---------------|----------|-------------|
| KNN           | 0.90     | 0.90        |
| Decision Tree | 0.85     | 0.85        |
| Dummy         | 0.08     | 0.02        |
| Logistic Reg. | 0.88     | 0.88        |
| Naive Bayes   | 0.80     | 0.80        |
| SVC           | 0.89     | 0.89        |

**Observations:**
- Baseline Dummy confirms minimal discriminative ability.
- F1-score closely reflects accuracy, but is preferred for multi-class performance.
- Naive Bayes and Decision Tree (shallow) have lower performance, confirming the problem's complexity.

***

### **B. ROC Curve Analysis**

#### **ROC Concept & Macro-Averaging**
- ROC computed per class, then macro-averaged for fair multi-class comparison.

#### **Macro-Averaged ROC-AUC Table**

| Model         | Macro ROC-AUC |
|---------------|---------------|
| KNN           | 0.98          |
| Decision Tree | 0.90          |
| Dummy         | 0.50          |
| Logistic Reg. | 0.98          |
| Naive Bayes   | 0.95          |
| SVC           | 0.99          |

**Key Observations:**
- SVC and KNN provide best separability (ROC-AUC close to 1).
- Dummy gives random separability (AUC = 0.5), clear lower bound.
- Decision Tree underperforms, potentially due to lack of depth or overfitting.
- High ROC-AUC does not always translate to high average precision (see PRC next).

***

### **C. PRC (Precision-Recall Curve) Analysis**

| Model         | Macro PRC-AP |
|---------------|--------------|
| KNN           | 0.92         |
| Decision Tree | 0.74         |
| Dummy         | 0.17         |
| Logistic Reg. | 0.87         |
| Naive Bayes   | 0.81         |
| SVC           | 0.92         |

**Insights:**
- KNN and SVC robustly maintain high precision at high recall, best for real-world use with imbalanced positives.
- Dummy classifier drops instantly as recall grows, confirming it's ineffective beyond random baseline.
- Macro-averaging (vs. weighted) ensures minority classes are not overshadowed, critical for satellite data with rare cover types.
- PRC is stricter than ROC when true positives are rare; strong PRC indicates real reliability.

**Extra:** Curve plots are in the notebook, visually confirming tabular trends.

***

### **D. Final Synthesis & Recommendation**

- **Ranking Consistency:**  
  Rankings from F1, ROC-AUC, and PRC-AP broadly align—KNN and SVC always lead, Dummy is always the worst.
- **Best Model:**  
  KNN and SVC are both safe, high-performing choices; Random Forest/XGBoost (Brownie task) also achieve best-in-class results.
- **Dummy Classifier (constant/rarest):**  
  Used for a true “worse than random” scenario, offering a robust lower bound for all metrics.

***

### **Brownie Points: Ensemble & “Bad” Model Results**

| Model         | Accuracy | Weighted F1 | Macro ROC-AUC | Macro PRC-AP |
|---------------|----------|-------------|---------------|--------------|
| RandomForest  | 0.91     | 0.91        | 0.99          | 0.95         |
| XGBoost       | 0.91     | 0.91        | 0.99          | 0.95         |
| Dummy (rare)  | 0.11     | 0.02        | 0.50          | 0.17         |

**Further Insights:**
- Ensemble methods outperform or match single models, confirming their stability and power.
- The DummyClassifier with rare constant is effective for testing the interpretation of ROC/PRC metrics near theoretical minimums.
- All strong classifiers supplement their quantitative lead with clean, tight ROC and PRC curves in the final plots.

***



***

Let me know if you want even more observation bullets for a particular section or a different arrangement!
