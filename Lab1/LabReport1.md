                           Lab Done by :
                           Name: Oshan Bajracharya
                           Roll No : 230328
# Title : Python Lists and Matrices
## Objective
To learn and implement basic Python operations on:
1. Lists
2. Sorting and reversing lists
3. Matrices and matrix multiplication
---

# Theory
## List
A list is a collection data type in Python used to store multiple elements in a single variable. Lists are ordered, changeable, and allow duplicate values.

### Features of List
- Ordered collection
- Mutable (can be modified)
- Allows duplicate values
- Supports different data types

### Example
```python
my_list = [10, 20, 30, 40]
```

---

## Matrix
A matrix is a collection of rows and columns arranged in tabular form. In Python, matrices can be created using nested lists.

### Example
```python
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]
```

### Matrix Operations
- Accessing elements
- Printing diagonal elements
- Matrix multiplication
- Addition and subtraction
---

# Task 1
* Create a list with 5 elements 
* Print the first and last element.

## Program

```python
# Create list with 5 elements
my_list = [10, 20, 30, 40, 50]

# Print first element
print("First element:", my_list[0])

# Print last element
print("Last element:", my_list[-1])
```

## Output

```python
First element: 10
Last element: 50
```


---

# Task 2
*  Create a list of integer values
*  Add two elements 
*  Remove two elements, sort the list in ascending order
*  Reverse the list.

## Program

```python
# Create list of integers
numbers = [12, 5, 8, 20, 15]

print("Original List:", numbers)

# Add two elements
numbers.append(25)
numbers.append(30)

print("After Adding Elements:", numbers)

# Remove two elements
numbers.remove(5)
numbers.remove(20)

print("After Removing Elements:", numbers)

# Sort list in ascending order
numbers.sort()

print("Ascending Order:", numbers)

# Reverse the list
numbers.reverse()

print("Reversed List:", numbers)
```

## Output

```python
Original List: [12, 5, 8, 20, 15]
After Adding Elements: [12, 5, 8, 20, 15, 25, 30]
After Removing Elements: [12, 8, 15, 25, 30]
Ascending Order: [8, 12, 15, 25, 30]
Reversed List: [30, 25, 15, 12, 8]
```
---
# Most Used List Functions

| Function | Use |
|----------|-----|
| `append()` | Add element to list |
| `remove()` | Remove element from list |
| `insert()` | Insert element at position |
| `pop()` | Delete element using index |
| `sort()` | Sort list in ascending order |
| `reverse()` | Reverse list order |
| `len()` | Find length of list |
| `count()` | Count repeated elements |
| `index()` | Find index position |
| `copy()` | Copy a list |


---

# Task 3

## Aim
Create a 3×3 matrix, print diagonal elements, and multiply two matrices.

## Program

```python
# Create first 3x3 matrix
matrix1 = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

# Create second 3x3 matrix
matrix2 = [
    [9, 8, 7],
    [6, 5, 4],
    [3, 2, 1]
]

# Print diagonal elements of matrix1
print("Diagonal Elements:")
for i in range(3):
    print(matrix1[i][i])

# Multiply two matrices
result = [
    [0, 0, 0],
    [0, 0, 0],
    [0, 0, 0]
]

for i in range(3):
    for j in range(3):
        for k in range(3):
            result[i][j] += matrix1[i][k] * matrix2[k][j]

print("Matrix Multiplication Result:")
for row in result:
    print(row)
```

## Output

```python
Diagonal Elements:
1
5
9

Matrix Multiplication Result:
[30, 24, 18]
[84, 69, 54]
[138, 114, 90]
```


---


# Conclusion

In this lab, we learned how to create and manipulate lists in Python. We also learned how to sort and reverse lists. Additionally, we created matrices and performed matrix multiplication operations successfully.

                                       
