import pandas as pd
import numpy as np

# Sample DataFrames for Combining and Merging
sales_data_1 = pd.DataFrame({'OrderID': [1, 2, 3, 4], 'Product': ['Laptop', 'Tablet', 'Smartphone', 'Headphones'], 'Sales': [1200, 800, 1500, 300]})
sales_data_2 = pd.DataFrame({'OrderID': [3, 4, 5, 6], 'Product': ['Smartphone', 'Headphones', 'Smartwatch', 'Tablet'], 'Sales': [1500, 300, 200, 900]})

# Merging and Concatenation
merged_data = pd.merge(sales_data_1, sales_data_2, on='OrderID', how='inner', suffixes=('_1', '_2'))
combined_data = pd.concat([sales_data_1, sales_data_2], ignore_index=True)

print("Merged Data:\n", merged_data)
print("\nCombined Data:\n", combined_data)

# Reshaping with Melt
reshaping_data = pd.DataFrame({'Month': ['Jan', 'Feb', 'Mar'], 'Product_A': [100, 150, 130], 'Product_B': [90, 80, 120]})
melted_data = reshaping_data.melt(id_vars='Month', var_name='Product', value_name='Sales')
print("\nMelted Data:\n", melted_data)

# Pivoting
pivot_data = pd.DataFrame({'Month': ['Jan', 'Jan', 'Feb', 'Feb', 'Mar', 'Mar'], 'Product': ['Product_A', 'Product_B']*3, 'Sales': [100, 90, 150, 80, 130, 120]})
pivoted_data = pivot_data.pivot(index='Month', columns='Product', values='Sales')
print("\nPivoted Data:\n", pivoted_data)

# Handling Missing Data
pivoted_data.loc['Feb', 'Product_A'] = np.nan
pivoted_data.loc['Mar', 'Product_B'] = np.nan
filled_data = pivoted_data.fillna(pivoted_data.mean())
print("\nFilled Data:\n", filled_data)

# Summary Statistics
print("\nSummary Statistics:\n", filled_data.describe())

the output should be
Merged Data:
    OrderID   Product_1  Sales_1   Product_2  Sales_2
0        3  Smartphone     1500  Smartphone     1500
1        4  Headphones      300  Headphones      300

Combined Data:
    OrderID     Product  Sales
0        1      Laptop   1200
1        2      Tablet    800
2        3  Smartphone   1500
3        4  Headphones    300
4        3  Smartphone   1500
5        4  Headphones    300
6        5  Smartwatch    200
7        6      Tablet    900

Melted Data:
   Month    Product  Sales
0   Jan  Product_A    100
1   Feb  Product_A    150
2   Mar  Product_A    130
3   Jan  Product_B     90
4   Feb  Product_B     80
5   Mar  Product_B    120

Pivoted Data:
 Product  Product_A  Product_B
Month
Feb            150         80
Jan            100         90
Mar            130        120

Filled Data:
 Product  Product_A  Product_B
Month
Feb          115.0       80.0
Jan          100.0       90.0
Mar          130.0       85.0

Summary Statistics:
 Product  Product_A  Product_B
count          3.0        3.0
mean         115.0       85.0
std           15.0        5.0
min          100.0       80.0
25%          107.5       82.5
50%          115.0       85.0
75%          122.5       87.5
max          130.0       90.0
