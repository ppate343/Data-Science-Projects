### **Diabetes Classification**

**Business Problem:**  
The goal of this project is to predict whether individuals in the Pima Indians Diabetes Database, collected by the "National Institute of Diabetes and Digestive and Kidney Diseases," have diabetes or not. Early detection of diabetes allows for timely treatment and management, reducing health risks associated with the disease. The dataset contains various health indicators such as insulin levels, BMI, age, and more. Using logistic regression, we aim to classify whether a subject has diabetes based on these indicators.

---

**Approach:**

1. **Data Cleaning and Baseline Accuracy:**  
   Initially, I clean the dataset by handling missing values and ensuring all features are properly encoded. To establish a baseline, I calculate accuracy for the logistic regression model without tuning any parameters. This allows us to compare the performance of later models and determine if improvements are being made.

2. **Logistic Regression Model:**  
   I fit a logistic regression model to the data and analyze its performance using key metrics, including **accuracy**, **recall**, **precision**, **sensitivity**, and **specificity**. The following metrics were observed for the baseline model:

   - **True Positives (TP):** 23  
   - **True Negatives (TN):** 42  
   - **False Positives (FP):** 65  
   - **False Negatives (FN):** 24  
   
   - **Accuracy:** 42.2%  
   - **Recall (Sensitivity):** 48.9%  
   - **Precision:** 26.1%  
   - **Specificity:** 39.3%

   I also plotted the logistic regression curve, visualizing the relationship between insulin levels and the outcome (whether the subject has diabetes).

3. **Logistic Regression with No Penalty:**  
   To improve the model, I removed the regularization penalty (`penalty=None`) and observed improved metrics:

   - **TP:** 29  
   - **TN:** 98  
   - **FP:** 9  
   - **FN:** 18  
   
   - **Accuracy:** 82.5%  
   - **Recall (Sensitivity):** 61.7%  
   - **Precision:** 76.3%  
   - **Specificity:** 91.6%

4. **Threshold Adjustment (4% and 6%):**  
   I further experimented by adjusting the classification thresholds to fine-tune model performance.  
   
   - **Threshold = 4%:**  
     - **TP:** 34  
     - **TN:** 88  
     - **FP:** 19  
     - **FN:** 13  
     - **Accuracy:** 79.2%  
     - **Recall (Sensitivity):** 72.3%  
     - **Precision:** 64.2%  
     - **Specificity:** 82.2%
   
   - **Threshold = 6%:**  
     - **TP:** 26  
     - **TN:** 100  
     - **FP:** 7  
     - **FN:** 21  
     - **Accuracy:** 81.8%  
     - **Recall (Sensitivity):** 55.3%  
     - **Precision:** 78.8%  
     - **Specificity:** 93.5%

5. **Logistic Regression with L2 Penalty (C=0.01):**  
   I also tested logistic regression with L2 regularization and a regularization strength of `C=0.01`. This model showed the following performance:

   - **TP:** 28  
   - **TN:** 97  
   - **FP:** 10  
   - **FN:** 19  
   
   - **Accuracy:** 81.2%  
   - **Recall (Sensitivity):** 59.6%  
   - **Precision:** 73.7%  
   - **Specificity:** 90.7%

6. **Model Comparison (ROC Curves):**  
   I plotted ROC curves to compare the performance of the models. The **Area Under the Curve (AUC)** for each model is as follows:
   
   - **Baseline Model AUC:** 0.441  
   - **Model without Penalty AUC:** 0.766  
   - **Model with Threshold Adjusted to 4% AUC:** 0.751

   These results indicate that the model without regularization achieved the best balance between sensitivity and specificity.

7. **Histogram and Best Model:**  
   I created a histogram of the best-performing classifier (Model 3, with threshold = 4%) to visualize the distribution of predictions. This model provided a good balance between recall and precision.

---

**Results and Analysis:**

- The model with the best performance (Threshold = 4%) achieved a recall of **72.3%** and a precision of **64.2%**, indicating a strong ability to correctly classify diabetic individuals.
- The model with L2 regularization (`C=0.01`) showed decent performance, with a balanced accuracy of **81.2%**, but had slightly lower recall compared to the threshold-adjusted model.
- Overall, adjusting thresholds allowed for better fine-tuning of sensitivity and specificity, improving classification outcomes based on the business needs (e.g., focusing on reducing false negatives in healthcare).

---

**Additional Testing with SGD Classifier:**

I also tested the model using a **Stochastic Gradient Descent Classifier** (`SGDClassifier`) with L2 regularization and evaluated its performance with a **Balanced Accuracy Score**. After fitting the model and predicting values:

- **Balanced Accuracy Score:** `0.8664`

This indicates that the SGD classifier effectively handles class imbalances, achieving strong balanced accuracy for this dataset.

---

**Why These Steps Were Taken:**

1. **Data Cleaning & Baseline Accuracy:** Cleaning ensures a valid dataset, and baseline accuracy provides a reference for model improvements.
2. **Logistic Regression:** Logistic regression is a suitable model for binary classification and provides interpretable coefficients for health indicators like insulin levels.
3. **Regularization & Threshold Tuning:** Regularization (L2 penalty) prevents overfitting, while adjusting thresholds allows for tuning the trade-off between false positives and false negatives based on the specific needs of diabetes detection.
4. **ROC & AUC Analysis:** The ROC curve helps visualize the trade-offs between sensitivity and specificity across different models, while AUC gives a single measure of overall model performance.

