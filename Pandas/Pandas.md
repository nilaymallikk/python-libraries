### 1\. The DataFrame: Your New Spreadsheet

A DataFrame is just a table, but programmable.

```python
import pandas as pd
import numpy as np

# Creating a mock e-commerce dataset
# We use a dictionary to create a DataFrame
data = {
    'Product': ['Laptop', 'Mouse', 'Monitor', 'Laptop', 'Mouse', 'Monitor'],
    'Category': ['Electronics', 'Accessories', 'Electronics', 'Electronics', 'Accessories', 'Electronics'],
    'Price': [1000, 50, 300, 1200, 45, 400],
    'Quantity': [1, 5, 2, 1, 10, 3],
    'City': ['Mumbai', 'Delhi', 'Mumbai', 'Bangalore', 'Mumbai', 'Delhi']
}

# df = pd.read_csv("your_file.csv") # Only when data is available in Local
df = pd.DataFrame(data) # For this practice

print("--- The Data ---")
print(df.head()) # Shows first 5 rows
print("\n--- The Structure ---")
print(df.info()) # Crucial: Shows data types and missing values
```
```print(df.head()) ```

What it does: It prints only the first 5 rows.

Why? Real datasets have 1,000,000 rows. If you just type print(df), your terminal will explode with text and you won't be able to read anything. head() is a quick "sanity check" to see if the data loaded correctly.

```print(df.info())```

What it does: This is the Doctor's Checkup for your data. It does not show you the rows. It shows you the health of the columns.

Output explanation:

Non-Null Count: Tells you if data is missing. If you have 1000 rows, but "Age" says "800 non-null", you know 200 people are missing their age.

Dtype (Data Type): Crucial. If your "Price" column is listed as object (text) instead of int64 (number), you cannot do math on it. You need to know this immediately to fix it.

### 2\. GroupBy: The "Pivot Table" Killer

This is the most important command in Pandas. You use it to answer questions like: "What is the total revenue per City?" or "Average price per Category?"

**The Logic:** Split the data $\to$ Apply a function (sum, mean, count) $\to$ Combine it back.

**Type this:**

```python
# 1. Total Revenue per City
# First, we need a Revenue column
df['Revenue'] = df['Price'] * df['Quantity']

# Group by City and Sum the Revenue
city_revenue = df.groupby('City')['Revenue'].sum()
print("\n--- Revenue by City ---")
print(city_revenue)

# 2. Average Price per Category
# Group by Category and find Mean of Price
avg_price = df.groupby('Category')['Price'].mean()
print("\n--- Avg Price by Category ---")
print(avg_price)
Count = df.groupby('Category')['Price'].count()
print(Count)
```

You want to know exactly what math is happening "under the hood." Here is the step-by-step breakdown using the data we defined.

The Vector Multiplication
`df['Revenue'] = df['Price'] * df['Quantity']`

This is **element-wise multiplication**. Pandas takes the vector (column) of Price and the vector of Quantity and multiplies them row-by-row to create a new vector: Revenue.

**The Math:**
$$Revenue_i = Price_i \times Quantity_i$$

**The Data Calculation:**
* **Row 0 (Mumbai):** $1000 \times 1 = \mathbf{1000}$
* **Row 1 (Delhi):** $50 \times 5 = \mathbf{250}$
* **Row 2 (Mumbai):** $300 \times 2 = \mathbf{600}$
* **Row 3 (Bangalore):** $1200 \times 1 = \mathbf{1200}$
* **Row 4 (Mumbai):** $45 \times 10 = \mathbf{450}$
* **Row 5 (Delhi):** $400 \times 3 = \mathbf{1200}$

---

GroupBy Sum (City Revenue)
`df.groupby('City')['Revenue'].sum()`

This operation splits the data into buckets based on the "City" label, then adds up the "Revenue" numbers in each bucket.

**The Math:**
$$TotalRevenue_{City} = \sum (\text{Revenue of all rows belonging to that City})$$

**The Data Calculation:**

* **Bucket: Mumbai**
    * Includes Row 0 ($1000$), Row 2 ($600$), Row 4 ($450$)
    * Math: $1000 + 600 + 450 = \mathbf{2050}$

* **Bucket: Delhi**
    * Includes Row 1 ($250$), Row 5 ($1200$)
    * Math: $250 + 1200 = \mathbf{1450}$

* **Bucket: Bangalore**
    * Includes Row 3 ($1200$)
    * Math: $\mathbf{1200}$

---

GroupBy Mean (Average Price per Category)
`df.groupby('Category')['Price'].mean()`

This splits the data by "Category" and calculates the **arithmetic mean** (average) of the "Price" column for each bucket.

**The Math:**
$$AveragePrice_{Category} = \frac{\sum (\text{Prices in Category})}{\text{Count of items in Category}}$$

**The Data Calculation:**

* **Bucket: Electronics**
    * Includes: Laptop ($1000$), Monitor ($300$), Laptop ($1200$), Monitor ($400$)
    * Sum: $1000 + 300 + 1200 + 400 = 2900$
    * Count: 4 items
    * Math: $2900 / 4 = \mathbf{725.0}$

* **Bucket: Accessories**
    * Includes: Mouse ($50$), Mouse ($45$)
    * Sum: $50 + 45 = 95$
    * Count: 2 items
    * Math: $95 / 2 = \mathbf{47.5}$



**This is why the output looks the way it does. Does this mathematical breakdown help clarify the code logic?**

### 3\. Merging: The "VLOOKUP" Killer

In the real world, data is never in one table. You have a "Customers" table and a "Orders" table. You need to join them.

**Type this:**

```python
# Create two separate tables
customers = pd.DataFrame({
    'CustomerID': [101, 102, 103],
    'Name': ['Rahul', 'Anjali', 'Rohan']
})

orders = pd.DataFrame({
    'OrderID': [1, 2, 3, 4],
    'CustomerID': [101, 102, 101, 104], # Note 104 is not in customers
    'Amount': [500, 700, 200, 900]
})

# MERGE (Inner Join)
# Only keeps records where CustomerID exists in BOTH tables
# 104 will be dropped because we don't know the customer name
merged_df = pd.merge(orders, customers, on='CustomerID', how='inner')

print("\n--- Merged Data (Orders + Customer Names) ---")
print(merged_df)
```

*Note: If you wanted to keep Order 104 even without a name, you would use `how='left'`.*

### 4\. Pivot Tables: Summary Views

Sometimes `groupby` returns a format that is hard to read. `pivot_table` makes it human-readable.

**Type this:**

```python
# Let's pivot the original df
# We want to see Total Revenue: Rows = City, Columns = Category

pivot = df.pivot_table(
    values='Revenue', 
    index='City', 
    columns='Category', 
    aggfunc='sum',
    fill_value=0 # Replace NaN with 0 if no sales occurred
)

print("\n--- Pivot Table ---")
print(pivot)
```

-----

### 🚨 Task:


1.  Using the `df` created above.
2.  Filter the data to show only sales in 'Mumbai'.
3.  Calculate the total number of items sold (`Quantity`) in Mumbai.
4.  Sort the original dataframe by `Revenue` in descending order (highest revenue top).

**Code Solution (Type it out):**

```python
# 1. Filter for Mumbai
mumbai_sales = df[df['City'] == 'Mumbai']
print("\n--- Mumbai Data ---")
print(mumbai_sales)

# 2. Total Items in Mumbai
total_items = mumbai_sales['Quantity'].sum()
print(f"Total items sold in Mumbai: {total_items}")

# 3. Sorting
sorted_df = df.sort_values(by='Revenue', ascending=False)
print("\n--- Top Sales ---")
print(sorted_df)
```
