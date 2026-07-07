**Name:** Oshan <BR>
**Roll No:** 230328<BR>
**Faculty:** BCE<BR>
**Lab:** Python Programming — Logistic Regression, SVC, and SVR<BR>

---

# TITLE:
Logistic Regression, Support Vector Classification (SVC), and Support Vector Regression (SVR)

# OBJECTIVE
- To implement and evaluate a Logistic Regression model for binary classification using the Breast Cancer dataset.
- To train and compare Support Vector Classification (SVC) models with Linear and RBF kernels using the Iris dataset.
- To apply Support Vector Regression (SVR) with different kernels for predicting continuous values using the California Housing dataset.
- To understand the effect of hyperparameters such as C (regularization) and ε (epsilon) on model performance.
- To evaluate classification models using Accuracy, Precision, Recall, F1-Score, and Confusion Matrix.
- To evaluate regression models using MAE, MSE, RMSE, and R² Score.

---

# THEORY

#### Part I: Logistic Regression

**Logistic Regression** is a supervised linear classification algorithm used for binary and multi-class classification problems. It estimates the probability of a class using the **sigmoid (logistic) function**:

$$\sigma(z) = \frac{1}{1 + e^{-z}}$$

Where `z = wX + b` (linear combination of features and weights).

**Key Concepts:**

| Concept | Description |
|---------|-------------|
| Sigmoid Function | Maps any real value to a probability between 0 and 1 |
| Decision Boundary | Threshold (default 0.5) for assigning class labels |
| Coefficients | Weights learned by the model for each feature |
| Positive Coefficient | Feature pushes prediction toward class 1 |
| Negative Coefficient | Feature pushes prediction toward class 0 |

---

#### Part II: Support Vector Machine (SVM)

**Support Vector Machine (SVM)** is a powerful supervised learning algorithm that finds the optimal **hyperplane** which maximizes the margin between two classes.

**Key Terms:**

| Term | Description |
|------|-------------|
| Hyperplane | Decision boundary that separates classes |
| Support Vectors | Data points closest to the hyperplane |
| Margin | Distance between the hyperplane and support vectors |
| Kernel | Function that transforms data into higher dimensions |
| C (Regularization) | Controls trade-off between margin size and misclassification |

**Kernel Types:**

| Kernel | Use Case |
|--------|----------|
| Linear | Linearly separable data |
| RBF (Radial Basis Function) | Non-linearly separable data |
| Polynomial | Complex polynomial boundaries |

---

#### Part III: Support Vector Regression (SVR)

**SVR** extends SVM to regression tasks. Instead of predicting a class, it predicts a **continuous value** while allowing predictions within an ε-tube (epsilon-insensitive zone) without penalty.

**Key Parameters:**

| Parameter | Description |
|-----------|-------------|
| ε (Epsilon) | Width of the insensitive tube around predictions |
| C | Penalizes points outside the ε-tube |
| Kernel | Same kernel options as SVC |

---

#### Part IV: Evaluation Metrics

**Classification Metrics:**

| Metric | Formula | Description |
|--------|---------|-------------|
| Accuracy | TP+TN / Total | Overall correct predictions |
| Precision | TP / (TP+FP) | Correctness of positive predictions |
| Recall | TP / (TP+FN) | Coverage of actual positives |
| F1-Score | 2 × (P×R)/(P+R) | Harmonic mean of Precision and Recall |

**Regression Metrics:**

| Metric | Description |
|--------|-------------|
| MAE | Mean Absolute Error — average magnitude of errors |
| MSE | Mean Squared Error — penalizes large errors more |
| RMSE | Root Mean Squared Error — same unit as target variable |
| R² Score | Proportion of variance explained by the model |

---

#### Part V: Common Functions Used

| Task | Syntax |
|------|--------|
| Load Breast Cancer Dataset | `load_breast_cancer()` |
| Load Iris Dataset | `load_iris()` |
| Load California Housing | `fetch_california_housing()` |
| Train-Test Split | `train_test_split(X, y, test_size=0.2)` |
| Feature Scaling | `StandardScaler().fit_transform(X_train)` |
| Logistic Regression | `LogisticRegression().fit(X_train, y_train)` |
| SVM Classifier | `SVC(kernel='linear').fit(X_train, y_train)` |
| SVM Regressor | `SVR(kernel='rbf').fit(X_train, y_train)` |
| Predictions | `model.predict(X_test)` |
| Accuracy | `accuracy_score(y_test, y_pred)` |
| Confusion Matrix | `confusion_matrix(y_test, y_pred)` |
| Classification Report | `classification_report(y_test, y_pred)` |
| MAE | `mean_absolute_error(y_test, y_pred)` |
| MSE | `mean_squared_error(y_test, y_pred)` |
| R² Score | `r2_score(y_test, y_pred)` |
| View Coefficients | `model.coef_` |

---

# LAB TASK

---

## Part A: Logistic Regression

**Dataset:** Breast Cancer Dataset (Scikit-learn)

---

#### Task 1: Load the Dataset

```python
import pandas as pd
from pandas.core.frame import DataFrame
from sklearn.datasets import load_breast_cancer

data = load_breast_cancer()

df = DataFrame(data.data, columns=data.feature_names)

X = data.data
Y = data.target
```

---

#### Task 2: Explore the Dataset

```python
# Display the shape of X and Y
print(X.shape, Y.shape)

# Print the first five rows
print(df.head())

# Identify number of samples, features, and classes
print("Number of samples:", X.shape[0])
print("Number of features:", X.shape[1])
print("Number of classes:", len(data.target_names))
```

---

#### Task 3: Split the Dataset

```python
from sklearn.datasets import load_breast_cancer
from sklearn.model_selection import train_test_split

data = load_breast_cancer()
X = data.data
Y = data.target

# Split dataset: 80% training, 20% testing
X_train, X_test, Y_train, Y_test = train_test_split(
    X, Y,
    test_size=0.2,
    random_state=42
)

print("Training features shape:", X_train.shape)
print("Testing features shape:", X_test.shape)
print("Training labels shape:", Y_train.shape)
print("Testing labels shape:", Y_test.shape)
```

---

#### Task 4: Standardize Features

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()

X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled  = scaler.transform(X_test)

print("Scaled Training Features Shape:", X_train_scaled.shape)
print("Scaled Testing Features Shape:", X_test_scaled.shape)
```

---

#### Task 5: Train Logistic Regression Model

```python
from sklearn.linear_model import LogisticRegression

model = LogisticRegression()
model.fit(X_train_scaled, Y_train)

print("Logistic Regression model trained successfully!")
```

---

#### Task 6: Make Predictions

```python
Y_pred = model.predict(X_test_scaled)

print("Predicted labels:", Y_pred[:10])
print("Actual labels:   ", Y_test[:10])
```

---

#### Task 7: Evaluate the Model

```python
from sklearn.metrics import (
    accuracy_score,
    precision_score,
    recall_score,
    f1_score,
    confusion_matrix
)

accuracy  = accuracy_score(Y_test, Y_pred)
precision = precision_score(Y_test, Y_pred)
recall    = recall_score(Y_test, Y_pred)
f1        = f1_score(Y_test, Y_pred)
cm        = confusion_matrix(Y_test, Y_pred)

print("Accuracy :", accuracy)
print("Precision:", precision)
print("Recall   :", recall)
print("F1-Score :", f1)
print("\nConfusion Matrix:")
print(cm)
```

---

#### Task 8: Interpret Coefficients

```python
import numpy as np

# Display all coefficients
for feature, coef in zip(data.feature_names, model.coef_[0]):
    print(f"{feature}: {coef}")

# Largest positive coefficient
max_idx = np.argmax(model.coef_[0])
print("\n1. Largest positive coefficient:")
print(data.feature_names[max_idx], model.coef_[0][max_idx])

# Largest negative coefficient
min_idx = np.argmin(model.coef_[0])
print("\n2. Largest negative coefficient:")
print(data.feature_names[min_idx], model.coef_[0][min_idx])

print("\n3. Sign of coefficient:")
print("Positive (+): Feature increases likelihood of class 1 (Benign)")
print("Negative (-): Feature increases likelihood of class 0 (Malignant)")
```

**Answers:**

| Question | Answer |
|----------|--------|
| Largest positive coefficient | `compactness error` (0.6825) |
| Largest negative coefficient | `worst texture` (−1.3506) |
| Sign of a coefficient | A positive coefficient increases the probability of predicting class 1 (Benign), while a negative coefficient increases the probability of predicting class 0 (Malignant) |

---

## Part B: Support Vector Classification (SVC)

**Dataset:** Iris Dataset (Scikit-learn)

---

#### Task 1: Load the Dataset

```python
from sklearn.datasets import load_iris

data = load_iris()

X = data.data
Y = data.target

print("Dataset loaded successfully!")
```

---

#### Task 2: Exploratory Analysis

```python
print("Number of classes:", len(data.target_names))
print("Number of features:", len(data.feature_names))
print("Class labels:", data.target_names)
```

---

#### Task 3: Train-Test Split

```python
from sklearn.model_selection import train_test_split

# Split dataset into 70% training and 30% testing
X_train, X_test, Y_train, Y_test = train_test_split(
    X, Y,
    test_size=0.3,
    random_state=42
)

print("Training set shape:", X_train.shape)
print("Testing set shape:", X_test.shape)
```

---

#### Task 4: Standardize Features

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()

X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled  = scaler.transform(X_test)

print("Standardization completed successfully")
```

---

#### Task 5: Train Linear SVM

```python
from sklearn.svm import SVC

svc_linear = SVC(kernel='linear')
svc_linear.fit(X_train_scaled, Y_train)

print("Model trained successfully!")
```

---

#### Task 6: Evaluate the Linear SVM

```python
from sklearn.metrics import accuracy_score, confusion_matrix, classification_report

Y_pred = svc_linear.predict(X_test_scaled)

accuracy = accuracy_score(Y_test, Y_pred)
print("Accuracy:", accuracy)

cm = confusion_matrix(Y_test, Y_pred)
print("\nConfusion Matrix:\n", cm)

print("\nClassification Report:\n")
print(classification_report(Y_test, Y_pred))
```

---

#### Task 7: Train RBF Kernel SVM

```python
from sklearn.svm import SVC
from sklearn.metrics import accuracy_score, confusion_matrix, classification_report

svc_rbf = SVC(kernel='rbf')
svc_rbf.fit(X_train_scaled, Y_train)

Y_pred_rbf = svc_rbf.predict(X_test_scaled)

accuracy = accuracy_score(Y_test, Y_pred_rbf)
print("Accuracy:", accuracy)

cm = confusion_matrix(Y_test, Y_pred_rbf)
print("\nConfusion Matrix:\n", cm)

print("\nClassification Report:\n")
print(classification_report(Y_test, Y_pred_rbf))
```

---

#### Task 8: Compare Kernels

```python
import pandas as pd
from sklearn.metrics import accuracy_score

acc_linear = accuracy_score(Y_test, svc_linear.predict(X_test_scaled))
acc_rbf    = accuracy_score(Y_test, svc_rbf.predict(X_test_scaled))

comparison_table = pd.DataFrame({
    "Kernel":   ["Linear", "RBF"],
    "Accuracy": [acc_linear, acc_rbf]
})

print(comparison_table)
```

**Result:**

| Kernel | Accuracy |
|--------|----------|
| Linear | 0.9778 |
| RBF | 1.0000 |

---

#### Task 9: Hyperparameter Tuning

```python
from sklearn.svm import SVC
from sklearn.metrics import accuracy_score
import pandas as pd

C_values = [0.1, 1, 10, 100]
results   = []

for C in C_values:
    model = SVC(kernel='linear', C=C)
    model.fit(X_train_scaled, Y_train)
    Y_pred = model.predict(X_test_scaled)
    acc    = accuracy_score(Y_test, Y_pred)
    results.append([C, acc])

df_results = pd.DataFrame(results, columns=["C", "Accuracy"])
print(df_results)
```

**Result:**

| C | Accuracy |
|---|----------|
| 0.1 | 1.0000 |
| 1 | 0.9778 |
| 10 | 0.9778 |
| 100 | 1.0000 |

---

## Part C: Support Vector Regression (SVR)

**Dataset:** California Housing Dataset (Scikit-learn)

---

#### Task 1: Load Dataset

```python
from sklearn.datasets import fetch_california_housing

data = fetch_california_housing()

print("Number of observations:", data.data.shape[0])
print("Number of features:", data.data.shape[1])
print("\nTarget variable description:")
print(data.DESCR)
```

---

#### Task 2: Split Dataset

```python
from sklearn.model_selection import train_test_split
from sklearn.datasets import fetch_california_housing

data = fetch_california_housing()

X = data.data
Y = data.target

X_train, X_test, Y_train, Y_test = train_test_split(
    X, Y,
    test_size=0.2,
    random_state=42
)

print("Training set shape:", X_train.shape)
print("Testing set shape:", X_test.shape)
```

---

#### Task 3: Standardize Features

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()

X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled  = scaler.transform(X_test)

print("Feature scaling completed successfully")
```

---

#### Task 4: Train Linear SVR

```python
from sklearn.svm import SVR

svr_linear = SVR(kernel='linear')
svr_linear.fit(X_train_scaled, Y_train)

print("Linear SVR model trained successfully")
```

---

#### Task 5: Predict House Prices

```python
Y_pred = svr_linear.predict(X_test_scaled)

print("Predictions generated successfully")
print("First 10 predictions:", Y_pred[:10])
```

---

#### Task 6: Evaluate Model

```python
from sklearn.metrics import mean_absolute_error, mean_squared_error, r2_score
import numpy as np

mae  = mean_absolute_error(Y_test, Y_pred)
mse  = mean_squared_error(Y_test, Y_pred)
rmse = np.sqrt(mse)
r2   = r2_score(Y_test, Y_pred)

print("Mean Absolute Error (MAE):", mae)
print("Mean Squared Error (MSE):", mse)
print("Root Mean Squared Error (RMSE):", rmse)
print("R² Score:", r2)
```

---

#### Task 7: Train RBF SVR

```python
from sklearn.svm import SVR
from sklearn.metrics import mean_absolute_error, mean_squared_error, r2_score
import numpy as np

svr_rbf = SVR(kernel='rbf')
svr_rbf.fit(X_train_scaled, Y_train)

Y_pred_rbf = svr_rbf.predict(X_test_scaled)

mae  = mean_absolute_error(Y_test, Y_pred_rbf)
mse  = mean_squared_error(Y_test, Y_pred_rbf)
rmse = np.sqrt(mse)
r2   = r2_score(Y_test, Y_pred_rbf)

print("RBF SVR Results:")
print("MAE:", mae)
print("MSE:", mse)
print("RMSE:", rmse)
print("R² Score:", r2)
```

---

#### Task 8: Compare Results

```python
import pandas as pd
import numpy as np
from sklearn.metrics import mean_absolute_error, mean_squared_error, r2_score

mae_linear  = mean_absolute_error(Y_test, Y_pred)
rmse_linear = np.sqrt(mean_squared_error(Y_test, Y_pred))
r2_linear   = r2_score(Y_test, Y_pred)

mae_rbf  = mean_absolute_error(Y_test, Y_pred_rbf)
rmse_rbf = np.sqrt(mean_squared_error(Y_test, Y_pred_rbf))
r2_rbf   = r2_score(Y_test, Y_pred_rbf)

results = pd.DataFrame({
    "MODEL": ["Linear SVR", "RBF SVR"],
    "MAE":   [mae_linear, mae_rbf],
    "RMSE":  [rmse_linear, rmse_rbf],
    "R2":    [r2_linear, r2_rbf]
})

print(results)
```

**Result:**

| Model | MAE | RMSE | R² |
|-------|-----|------|----|
| Linear SVR | 0.5120 | 0.7611 | 0.5580 |
| RBF SVR | 0.3986 | 0.5975 | 0.7276 |

---

#### Task 9: Effect of ε (Epsilon)

```python
from sklearn.svm import SVR
from sklearn.metrics import mean_absolute_error
import pandas as pd

eps_values = [0.01, 0.1, 0.5, 1]
results    = []

for eps in eps_values:
    model = SVR(kernel='rbf', epsilon=eps)
    model.fit(X_train_scaled, Y_train)
    Y_pred = model.predict(X_test_scaled)
    mae    = mean_absolute_error(Y_test, Y_pred)
    results.append([eps, mae])

df_results = pd.DataFrame(results, columns=["ε (epsilon)", "MAE"])
print(df_results)
```

**Result:**

| ε (Epsilon) | MAE |
|-------------|-----|
| 0.01 | 0.3982 |
| 0.10 | 0.3986 |
| 0.50 | 0.4214 |
| 1.00 | 0.5337 |

---

## One-Page Summary: Comparing Logistic Regression, SVC, and SVR

### 1. Logistic Regression

Logistic Regression is a linear classification algorithm that predicts the probability of a class using the sigmoid function. It is primarily used for **binary classification** tasks.

| Property | Detail |
|----------|--------|
| Type | Linear Classifier |
| Output | Discrete class labels (0 or 1) |
| Key Parameter | Regularization strength C |
| Strength | Simple, fast, and interpretable |
| Limitation | Poor performance on non-linear data |

---

### 2. Support Vector Classification (SVC)

SVC is a classification algorithm that finds the optimal hyperplane maximizing the margin between classes. It supports kernel functions to handle non-linear decision boundaries.

| Property | Detail |
|----------|--------|
| Type | Classification Model |
| Output | Class labels |
| Key Parameters | C (regularization), kernel type, gamma |
| Strength | High accuracy, effective in high-dimensional spaces |
| Limitation | Computationally expensive on large datasets |

---

### 3. Support Vector Regression (SVR)

SVR is the regression extension of SVM. It predicts continuous values while tolerating errors within an ε-tube using an epsilon-insensitive loss function.

| Property | Detail |
|----------|--------|
| Type | Regression Model |
| Output | Continuous numerical values |
| Key Parameters | C, ε (epsilon), kernel type |
| Strength | Robust to outliers, flexible with kernel selection |
| Limitation | Sensitive to hyperparameter tuning, slow on large data |

---

### Overall Comparison

| Model | Task Type | Output | Best Use Case | Weakness |
|-------|-----------|--------|---------------|----------|
| Logistic Regression | Classification | Class labels | Binary classification, linearly separable data | Cannot model non-linear boundaries |
| SVC | Classification | Class labels | Complex multi-class problems with kernel flexibility | High computational cost |
| SVR | Regression | Continuous values | Regression with outlier robustness | Requires careful hyperparameter tuning |

---

## CONCLUSION

In this lab, three supervised machine learning algorithms were implemented using Scikit-learn. Logistic Regression was applied to the Breast Cancer dataset and achieved an accuracy of **97.37%**, demonstrating its effectiveness for binary classification with linearly separable data. The `compactness error` feature had the largest positive coefficient while `worst texture` had the largest negative coefficient, reflecting their opposing influence on tumor classification. Support Vector Classification was applied to the Iris dataset, where the **RBF kernel achieved 100% accuracy** compared to 97.78% for the Linear kernel, showing the advantage of non-linear kernels for this dataset. Hyperparameter tuning with C values showed that both C=0.1 and C=100 yielded perfect accuracy. Support Vector Regression was applied to the California Housing dataset, where **RBF SVR outperformed Linear SVR** across all metrics (MAE: 0.3986 vs 0.5120, R²: 0.7276 vs 0.5580). The epsilon experiment confirmed that smaller ε values produce lower MAE, while larger ε values allow more error tolerance, resulting in degraded predictions. Overall, kernel-based methods (RBF) consistently outperformed linear approaches for both classification and regression tasks in this lab.
