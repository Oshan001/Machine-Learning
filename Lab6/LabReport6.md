
## Linear Regression and Regularization

### Student Information
- **Name:** Oshan Bajracharya
- **Roll No:** 230328
---

# Objective

The objective of this lab is to implement **Linear Regression** on the California Housing dataset, evaluate its performance using common regression metrics, and compare it with **Ridge Regression** and **Lasso Regression** after feature standardization.

---

# Dataset

The **California Housing Dataset** from `sklearn.datasets` was used.

The dataset contains housing information collected from California districts, including:

- Median Income
- House Age
- Average Rooms
- Average Bedrooms
- Population
- Average Occupancy
- Latitude
- Longitude

**Target Variable**

- Median House Value (`MedHouseVal`)

---

# Tools and Libraries

- Python
- NumPy
- Pandas
- Matplotlib
- Scikit-learn

---

# Methodology

The following steps were performed during the lab:

1. Imported required libraries.
2. Loaded the California Housing dataset.
3. Explored the dataset.
4. Checked dataset information and statistics.
5. Checked for missing values.
6. Split features and target variable.
7. Performed Train-Test Split (80% training, 20% testing).
8. Standardized features using `StandardScaler`.
9. Trained a Linear Regression model.
10. Predicted house prices on the testing data.
11. Evaluated the model using:
    - MAE
    - MSE
    - RMSE
    - R² Score
12. Trained Ridge Regression (`alpha = 1.0`).
13. Trained Lasso Regression (`alpha = 0.1`).
14. Compared all three regression models graphically.

---

# Code

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

from sklearn.datasets import fetch_california_housing
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LinearRegression, Ridge, Lasso
from sklearn.metrics import mean_absolute_error, mean_squared_error, r2_score

# Load Dataset
housing = fetch_california_housing(as_frame=True)
df = housing.frame

# Explore Dataset
print(df.head())
print(df.info())
print(df.describe())
print(df.isnull().sum())

# Split Features and Target
X = df.drop("MedHouseVal", axis=1)
y = df["MedHouseVal"]

# Train-Test Split
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

# Feature Scaling
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)

# Linear Regression
linear_model = LinearRegression()
linear_model.fit(X_train_scaled, y_train)

linear_pred = linear_model.predict(X_test_scaled)

# Evaluation
mae = mean_absolute_error(y_test, linear_pred)
mse = mean_squared_error(y_test, linear_pred)
rmse = np.sqrt(mse)
r2 = r2_score(y_test, linear_pred)

print("MAE :", mae)
print("MSE :", mse)
print("RMSE:", rmse)
print("R2 Score:", r2)

# Ridge Regression
ridge = Ridge(alpha=1.0)
ridge.fit(X_train_scaled, y_train)
ridge_pred = ridge.predict(X_test_scaled)

# Lasso Regression
lasso = Lasso(alpha=0.1)
lasso.fit(X_train_scaled, y_train)
lasso_pred = lasso.predict(X_test_scaled)
```

---

# Performance Metrics

The following evaluation metrics were used:

### Mean Absolute Error (MAE)

Measures the average absolute difference between actual and predicted values.

### Mean Squared Error (MSE)

Measures the average squared error.

### Root Mean Squared Error (RMSE)

Square root of MSE. Lower values indicate better performance.

### R² Score

Measures how well the regression model explains the variance in the target variable.

---

# Graph 1: Actual vs Predicted

```python
plt.figure(figsize=(8,6))
plt.scatter(y_test, linear_pred, color="blue", alpha=0.5)

plt.plot(
    [y_test.min(), y_test.max()],
    [y_test.min(), y_test.max()],
    color="red",
    linewidth=2
)

plt.xlabel("Actual House Price")
plt.ylabel("Predicted House Price")
plt.title("Actual vs Predicted House Prices")
plt.grid(True)

plt.show()
```

---

# Graph 2: Residual Plot

```python
residuals = y_test - linear_pred

plt.figure(figsize=(8,6))
plt.scatter(linear_pred, residuals, color="green", alpha=0.5)

plt.axhline(y=0, color="red", linestyle="--")

plt.xlabel("Predicted House Price")
plt.ylabel("Residuals")
plt.title("Residual Plot")

plt.grid(True)

plt.show()
```

---

# Graph 3: Comparison of Linear, Ridge and Lasso

```python
plt.figure(figsize=(8,6))

plt.scatter(y_test, linear_pred, alpha=0.5, label="Linear")
plt.scatter(y_test, ridge_pred, alpha=0.5, label="Ridge")
plt.scatter(y_test, lasso_pred, alpha=0.5, label="Lasso")

plt.plot(
    [y_test.min(), y_test.max()],
    [y_test.min(), y_test.max()],
    "r--"
)

plt.xlabel("Actual House Price")
plt.ylabel("Predicted House Price")
plt.title("Comparison of Regression Models")

plt.legend()
plt.grid(True)

plt.show()
```

---

# Observations

- The California Housing dataset contains no missing values.
- Feature scaling improves the stability of regression models.
- Linear Regression provides a strong baseline for prediction.
- Ridge Regression helps reduce overfitting by applying L2 regularization.
- Lasso Regression performs feature selection by shrinking less important coefficients toward zero.
- The Actual vs Predicted plot shows that predictions closely follow the ideal prediction line.
- The Residual Plot indicates that residuals are distributed around zero, suggesting a reasonably good model fit.

---

# Conclusion

In this lab, Linear Regression was successfully implemented on the California Housing dataset. The model was evaluated using MAE, MSE, RMSE, and R² score. Ridge and Lasso Regression were also implemented to study the effects of regularization. The comparison showed that regularization can improve model generalization while reducing the impact of overfitting. Overall, all three regression models produced satisfactory predictions, with Ridge and Lasso providing additional robustness through regularization.

---

# References

1. Scikit-learn Documentation
2. California Housing Dataset
3. Machine Learning Lab Manual