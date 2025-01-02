# 1. Visualizing Monthly Sales Trends with Python

This script provides a simple way to visualize monthly sales trends using **Matplotlib** and **Seaborn**. It's great for understanding sales performance over a year.

---

## Steps:
1. **Load the Dataset**: Ensure the dataset is in CSV format with `Month` and `Sales` columns.
2. **Process the Data**: Verify and sort the months in the correct order.
3. **Visualize the Trends**: Create a line chart showing monthly sales trends.

---

## Python Script

```python
# Import necessary libraries
import matplotlib.pyplot as plt
import seaborn as sns

# Load the dataset
data = pd.read_csv('sales_data.csv')

# Optional: Ensure 'Month' is in the correct order
month_order = ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 
               'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec']
data['Month'] = pd.Categorical(data['Month'], categories=month_order, ordered=True)

# Sort data by Month
data = data.sort_values('Month')

# Create the plot
plt.figure(figsize=(10, 6))
sns.lineplot(data=data, x='Month', y='Sales', marker='o', color='blue')

# Add titles and labels
plt.title('Monthly Sales Trends', fontsize=16)
plt.xlabel('Month', fontsize=12)
plt.ylabel('Sales', fontsize=12)
plt.grid(True)

# Show the plot
plt.show()
```

---
# 2. Extracting Unique Values from a CSV Column Using Python

This script demonstrates how to extract unique values from a specific column in a CSV file and save them to a new file.

---

## Python Script

```python
import pandas as pd

# Read the CSV file
df = pd.read_csv('your_file.csv')

# Extract unique values from the column and save to a new CSV
df['ColumnName'].drop_duplicates().to_csv('unique_values.csv', index=False, header=True)

print("Unique values saved to 'unique_values.csv'")

