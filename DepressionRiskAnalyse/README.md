
# Model Card: Depression Risk Predictor

## 1. Model Details
- **Name:** Depression Risk Predictor  
- **Model type:** Supervised classifier (e.g., Random Forest, Logistic Regression)  
- **Framework:** Python (scikit-learn)  
- **Authors:** Bruno Valniery / [brunovalniery.github.io]  
- **Version:** 1.0  

> This model was trained to predict depression risk based on personal and behavioral characteristics. The model uses synthetically generated data inspired by research literature.

---

## 2. Intended Use
- **Purpose:** To support academic studies and initial analyses of depression risk factors.  
- **Target users:** Researchers, mental health professionals, data science students.  
- **Recommended use cases:** Controlled research and educational environments.  

⚠️ **It's not recommended for real clinical use.**

---

## 3. Factors
- **Included factors:**
  - Age
  - Gender
  - Family history of depression
  - Job satisfaction
  - Study hours
- **Excluded factors:** Prior mental health conditions, medication use, real socioeconomic context.

---

## 4. Metrics
- **Evaluated metrics:** Accuracy, Precision, Recall, F1-score, Confusion Matrix  
- **Performance (example):**
  - Accuracy: 0.85
  - F1-score for positive class: 0.78
  - Note: Class imbalance may affect evaluation metrics


- **exemplo**
In order to follow the performance of machine learning experiments, the project marked certains stage outputs of the data pipeline as metrics. The metrics adopted are: [accuracy](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.accuracy_score.html), [f1](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.f1_score.html#sklearn.metrics.f1_score), [precision](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.precision_score.html#sklearn.metrics.precision_score), [recall](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.recall_score.html#sklearn.metrics.recall_score).

To calculate the evaluations metrics is only necessary to run:

```bash
dvc metrics show
```

The follow results will be shown:

 **Path**                        | **Accuracy** | **F1** | **Precision** | **Recall** | 
---------------------------------|--------------|--------|---------------|------------|
 pipeline/data/train_scores.json | 0.8328       | 0.6321 | 0.6728        | 0.5959     |  
 pipeline/data/test_scores.json  | 0.8382       | 0.6347 | 0.6960        | 0.5833     |

---

## 5. Training Data
- **Data source:** Synthetically generated based on realistic distributions  
- **Dataset size:** ~1000 samples  
- **Data license:** Free/academic use with proper attribution

---

## 6. Evaluation Data
- **Split:** 80% training / 20% testing  
- **Cross-validation:** 5-fold cross-validation  
- **Evaluation criteria:** Model tested on holdout data

---

## 7. Ethical Considerations
- **Bias:** The model may reflect bias in synthetic data, including class imbalance or lack of representativeness  
- **Limitations:** Not validated on real clinical data. May lead to misuse if interpreted as a diagnostic tool  
- **Misuse risks:** May be wrongly perceived as an automated diagnostic system

---

## 8. Caveats and Recommendations
- It is recommended to retrain the model using real, representative data before any practical application  
- The model should be periodically audited for bias and performance