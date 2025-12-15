### 1\. The Weapon: The `ndarray`

Lists are slow. NumPy arrays are fast. In Machine Learning, you will process millions of rows. You cannot afford "slow."

**The Basics:**

```python
import numpy as np

# 1D Array (Vector)
vector = np.array([1, 2, 3])

# 2D Array (Matrix)
matrix = np.array([[1, 2, 3], 
                   [4, 5, 6]])

# Check the dimensions (Vital for debugging shape errors later)
print(matrix.shape)  # Output: (2, 3) -> 2 Rows, 3 Columns
```

### 2\. Surgical Extraction: Indexing & Slicing

You need to be able to slice data like a surgeon.

  * **Syntax:** `[start:stop:step]`
  * **Rule:** The `stop` index is *exclusive* (it doesn't include that number).

**Type this:**

```python
# Create a 3x3 matrix of numbers 0-8
arr = np.arange(9).reshape(3, 3)
print("Original Matrix:\n", arr)

# 1. Grab the last row
print("Last Row:", arr[-1])

# 2. Grab the first two columns of ALL rows
# Syntax: [rows, columns]
print("First 2 cols:\n", arr[:, 0:2]) 

# 3. Boolean Indexing (CRITICAL for Data Cleaning)
# This is how you filter data without 'for' loops.
mask = arr > 4
print("Elements > 4:", arr[mask]) 
# Returns a 1D array of elements that meet the condition
```

### 3\. The Heavy Lifter: Broadcasting

This is the concept that fails most juniors in interviews.
**Broadcasting** allows NumPy to perform arithmetic operations on arrays of *different shapes*.

**How it works:**
If you try to add a `(3, 3)` matrix and a `(3,)` vector, NumPy automatically "stretches" (broadcasts) the vector to match the matrix so the math works.

**Type this:**

```python
A = np.array([[1, 1, 1],
              [1, 1, 1],
              [1, 1, 1]]) # Shape (3, 3)

B = np.array([0, 1, 2])   # Shape (3,)

# The Magic: B is "broadcast" across every row of A
C = A + B 

print("Result of Broadcasting:\n", C)
# Output will be:
# [[1, 2, 3],
#  [1, 2, 3],
#  [1, 2, 3]]
```

*Why this matters:* When you normalize data later (subtracting the mean from every row), you are using broadcasting. [cite_start]If you don't understand this, you cannot clean the dataset tonight[cite: 23].

-----

### 🚨 Task:

1.  Generate a random 5x5 matrix with integers between 1 and 100.
2.  Extract the sub-matrix of the middle 3x3 elements.
3.  Replace all values greater than 50 with 0.

**👇👇👇**

```python
import numpy as np

# 1. Generate Data
data = np.random.randint(1, 101, size=(5, 5))
print("Original:\n", data)

# 2. Extract Middle 3x3
# Rows: index 1 to 4 (exclusive), Cols: index 1 to 4 (exclusive)
middle = data[1:4, 1:4]
print("Middle 3x3:\n", middle)

# 3. Filter (The "Kill" Switch)
data[data > 50] = 0
print("Filtered Matrix:\n", data)
```

### Task 2:
The "Normalizer" (Standardization):

In Machine Learning, your data will have different scales (e.g., Age: 0-100, Salary: 10000-100000). You must scale them to a standard range (Mean = 0, Std Dev = 1) or your model will crash.

The Drill:

Create a (5, 3) matrix representing 5 samples with 3 features each (Random integers 1-100).Calculate the mean and standard deviation of each column (feature).Subtract the mean from each element and divide by the standard deviation. (This is the formula:  Z=X−μσ )Hint: Use axis=0 for column-wise operations.

**👇👇👇**

```python

import numpy as np
X = np.random.randint(1, 100, (5,3))
print(X)

mean = X.mean(axis=0)
std = X.std(axis=0)
print(mean)
print(std)
```
