# **Health Insurance Feature Importance Analysis Using XGBoost**

This project explores multiple modeling approaches to predict hospital charges using patient demographic and health data. The goal was to compare model performance, interpretability, and overall suitability for forecasting costs for new patients.

This project uses the U.S. Health Insurance [Dataset](https://www.kaggle.com/datasets/teertha/ushealthinsurancedataset), from Kaggle.

## **1. Data Exploration and Preprocessing**

The workflow began with an exploration of the dataset:

* **Checked variable types and distributions** for features like age, BMI, children, smoker, sex, and region
* **Identified skewness** in hospital charges and applied log-transformations for linear modeling
* **Explored categorical variables** such as smoker status, sex, and geographic region, converting them into numerical dummy variables (`region_northwest`, `region_southeast`, `region_southwest`).
* **Created visualizations**, including:

  * Boxplots of charges by region
  * Residual plots for early models
  * Scatterplots of predicted vs. actual values
* **Investigated potential interactions** between variables that could explain nonlinear patterns or curvature in residuals.

These steps helped uncover strong nonlinear trends, substantial heteroskedasticity, and complex interactions.

### **2. Initial Exploration: Linear and GLM Models**

The first step for this analysis was an exploration of linear regression and several GLM formulations (Gamma, log-link, Tweedie). Despite model-tuning, diagnostic plots revealed persistent heteroskedasticity and a curved residual pattern. Even after adding interaction terms, the GLMs were unable to capture the nonlinear structure of the data. This indicated that linear-based models were not the best fit for this prediction task, as they didn't scale as fast as the hospital charges did.

### **3. Tree-Based Models**

Next, tree-based models were explored due to their ability to naturally capture nonlinear relationships and interaction effects.

* **Decision Tree Regression**

  * MAE: **2878.46**
  * R²: **0.84**
    Decision trees provided strong interpretability and easy visualization but they to overfit and had lower predictive accuracy.

* **Random Forest Regression**

  * MAE: **2794.46**
  * R²: **0.86**
    Random Forests improved accuracy but still fell short of an XGBoost model.

### **4. Gradient Boosting with XGBoost**

The final step was testing XGBoost as a more powerful ensemble model capable of handling complex nonlinear patterns and variable interactions.

* **XGBoost Regression**

  * MAE: **2460.46**
  * R²: **0.89**

XGBoost achieved the **lowest mean absolute error** and the **highest R² score** on the test set among all models. This indicates that the model captures the structure of hospital charges more effectively than both decision trees and Random Forests.

### **5. Final Conclusion**

While decision trees remain more interpretable and easier to visualize, **XGBoost provides the best predictive performance** by a significant margin. Its ability to model nonlinearities and interactions without explicit feature engineering makes it the strongest choice for predicting hospital charges.

**Therefore, XGBoost is selected as the final model for this project.**