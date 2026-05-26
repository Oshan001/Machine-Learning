

**Name:** Oshan <BR>
**Roll No:** 230328<BR>
**Faculty:** BCE<BR>
**Lab:** Python Programming — Data Structures & Pandas<BR>

---
# TITLE: 
Working with Dictionary and DataFrame

# OBJECTIVE
- To understand Python Dictionary operations.
- To create and manipulate Pandas DataFrames.
- To perform data selection, filtering, updating, and sorting operations.
- To learn row and column manipulation in DataFrames.
- To read and write CSV and Excel files using Pandas.
- To understand basic data manipulation techniques in Python.
---

# THEORY

#### Part I: Working with Dictionary

A **dictionary** is a data structure used to store data in key-value pairs. Each key must be unique and immutable, while values can be of any data type.

```python
student = {
    "name": "Ram",
    "age": 20,
    "faculty": "BCE"
}
```

| Operation | Syntax | Example |
|---|---|---|
| Create Dictionary | `d = {}` | `d = {"a":1, "b":2}` |
| Access Value | `d[key]` | `d["a"]` |
| Use get() | `d.get(key)` | `d.get("a")` |
| Add Item | `d[key] = value` | `d["c"] = 3` |
| Update Value | `d[key] = new_value` | `d["a"] = 10` |
| Remove using del | `del d[key]` | `del d["b"]` |
| Remove using pop() | `d.pop(key)` | `d.pop("a")` |
| Remove Last Item | `d.popitem()` | `d.popitem()` |
| Clear Dictionary | `d.clear()` | `d.clear()` |
| Copy Dictionary | `d.copy()` | `new_d = d.copy()` |
| Get All Keys | `d.keys()` | `d.keys()` |
| Get All Values | `d.values()` | `d.values()` |
| Get All Items | `d.items()` | `d.items()` |
| Check Key Exists | `key in d` | `"a" in d` |
| Get Length | `len(d)` | `len(d)` |
| Loop Through Keys | `for k in d:` | `for k in d:` |
| Loop Through Values | `for v in d.values():` | `for v in d.values():` |
| Loop Through Items | `for k,v in d.items():` | `for k,v in d.items():` |

---

#### Part II: Working with Pandas DataFrame

A **DataFrame** in Python is a two-dimensional, tabular data structure that organizes data into labeled rows and columns. It is conceptually identical to an Excel spreadsheet or a SQL table, making it the primary tool for data manipulation and analysis in the Pandas library.

| Task | Syntax |
|---|---|
| Create a DataFrame | `df = pd.DataFrame()` |
| Display first 5 rows | `df.head()` |
| Display last 5 rows | `df.tail()` |
| Total rows and columns | `df.shape` |
| Display all column names | `df.columns` |
| Complete DataFrame info | `df.info()` |
| Statistical summary | `df.describe()` |
| Select single column | `df['Name']` |
| Select multiple columns | `df[['Name','Marks']]` |
| First row (positional) | `df.iloc[0]` |
| First row (label-based) | `df.loc[0]` |
| Access specific cell | `df.loc[0,'Marks']` |
| Filter by Marks > 80 | `df[df['Marks'] > 80]` |
| Filter multiple conditions | `df[(df['Age'] > 20) & (df['Marks'] > 75)]` |
| Add new column | `df['Grade'] = ['A','B']` |
| Increase all Marks by 5 | `df['Marks'] = df['Marks'] + 5` |
| Update specific row | `df.loc[df['Name']=='Ram','Marks'] = 95` |
| Remove a column | `df.drop('Age', axis=1)` |
| Remove a row | `df.drop(0, axis=0)` |
| Sort ascending | `df.sort_values('Marks')` |
| Sort descending | `df.sort_values('Marks', ascending=False)` |
| Concatenate DataFrames | `pd.concat([df1, df2])` |
| Read CSV file | `pd.read_csv('file.csv')` |
| Write CSV file | `df.to_csv('file.csv')` |
| Read Excel file | `pd.read_excel('file.xlsx')` |
| Write Excel file | `df.to_excel('file.xlsx')` |

---

# LAB TASK 

### 1. Working with Dictionary

#### 1.1 Creating a Dictionary

A dictionary stores data as key-value pairs.

```python
student = {
    "name": "oshan",
    "roll_no": 230328,
    "age": 22,
    "facality": "BCE"
}
```

**Output:**
```
{'name': 'oshan', 'roll_no': 230328, 'age': 22, 'facality': 'BCE'}
```

<!-- ![1.1 Creating Dictionary](images/1_1_create_dict.png) -->

---

#### 1.2 Accessing Values

Using direct key access or the `.get()` method:

```python
print(student["name"])
student.get("name")
```

**Output:**
```
oshan
'oshan'
```

<!-- ![1.2 Accessing Values](images/1_2_access_value.png) -->

---

#### 1.3 Adding an Item

```python
student["phone_no"] = 97416635741
student
```

**Output:**
```
{'name': 'oshan', 'roll_no': 230328, 'age': 22, 'facality': 'BCE', 'phone_no': 97416635741}
```

<!-- ![1.3 Adding Item](images/1_3_add_item.png) -->

---

#### 1.4 Updating a Value

```python
student["roll_no"] = 28
student
```

**Output:**
```
{'name': 'oshan', 'roll_no': 28, 'age': 22, 'facality': 'BCE', 'phone_no': 97416635741}
```

<!-- ![1.4 Updating Value](images/1_4_update_value.png) -->

---

#### 1.5 Deleting a Value Using `del`

```python
del student["phone_no"]
student
```

**Output:**
```
{'name': 'oshan', 'roll_no': 28, 'age': 22, 'facality': 'BCE'}
```

<!-- ![1.5 Delete with del](images/1_5_del.png) -->

---

#### 1.6 Removing an Item Using `pop()`

```python
student.pop("facality")
student
```

**Output:**
```
'BCE'
{'name': 'oshan', 'roll_no': 28, 'age': 22}
```

<!-- ![1.6 pop()](images/1_6_pop.png) -->

---

#### 1.7 Removing Last Item Using `popitem()`

`popitem()` removes and returns the last inserted key-value pair.

```python
student.popitem()
student
```

**Output:**
```
('age', 22)
{'name': 'oshan', 'roll_no': 28}
```

<!-- ![1.7 popitem()](images/1_7_popitem.png) -->

---

#### 1.8 Copying a Dictionary

```python
copyStudent = student.copy()
copyStudent
```

**Output:**
```
{'name': 'oshan', 'roll_no': 28}
```

<!-- ![1.8 Copy Dict](images/1_8_copy.png) -->

---

#### 1.9 Getting All Keys

```python
student.keys()
```

**Output:**
```
dict_keys(['name', 'roll_no'])
```

<!-- ![1.9 Keys](images/1_9_keys.png) -->

---

#### 1.10 Getting All Values

```python
student.values()
```

**Output:**
```
dict_values(['oshan', 28])
```

<!-- ![1.10 Values](images/1_10_values.png) -->

---

#### 1.11 Clearing a Dictionary

```python
copyStudent.clear()
copyStudent
```

**Output:**
```
{}
```

<!-- ![1.11 Clear](images/1_11_clear.png) -->

---

#### 1.12 Getting All Items

```python
student.items()
```

**Output:**
```
dict_items([('name', 'oshan'), ('roll_no', 28)])
```

<!-- ![1.12 Items](images/1_12_items.png) -->

---

#### 1.13 Checking if a Key Exists & Getting Length

```python
"name" in student
len(student)
```

**Output:**
```
True
2
```

<!-- ![1.13 Key Check & Length](images/1_13_check_len.png) -->

---

#### 1.14 Looping Through Keys

```python
for k in student:
    print(k)
```

**Output:**
```
name
roll_no
```

<!-- ![1.14 Loop Keys](images/1_14_loop_keys.png) -->

---

#### 1.15 Looping Through Values

```python
for i in student.values():
    print(i)
```

**Output:**
```
oshan
28
```

<!-- ![1.15 Loop Values](images/1_15_loop_values.png) -->

---

#### 1.16 Looping Through Items

```python
for i, j in student.items():
    print(i, j)
```

**Output:**
```
name oshan
roll_no 28
```

<!-- ![1.16 Loop Items](images/1_16_loop_items.png) -->

---

### 2. Working with Pandas DataFrame

### Setup

```python
import pandas as pd
```

---

#### 2.1 Creating a DataFrame

```python
list1 = {
    "Name": ["Oshan", "Sudeep", "Sworup", "Bibek", "Alok", "Manish"],
    "Age":  [22, 20, 21, 23, 23, 22],
    "Mark": [90, 99, 85, 88, 91, 87]
}
df = pd.DataFrame(list1)
```

**Output:**

| | Name | Age | Mark |
|---|------|-----|------|
| 0 | Oshan | 22 | 90 |
| 1 | Sudeep | 20 | 99 |
| 2 | Sworup | 21 | 85 |
| 3 | Bibek | 23 | 88 |
| 4 | Alok | 23 | 91 |
| 5 | Manish | 22 | 87 |

<!-- ![2.1 Create DataFrame](images/2_1_create_df.png) -->

---

#### 2.2 Display First 5 Rows

```python
df.head()
```

**Output:**

| | Name | Age | Mark |
|---|------|-----|------|
| 0 | Oshan | 22 | 90 |
| 1 | Sudeep | 20 | 99 |
| 2 | Sworup | 21 | 85 |
| 3 | Bibek | 23 | 88 |
| 4 | Alok | 23 | 91 |

<!-- ![2.2 head()](images/2_2_head.png) -->

---

#### 2.3 Display Last 5 Rows

```python
df.tail()
```

**Output:**

| | Name | Age | Mark |
|---|------|-----|------|
| 1 | Sudeep | 20 | 99 |
| 2 | Sworup | 21 | 85 |
| 3 | Bibek | 23 | 88 |
| 4 | Alok | 23 | 91 |
| 5 | Manish | 22 | 87 |

<!-- ![2.3 tail()](images/2_3_tail.png) -->

---

#### 2.4 Find Total Rows and Columns

```python
df.shape
```

**Output:**
```
(6, 3)
```

<!-- ![2.4 shape](images/2_4_shape.png) -->

---

#### 2.5 Display All Column Names

```python
df.columns
```

**Output:**
```
Index(['Name', 'Age', 'Mark'], dtype='object')
```

<!-- ![2.5 columns](images/2_5_columns.png) -->

---

#### 2.6 Display Complete DataFrame Info

```python
df.info()
```

**Output:**
```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 6 entries, 0 to 5
Data columns (total 3 columns):
 #   Column  Non-Null Count  Dtype 
---  ------  --------------  ----- 
 0   Name    6 non-null      object
 1   Age     6 non-null      int64 
 2   Mark    6 non-null      int64 
dtypes: int64(2), object(1)
memory usage: 272.0+ bytes
```

<!-- ![2.6 info()](images/2_6_info.png) -->

---

#### 2.7 Statistical Summary of Numerical Columns

```python
df.describe()
```

**Output:**

| | Age | Mark |
|---|-----|------|
| count | 6.000000 | 6.000000 |
| mean | 21.833333 | 90.000000 |
| std | 1.169045 | 4.817997 |
| min | 20.000000 | 85.000000 |
| 25% | 21.250000 | 87.250000 |
| 50% | 22.000000 | 89.500000 |
| 75% | 22.750000 | 90.750000 |
| max | 23.000000 | 99.000000 |

<!-- ![2.7 describe()](images/2_7_describe.png) -->

---

#### 2.8 Select a Single Column

```python
df['Name']
```

**Output:**
```
0     Oshan
1    Sudeep
2    Sworup
3     Bibek
4      Alok
5    Manish
Name: Name, dtype: object
```

<!-- ![2.8 Single Column](images/2_8_single_col.png) -->

---

#### 2.9 Select Multiple Columns

```python
df[['Name', 'Mark']]
```

**Output:**

| | Name | Mark |
|---|------|------|
| 0 | Oshan | 90 |
| 1 | Sudeep | 99 |
| 2 | Sworup | 85 |
| 3 | Bibek | 88 |
| 4 | Alok | 91 |
| 5 | Manish | 87 |

<!-- ![2.9 Multiple Columns](images/2_9_multi_col.png) -->

---

#### 2.10 Display First Row Using Positional Indexing (`iloc`)

```python
df.iloc[0]
```

**Output:**
```
Name    Oshan
Age        22
Mark       90
Name: 0, dtype: object
```

<!-- ![2.10 iloc](images/2_10_iloc.png) -->

---

#### 2.11 Display First Row Using Label-Based Indexing (`loc`)

```python
df.loc[0]
```

**Output:**
```
Name    Oshan
Age        22
Mark       90
Name: 0, dtype: object
```

<!-- ![2.11 loc](images/2_11_loc.png) -->

---

#### 2.12 Access a Specific Cell Value

```python
df.loc[0, 'Mark']
```

**Output:**
```
90
```

<!-- ![2.12 Cell Value](images/2_12_cell.png) -->

---

#### 2.13 Filter Rows Where Marks > 80

```python
df[df['Mark'] > 80]
```

**Output:**

| | Name | Age | Mark |
|---|------|-----|------|
| 0 | Oshan | 22 | 90 |
| 1 | Sudeep | 20 | 99 |
| 2 | Sworup | 21 | 85 |
| 3 | Bibek | 23 | 88 |
| 4 | Alok | 23 | 91 |
| 5 | Manish | 22 | 87 |

<!-- ![2.13 Filter Mark > 80](images/2_13_filter.png) -->

---

#### 2.14 Filter with Multiple Conditions

Students with Age > 20 **and** Marks > 75:

```python
df[(df['Age'] > 20) & (df['Mark'] > 75)]
```

**Output:**

| | Name | Age | Mark |
|---|------|-----|------|
| 0 | Oshan | 22 | 90 |
| 2 | Sworup | 21 | 85 |
| 3 | Bibek | 23 | 88 |
| 4 | Alok | 23 | 91 |
| 5 | Manish | 22 | 87 |

<!-- ![2.14 Multi-condition Filter](images/2_14_multi_filter.png) -->

---

#### 2.15 Add a New Column (Grade)

```python
df['Grade'] = ['A', 'B', 'C', 'D', 'E', 'F']
df
```

**Output:**

| | Name | Age | Mark | Grade |
|---|------|-----|------|-------|
| 0 | Oshan | 22 | 90 | A |
| 1 | Sudeep | 20 | 99 | B |
| 2 | Sworup | 21 | 85 | C |
| 3 | Bibek | 23 | 88 | D |
| 4 | Alok | 23 | 91 | E |
| 5 | Manish | 22 | 87 | F |

<!-- ![2.15 Add Column](images/2_15_add_col.png) -->

---

#### 2.16 Increase All Marks by 5

```python
df['Mark'] = df['Mark'] + 5
df
```

**Output:**

| | Name | Age | Mark | Grade |
|---|------|-----|------|-------|
| 0 | Oshan | 22 | 95 | A |
| 1 | Sudeep | 20 | 104 | B |
| 2 | Sworup | 21 | 90 | C |
| 3 | Bibek | 23 | 93 | D |
| 4 | Alok | 23 | 96 | E |
| 5 | Manish | 22 | 92 | F |

<!-- ![2.16 Increase Marks](images/2_16_increase_mark.png) -->

---

#### 2.17 Update a Specific Student's Marks Using a Condition

```python
df.loc[df['Name'] == 'Oshan', 'Mark'] = 95
df
```

**Output:**

| | Name | Age | Mark | Grade |
|---|------|-----|------|-------|
| 0 | Oshan | 22 | 95 | A |
| 1 | Sudeep | 20 | 104 | B |
| 2 | Sworup | 21 | 90 | C |
| 3 | Bibek | 23 | 93 | D |
| 4 | Alok | 23 | 96 | E |
| 5 | Manish | 22 | 92 | F |

<!-- ![2.17 Update Condition](images/2_17_update_cond.png) -->

---

#### 2.18 Remove a Column

```python
df.drop('Age', axis=1)
```

**Output:**

| | Name | Mark | Grade |
|---|------|------|-------|
| 0 | Oshan | 95 | A |
| 1 | Sudeep | 104 | B |
| 2 | Sworup | 90 | C |
| 3 | Bibek | 93 | D |
| 4 | Alok | 96 | E |
| 5 | Manish | 92 | F |

<!-- ![2.18 Drop Column](images/2_18_drop_col.png) -->

---

#### 2.19 Remove the First Row

```python
df.drop(0, axis=0)
```

**Output:**

| | Name | Age | Mark | Grade |
|---|------|-----|------|-------|
| 1 | Sudeep | 20 | 104 | B |
| 2 | Sworup | 21 | 90 | C |
| 3 | Bibek | 23 | 93 | D |
| 4 | Alok | 23 | 96 | E |
| 5 | Manish | 22 | 92 | F |

<!-- ![2.19 Drop Row](images/2_19_drop_row.png) -->

---

#### 2.20 Sort DataFrame by Marks (Ascending)

```python
df.sort_values('Mark')
```

**Output:**

| | Name | Age | Mark | Grade |
|---|------|-----|------|-------|
| 2 | Sworup | 21 | 90 | C |
| 5 | Manish | 22 | 92 | F |
| 3 | Bibek | 23 | 93 | D |
| 0 | Oshan | 22 | 95 | A |
| 4 | Alok | 23 | 96 | E |
| 1 | Sudeep | 20 | 104 | B |

<!-- ![2.20 Sort Values](images/2_20_sort.png) -->

---

#### 2.21 Concatenate Two DataFrames Vertically

```python
list2 = {
    "Name": ["Ram", "Shyam", "Hari", "Sita", "Gita", "Ramesh"],
    "Age":  [21, 22, 20, 23, 21, 24],
    "Mark": [78, 85, 92, 88, 95, 80]
}
df1 = pd.DataFrame(list2)
pd.concat([df, df1])
```

**Output:**

| | Name | Age | Mark | Grade |
|---|------|-----|------|-------|
| 0 | Oshan | 22.0 | 95 | A |
| 1 | Sudeep | 20.0 | 104 | B |
| 2 | Sworup | 21.0 | 90 | C |
| 3 | Bibek | 23.0 | 93 | D |
| 4 | Alok | 23.0 | 96 | E |
| 5 | Manish | 22.0 | 92 | F |
| 0 | Ram | 21.0 | 78 | NaN |
| 1 | Shyam | 22.0 | 85 | NaN |
| 2 | Hari | 20.0 | 92 | NaN |
| 3 | Sita | 23.0 | 88 | NaN |
| 4 | Gita | 21.0 | 95 | NaN |
| 5 | Ramesh | 24.0 | 80 | NaN |

<!-- ![2.21 Concat](images/2_21_concat.png) -->

---

#### 2.22 Read Data from a CSV File

```python
pd.read_csv('StudentData1.csv')
```

**Output:**
```
DataFrame loaded from StudentData1.csv with student records.
```

<!-- ![2.22 Read CSV](images/2_22_read_csv.png) -->

---

#### 2.23 Write DataFrame to a CSV File

```python
df.to_csv('StudentData2.csv')
```

**Output:**
```
File 'StudentData2.csv' saved successfully in the working directory.
```

<!-- ![2.23 Write CSV](images/2_23_write_csv.png) -->

---

#### 2.24 Read Data from an Excel File

```python
pd.read_excel('excleStudentData2.xlsx')
```

**Output:**
```
DataFrame loaded from excleStudentData2.xlsx with student records.
```

<!-- ![2.24 Read Excel](images/2_24_read_excel.png) -->

---

#### 2.25 Write DataFrame to an Excel File

```python
df.to_excel('excleStudentData1.xlsx')
```

**Output:**
```
File 'excleStudentData1.xlsx' saved successfully in the working directory.
```

<!-- ![2.25 Write Excel](images/2_25_write_excel.png) -->

---

## CONCLUSION

In this lab, dictionary operations and Pandas DataFrame functions were successfully performed. Various data manipulation techniques including filtering, updating, sorting, concatenating, and file handling using CSV and Excel files were learned and implemented successfully.

