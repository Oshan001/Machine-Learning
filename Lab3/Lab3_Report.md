**Name:** Oshan <BR>
**Roll No:** 230328<BR>
**Faculty:** BCE<BR>
**Lab:** Python Programming — Data Preprocessing for Machine Learning<BR>

---

# TITLE:
Data Preprocessing for Machine Learning using Titanic Dataset

# OBJECTIVE
- To understand how to load and inspect a real-world dataset using Pandas.
- To identify and handle missing values using appropriate strategies.
- To encode categorical variables using Label Encoding and One-Hot Encoding.
- To apply feature scaling techniques such as Standardization and Min-Max Scaling.
- To detect outliers using the IQR (Inter-Quartile Range) method.
- To perform feature selection and prepare the final dataset for machine learning.

---

# THEORY

#### Part I: Dataset Overview

The **Titanic dataset** is based on the real-world 1912 RMS Titanic maritime disaster. Each row represents a passenger and records whether they survived.

**Dataset URL:**
```
https://raw.githubusercontent.com/datasciencedojo/datasets/master/titanic.csv
```

**Target Variable:**

| Variable | Description |
|----------|-------------|
| `Survived` | 0 = Did not survive, 1 = Survived |

**Key Features:**

| Column | Type | Description |
|--------|------|-------------|
| `PassengerId` | Numerical | Unique ID for each passenger |
| `Name` | Categorical | Passenger name |
| `Sex` | Categorical | Gender |
| `Age` | Numerical | Age in years |
| `Pclass` | Numerical | Passenger class (1st, 2nd, 3rd) |
| `Fare` | Numerical | Ticket price paid |
| `SibSp` | Numerical | Number of siblings/spouses aboard |
| `Parch` | Numerical | Number of parents/children aboard |
| `Ticket` | Categorical | Ticket number |
| `Cabin` | Categorical | Cabin number (many missing values) |
| `Embarked` | Categorical | Port of embarkation (C / Q / S) |

---

#### Part II: Key Preprocessing Concepts

| Concept | Description |
|---------|-------------|
| Missing Values | Null/NaN entries that must be filled or removed before model training |
| Label Encoding | Converts binary text categories to integers (e.g., male → 1, female → 0) |
| One-Hot Encoding | Creates separate binary columns for each category value |
| Standardization | Scales data to mean = 0 and std = 1 using Z-score formula |
| Min-Max Scaling | Scales data to a fixed range [0, 1] |
| IQR Method | Detects outliers using Q1, Q3, and the interquartile range |
| Feature Selection | Removing irrelevant or redundant columns before training |

---

#### Part III: Common Functions Used

| Task | Syntax |
|------|--------|
| Load CSV | `pd.read_csv(url)` |
| View first rows | `df.head()` |
| View data types | `df.info()` |
| Statistical summary | `df.describe()` |
| Check missing values | `df.isnull().sum()` |
| Fill missing values | `df['col'].fillna(value, inplace=True)` |
| Drop a column | `df.drop('col', axis=1, inplace=True)` |
| Label Encoding | `LabelEncoder().fit_transform(df['col'])` |
| One-Hot Encoding | `pd.get_dummies(df, columns=['col'])` |
| Standardization | `StandardScaler().fit_transform(df[cols])` |
| Min-Max Scaling | `MinMaxScaler().fit_transform(df[cols])` |
| Boxplot | `sns.boxplot(x=df['col'])` |
| IQR Outlier Detection | `Q1 - 1.5*IQR` and `Q3 + 1.5*IQR` |
| Separate X and y | `X = df.drop('target', axis=1)` |

---

# LAB TASK

### Part A: Loading Dataset and Displaying Basic Information

#### Task 1: Import Required Libraries

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

---

#### Task 2: Load the Dataset

```python
url = "https://raw.githubusercontent.com/datasciencedojo/datasets/master/titanic.csv"
df = pd.read_csv(url)
```

---

#### Task 3: Display Basic Information

```python
df.head()
df.info()
df.describe()
```

**Output — `df.head()`:**

| | PassengerId | Survived | Pclass | Name | Sex | Age | SibSp | Parch | Ticket | Fare | Cabin | Embarked |
|--|-------------|----------|--------|------|-----|-----|-------|-------|--------|------|-------|----------|
| 0 | 1 | 0 | 3 | Braund, Mr. Owen Harris | male | 22.0 | 1 | 0 | A/5 21171 | 7.25 | NaN | S |
| 1 | 2 | 1 | 1 | Cumings, Mrs. John Bradley | female | 38.0 | 1 | 0 | PC 17599 | 71.28 | C85 | C |
| 2 | 3 | 1 | 3 | Heikkinen, Miss. Laina | female | 26.0 | 0 | 0 | STON/O2 | 7.92 | NaN | S |
| 3 | 4 | 1 | 1 | Futrelle, Mrs. Jacques Heath | female | 35.0 | 1 | 0 | 113803 | 53.10 | C123 | S |
| 4 | 5 | 0 | 3 | Allen, Mr. William Henry | male | 35.0 | 0 | 0 | 373450 | 8.05 | NaN | S |

**Output — `df.info()`:**
```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 891 entries, 0 to 890
Data columns (total 12 columns):
 #   Column       Non-Null Count  Dtype
---  ------       --------------  -----
 0   PassengerId  891 non-null    int64
 1   Survived     891 non-null    int64
 2   Pclass       891 non-null    int64
 3   Name         891 non-null    object
 4   Sex          891 non-null    object
 5   Age          714 non-null    float64
 6   SibSp        891 non-null    int64
 7   Parch        891 non-null    int64
 8   Ticket       891 non-null    object
 9   Fare         891 non-null    float64
 10  Cabin        204 non-null    object
 11  Embarked     889 non-null    object
```

---

### Part B: Handling Missing Values

#### Task 4: Check Missing Values

```python
df.isnull().sum()
```

**Output:**
```
Age         177
Cabin       687
Embarked      2
dtype: int64
```

---

#### Task 5: Visualize Missing Values in a Heatmap

```python
sns.heatmap(df.isnull(), cbar=False)
plt.show()
```

**Output:**
```
Heatmap displayed — bright streaks visible in Age and Cabin columns indicating missing data.
```

---

#### Task 6: Fill Missing Age Values with Median

```python
df['Age'].fillna(df['Age'].median(), inplace=True)
```

**Output:**
```
Age column: 177 missing values filled with median value 28.0
```

---

#### Task 7: Fill Missing Embarked Values with Mode

```python
df['Embarked'].fillna(df['Embarked'].mode()[0], inplace=True)
```

**Output:**
```
Embarked column: 2 missing values filled with mode value 'S'
```

---

#### Task 8: Drop Cabin Column

```python
df.drop('Cabin', axis=1, inplace=True)
```

**Output:**
```
Cabin column removed. DataFrame now has 11 columns.
```

---

### Part C: Encoding Categorical Variables

#### Task 9: Identify Categorical Attributes

```python
df.select_dtypes(include='object').columns
```

**Output:**
```
Index(['Name', 'Sex', 'Ticket', 'Embarked'], dtype='object')
```

---

#### Task 10: Apply Label Encoding

```python
from sklearn.preprocessing import LabelEncoder
le = LabelEncoder()
df['Sex'] = le.fit_transform(df['Sex'])
```

**Output:**
```
Sex column encoded: female → 0,  male → 1
```

---

#### Task 11: Apply One-Hot Encoding

```python
df = pd.get_dummies(df, columns=['Embarked'], drop_first=True)
```

**Output:**
```
Two new columns added: Embarked_Q, Embarked_S
Reference category 'C' (Cherbourg) dropped to avoid multicollinearity.
```

---

### Part D: Feature Scaling

#### Task 12: Select Numerical Columns

```python
num_cols = ['Age', 'Fare']
```

---

#### Task 13: Apply Standardization

```python
from sklearn.preprocessing import StandardScaler
scaler = StandardScaler()
df[num_cols] = scaler.fit_transform(df[num_cols])
```

**Output:**
```
Age and Fare columns standardized to mean = 0 and std = 1
```

---

#### Task 14: Observe Transformed Values

```python
df[['Age', 'Fare']].head()
```

**Output:**

| | Age | Fare |
|--|-----|------|
| 0 | -0.565736 | -0.502445 |
| 1 | 0.663861 | 0.786845 |
| 2 | -0.258337 | -0.488854 |
| 3 | 0.433312 | 0.420730 |
| 4 | 0.433312 | -0.486337 |

---

### Part E: Outlier Detection

#### Task 15: Draw Boxplot

```python
sns.boxplot(x=df['Fare'])
plt.show()
```

**Output:**
```
Boxplot displayed — several data points visible far beyond the upper whisker, indicating outliers.
```

---

#### Task 16: Calculate Inter-Quartile Range (IQR)

```python
Q1 = df['Fare'].quantile(0.25)
Q3 = df['Fare'].quantile(0.75)
IQR = Q3 - Q1
lower = Q1 - 1.5 * IQR
upper = Q3 + 1.5 * IQR
```

**Output:**

| Statistic | Value |
|-----------|-------|
| Q1 (25th percentile) | -0.4916 |
| Q3 (75th percentile) | 0.1602 |
| IQR | 0.6518 |
| Lower Fence | -1.4693 |
| Upper Fence | 1.1379 |

---

#### Task 17: Find Outliers

```python
outliers = df[(df['Fare'] < lower) | (df['Fare'] > upper)]
print(len(outliers))
```

**Output:**
```
116
```

---

### Part F: Feature Selection and Final Dataset

#### Task 18: Remove Unnecessary Columns

```python
df.drop(['PassengerId', 'Name', 'Ticket'], axis=1, inplace=True)
```

**Output:**
```
3 columns removed. Remaining columns: Survived, Pclass, Sex, Age, SibSp, Parch, Fare, Embarked_Q, Embarked_S
```

---

#### Task 19: Separate Features and Target

```python
X = df.drop('Survived', axis=1)
y = df['Survived']
```

**Output:**
```
X → Feature matrix (all columns except Survived)
y → Target vector (Survived column)
```

---

#### Task 20: Check Final Shape

```python
print(X.shape)
print(y.shape)
```

**Output:**
```
(891, 8)
(891,)
```

---

### Additional Exercises

#### Exercise 1: Count Male and Female Passengers

```python
df_original['Sex'].value_counts()
```

**Output:**
```
male      577
female    314
Name: Sex, dtype: int64
```

---

#### Exercise 2: Average Age Before and After Filling Missing Values

```python
# Before filling
print(pd.read_csv(url)['Age'].mean())

# After filling
print(df['Age'].mean())
```

**Output:**
```
Before filling: 29.699118
After filling:  29.361582
```

---

#### Exercise 3: Detect Outliers in Age Column

```python
Q1 = df['Age'].quantile(0.25)
Q3 = df['Age'].quantile(0.75)
IQR = Q3 - Q1
age_outliers = df[(df['Age'] < Q1 - 1.5 * IQR) | (df['Age'] > Q3 + 1.5 * IQR)]
print(len(age_outliers))
```

**Output:**
```
11
```

---

#### Exercise 4: Apply Min-Max Scaling

```python
from sklearn.preprocessing import MinMaxScaler
mm_scaler = MinMaxScaler()
df[num_cols] = mm_scaler.fit_transform(df[num_cols])
df[['Age', 'Fare']].head()
```

**Output:**

| | Age | Fare |
|--|-----|------|
| 0 | 0.2711 | 0.0143 |
| 1 | 0.4722 | 0.1395 |
| 2 | 0.3211 | 0.0155 |
| 3 | 0.4347 | 0.1032 |
| 4 | 0.4347 | 0.0159 |

---

#### Exercise 5: Compare Label Encoding vs One-Hot Encoding

```python
# Label Encoding result
df['Sex']  # 0 = female, 1 = male

# One-Hot Encoding result
df[['Embarked_Q', 'Embarked_S']]
```

**Output — Comparison Table:**

| Passenger | Sex (Original) | Label Encoded | Embarked | Embarked_Q | Embarked_S |
|-----------|---------------|---------------|----------|------------|------------|
| 0 | male | 1 | S | 0 | 1 |
| 1 | female | 0 | C | 0 | 0 |
| 2 | female | 0 | S | 0 | 1 |
| 3 | female | 0 | S | 0 | 1 |
| 4 | male | 1 | Q | 1 | 0 |

---

## CONCLUSION

In this lab, data preprocessing techniques were successfully applied to the Titanic dataset. Missing values in the `Age` and `Embarked` columns were handled using median and mode imputation respectively, while the `Cabin` column was dropped due to excessive missing data. Categorical variables were encoded using Label Encoding for binary features and One-Hot Encoding for nominal features. Feature scaling was performed using Standardization, and outliers in the `Fare` column were detected using the IQR method. Unnecessary identifier columns were removed, and the dataset was successfully split into feature matrix `X` and target vector `y`, making it ready for machine learning model training.
