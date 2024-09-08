### 1. **Customer Lifetime Value Prediction**

**Business Problem:**  
Customer Lifetime Value (CLV) is the total revenue a business can expect from a customer throughout their relationship with the company. For an auto insurance company, predicting CLV is essential for identifying and retaining high-value customers, optimizing marketing budgets, and improving profitability. Retaining valuable customers is cheaper than acquiring new ones, making CLV a key metric for business growth.

---

**Approach:**

1. **Data Cleaning and Preparation:**  
   To ensure the data is ready for modeling, I clean it by handling missing values, removing outliers, and encoding categorical variables using **one-hot encoding**. This step ensures that all data types are numerical, which is essential for machine learning models.

2. **Feature Engineering:**  
   I create interaction terms and higher-degree polynomial terms using `PolynomialFeatures`. This helps capture nonlinear relationships between features, enriching the dataset with additional predictive power. The new feature matrix is then **fit-transformed** to apply these transformations.

3. **Data Standardization:**  
   Before fitting models, I standardize the data using `StandardScaler` to ensure that each feature has a mean of 0 and a standard deviation of 1. Standardizing is critical, especially when using models like Ridge, Lasso, and ElasticNet, which are sensitive to the scale of features.

4. **Train-Test Split:**  
   The dataset is split into training and testing sets using `train_test_split`. This step allows us to train the model on one portion of the data and test it on unseen data to evaluate performance and avoid overfitting.

---

**Modeling:**

I train the following models on the prepared dataset to compare performance:

- **Linear Regression:** A baseline model that assumes a linear relationship between features and the target.
- **Ridge Regression:** Adds a penalty on the size of coefficients to prevent overfitting.
- **Lasso Regression:** Performs both variable selection and regularization by driving some coefficients to zero.
- **Elastic Net Regression:** Combines the penalties of both Ridge and Lasso, allowing for a balanced regularization.
- **Linear Regression (Selected Features):** After feature selection using `SequentialFeatureSelector`, I train a new linear model with the most relevant features to reduce noise and improve performance.

---

**Results and Analysis:**

The following table shows the Mean Squared Error (MSE) for each model:

| **Model**                            | **Mean Squared Error (MSE)**       |
|---------------------------------------|------------------------------------|
| Linear Regression                     | 0.11048051028093514                |
| Ridge Regression                      | 0.1101501999617784                 |
| Lasso CV                              | 0.10992600726531618                |
| Elastic Net CV                        | 0.10992600726531618                |
| Linear Regression (Selected Features) | 0.11077019282893105                |

- **Lasso CV and Elastic Net CV** yielded the lowest MSE (`0.10992600726531618`), showing a slight improvement over Linear and Ridge regression. This suggests that both **Lasso** and **Elastic Net** effectively handled feature selection, reducing overfitting by driving irrelevant feature coefficients to zero.
  
- **Ridge Regression** slightly outperformed the baseline Linear Regression, indicating that controlling the size of coefficients helped with generalization to the test set.
  
- **Linear Regression with Sequential Feature Selection** performed slightly worse than the baseline Linear model. This could indicate that feature selection did not provide enough meaningful reduction in noise or irrelevant data for this particular model.

---

**Why These Steps Were Taken:**

1. **Data Cleaning & One-Hot Encoding:** Categorical variables must be converted into a numerical form to be processed by machine learning algorithms. One-hot encoding ensures that no implicit ordering is introduced, which could bias the model.

2. **Polynomial Feature Transformation:** Polynomial transformations allow the model to account for nonlinear relationships, which are often present in real-world data. By adding higher-order terms, the model gains flexibility in fitting more complex patterns.

3. **Standardization:** Many machine learning models, especially regularization-based models like Ridge, Lasso, and ElasticNet, are sensitive to the scale of input features. Standardizing ensures that each feature contributes equally to the model.

4. **Train-Test Split:** This ensures that the model's performance is evaluated on unseen data, giving us a true measure of how well the model will generalize to new, unseen data.

5. **Model Comparison:** Trying multiple models allows us to determine which approach best handles the trade-off between bias and variance. Lasso and ElasticNet, in particular, show the advantage of combining regularization with feature selection to avoid overfitting while maintaining predictive accuracy.



