
# 1. List vs Tuple

**Interviewer:** Can you explain what Python lists and tuples are, and how they differ?

**Candidate:** Sure! Lists and tuples are both used to store collections of items in Python, but they have key differences.

A **list** is **mutable**, meaning its elements can be changed after creation. It consumes more memory and is slower when iterating compared to a tuple, but it's great for operations like inserting and deleting items. Lists also offer a variety of built-in methods for manipulation.

For example:
```python
a_list = ["Data", "Camp", "Tutorial"]
a_list.append("Session")
print(a_list)  # Output: ['Data', 'Camp', 'Tutorial', 'Session']
```

A **tuple**, on the other hand, is **immutable**, so once it’s created, its elements can't be changed. It uses less memory and is faster when iterating over compared to lists, but it doesn’t have as many built-in methods. 

For example:
```python
a_tuple = ("Data", "Camp", "Tutorial")
print(a_tuple)  # Output: ('Data', 'Camp', 'Tutorial')
```

In summary, if you need a collection of items that will change, go with a list. If the data won’t change, a tuple is more efficient.

----------

# 2. __init__()


**Interviewer:** Can you explain the __init__() method in Python?

**Candidate:** The `__init__()` method is a special method in Python, commonly known as a constructor in object-oriented programming (OOP). It’s automatically called when a new object is created from a class, and it’s used to initialize the object’s state.

The main purpose of `__init__()` is to assign values to an object’s properties or perform any setup tasks that are necessary when an object is created.

For example, in the following code, we define a class `book_shop`, which has an `__init__()` method that initializes the `title` of the book. The `book()` method prints the title of the book.

```python
class book_shop:
    # constructor
    def __init__(self, title):
        self.title = title

    # Sample method
    def book(self):
        print('The title of the book is', self.title)

# Creating an object 'b' and initializing with 'Sandman'
b = book_shop('Sandman')
b.book()  # Output: The title of the book is Sandman
```

In this case, when we create the object `b` and pass the title 'Sandman', the `__init__()` method assigns this value to `self.title`, and then the `book()` method prints it. The constructor helps in setting up the object with necessary data at the time of creation.


------
# 3. list, dictionary, and tuple comprehension


**Interviewer:** Can you explain list, dictionary, and tuple comprehension with examples?

**Candidate:** Sure! Comprehensions are concise ways to create lists, dictionaries, or tuples using a single line of code, often making them more readable and efficient.

### **List Comprehension**
List comprehensions are used to create new lists by iterating over an iterable and optionally applying a condition or transformation.

Example:
```python
my_list = [i for i in range(1, 10)]
my_list
# [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### **Dictionary Comprehension**
Dictionary comprehensions are used to create dictionaries by specifying key-value pairs in a compact way.

Example:
```python
# Creating a dictionary using dictionary comprehension
my_dict = {i: i**2 for i in range(1, 10)}

# Output the dictionary
my_dict

{1: 1, 2: 4, 3: 9, 4: 16, 5: 25, 6: 36, 7: 49, 8: 64, 9: 81}
```

### **Tuple Comprehension**
Tuple comprehensions are similar to list comprehensions but use parentheses. However, they generate a generator object instead of a tuple directly, which is more memory efficient.

Example:
```python
# Create a generator for squares of numbers from 1 to 5
squares_gen = (x**2 for x in range(1, 6))
print(tuple(squares_gen))  # Output: (1, 4, 9, 16, 25)
```

### Summary:
- **List Comprehension:** Creates a list.
- **Dictionary Comprehension:** Creates a dictionary.
- **Tuple Comprehension:** Creates a generator object; converting it to a tuple requires explicitly calling `tuple()`.

----------

# 4. 

**Interviewer:** What is a KeyError in Python, and how can you handle it?

**Candidate:** A **KeyError** occurs in Python when you try to access a key that doesn’t exist in a dictionary. For example:

```python
scores = {"Alice": 90, "Bob": 85}
print(scores["Charlie"])  # Raises KeyError: 'Charlie'
```

This happens because Python expects the key to exist, and if it doesn’t, it raises the error.

### **Ways to Handle a KeyError**

1. **Use the `.get()` Method:**
   The `.get()` method returns `None` or a default value if the key isn’t found, instead of raising an error.
   ```python
   print(scores.get("Charlie", "Key not found"))  # Output: Key not found
   ```

2. **Use a `try-except` Block:**
   You can catch the `KeyError` and handle it gracefully.
   ```python
   try:
       print(scores["Charlie"])
   except KeyError:
       print("Key not found")
   ```

3. **Check for the Key Using `in`:**
   Before accessing a key, you can check if it exists in the dictionary.
   ```python
   if "Charlie" in scores:
       print(scores["Charlie"])
   else:
       print("Key not found")
   ```

### **Best Practice:**
Choose the method based on your use case:
- Use `.get()` when you want to provide a default value.
- Use `try-except` for robust error handling.
- Use `in` when you need to explicitly check for key existence before proceeding.
- --------


# 5. Python handle memory management

**Interviewer:** How does Python handle memory management, and what role does garbage collection play?

**Candidate:** Python takes care of memory management automatically. All objects are stored in a private heap, and Python’s memory manager handles the allocation and deallocation of memory so we don’t have to do it manually.

Garbage collection plays an important role here. It cleans up objects that are no longer needed to free up memory. Python uses reference counting to track how many references an object has. If the reference count drops to zero, the object gets deleted. 

For example, if you create a list and then delete all references to it, Python automatically clears it from memory.

Python also has a cyclic garbage collector to deal with situations where objects reference each other in a cycle. You can even control garbage collection using the `gc` module, like manually triggering it with `gc.collect()`.

So, memory management in Python is mostly hands-off, but we have tools to intervene if needed.


# 6. Shallow copy and Deep copy

**Interviewer:** Can you explain the difference between a shallow copy and a deep copy in Python, and when you would use each?

**Candidate:** Sure! The main difference lies in how they handle nested structures like lists within lists.

- **Shallow Copy:** A shallow copy creates a new object, but the nested objects inside it are still references to the same memory locations as the original. So, changes to the nested objects in one copy will affect the other.

  Example:
  ```python
  import copy

  original = [[1, 2, 3], [4, 5, 6]]
  shallow = copy.copy(original)

  shallow[0][0] = 99
  print(original)  # Output: [[99, 2, 3], [4, 5, 6]]
  ```

- **Deep Copy:** A deep copy creates a completely independent copy of the original object, including all nested objects. Changes in one copy do not affect the other.

  Example:
  ```python
  import copy

  original = [[1, 2, 3], [4, 5, 6]]
  deep = copy.deepcopy(original)

  deep[0][0] = 99
  print(original)  # Output: [[1, 2, 3], [4, 5, 6]]
  ```

### **When to Use Each:**
- Use a **shallow copy** when:
  - The object contains only immutable items, like numbers or strings.
  - You want changes in nested objects to reflect in both the original and the copy.

- Use a **deep copy** when:
  - You’re dealing with complex, nested structures.
  - You want the copy to be entirely independent of the original.

In short, choose shallow copy for efficiency when shared references are okay, and deep copy when you need complete separation between the copies.

-------
# 7. Range & XRange

**Interviewer:** What is the difference between `range` and `xrange`?

**Candidate:** The difference between `range` and `xrange` is relevant only in Python 2. 

- In **Python 2**, `range()` creates a list of numbers in memory, which can use a lot of memory if the range is large. On the other hand, `xrange()` generates the numbers one at a time as you iterate over it, making it more memory-efficient because it doesn’t store the entire range in memory.

  Example in Python 2:
  ```python
  r = range(1, 1000)  # Creates a list of 999 numbers
  xr = xrange(1, 1000)  # Creates an iterator
  ```

- In **Python 3**, `xrange()` has been removed, and `range()` behaves like `xrange` from Python 2. It acts as a generator-like object, producing numbers on demand rather than creating a full list.

So, if you're using Python 3, there's no `xrange`, and `range()` is both memory-efficient and easy to use.
-----

# 8. 

**Interviewer:** What is pickling and unpickling in Python?

**Candidate:** Pickling and unpickling are processes used to serialize and deserialize Python objects.

- **Pickling:** This is the process of converting a Python object (like a list, dictionary, or even a custom object) into a byte stream, which can be stored in a file or transferred over a network. It essentially "freezes" the state of an object.

- **Unpickling:** This is the reverse process, where the byte stream is converted back into a Python object. It "unfreezes" the object, restoring its original state.

### Example:
```python
import pickle

# Pickling
data = {"name": "Alice", "age": 25, "city": "New York"}
with open("data.pkl", "wb") as file:
    pickle.dump(data, file)

# Unpickling
with open("data.pkl", "rb") as file:
    loaded_data = pickle.load(file)

print(loaded_data)  # Output: {'name': 'Alice', 'age': 25, 'city': 'New York'}
```

### When to Use:
Pickling is commonly used for:
- Saving program state to a file.
- Sending data between Python programs over a network.

You can use the `pickle` module for most use cases, or `dill` for more advanced serialization needs (like handling functions or lambdas).

------

# 9. 

**Interviewer:** What is the use of the `pass` keyword in Python?

**Candidate:** The `pass` keyword is a null statement in Python that does nothing. It’s often used as a placeholder where the code requires a statement syntactically, but no action needs to be performed at that point.

For example, if you’re defining a function or class but haven’t written the implementation yet, you can use `pass` to avoid syntax errors:

```python
def my_function():
    pass  # Placeholder for future code

class MyClass:
    pass  # Placeholder for class definition
```

It’s useful during development when you want to leave parts of your code unfinished while keeping the structure intact.



---------
**Interviewer:** What is a lambda function in Python?

**Candidate:** A lambda function in Python is a small, anonymous function defined using the `lambda` keyword. Unlike regular functions, it doesn’t have a name and is limited to a single line of expression.

### Key Points:
- It can take multiple arguments but has only one expression.
- It’s often used for short, simple operations like filtering, mapping, or sorting.

### Example:
Here’s a comparison of a normal function and a lambda function that both double a number:

**Normal Function:**
```python
def double(x):
    return x + x

print(double(5))  # Output: 10
```

**Lambda Function:**
```python
double = lambda x: x + x
print(double(5))  # Output: 10
```

### When to Use:
Lambda functions are useful for quick, throwaway functions, especially when used with functions like `map()`, `filter()`, or `sorted()`.

**Example with `map`:**
```python
nums = [1, 2, 3, 4]
doubled = list(map(lambda x: x * 2, nums))
print(doubled)  # Output: [2, 4, 6, 8]
```

-----





**Interviewer:** What is a compound datatype?

**Candidate:** A compound datatype is a single variable that can store multiple values, making it useful for organizing related data. In Python, the most common compound datatypes are:

1. **Lists**: 
   - A collection of values where order matters.
   - Elements can be modified (mutable).
   - Example:
     ```python
     my_list = [1, 2, 3, 4]
     ```

2. **Tuples**: 
   - A sequence of values where order matters.
   - Immutable, meaning elements cannot be changed after creation.
   - Example:
     ```python
     my_tuple = (1, 2, 3, 4)
     ```

3. **Sets**: 
   - A collection of unique values where order doesn’t matter.
   - Used to check membership or remove duplicates.
   - Example:
     ```python
     my_set = {1, 2, 3, 4}
     ```

### Use Case:
Compound datatypes are great for handling structured or grouped data, like managing a list of names, a set of unique IDs, or a tuple of coordinates.

-



# 10. 


**Interviewer:** What is the use of the `continue` keyword in Python?

**Candidate:** The `continue` keyword is used inside loops to skip the rest of the current iteration and move directly to the next one. It’s useful when you want to bypass certain parts of the loop for specific conditions without stopping the entire loop.

### Example:
```python
for num in range(1, 6):
    if num == 3:
        continue  # Skip the iteration when num is 3
    print(num)
```

**Output:**
```
1
2
4
5
```

Here, the number `3` is skipped because `continue` causes the loop to immediately move to the next iteration. It’s handy for filtering data or skipping unnecessary operations.



-----------






# 11. 

**Interviewer:** What is the use of the `try` and `except` block in Python?

**Candidate:** The `try` and `except` blocks in Python are used for **exception handling**. Exceptions are errors that occur during program execution, and these blocks help us manage them gracefully without crashing the program.

- The **`try` block** contains code that might raise an exception.
- The **`except` block** defines how to handle the exception if it occurs.

This way, you can prevent your program from stopping abruptly and provide meaningful feedback or alternative behavior.

### Example:
```python
try:
    num = int(input("Enter a number: "))
    print(10 / num)
except ZeroDivisionError:
    print("You cannot divide by zero!")
except ValueError:
    print("Invalid input! Please enter a number.")
```

### How It Works:
- If the user enters `0`, a `ZeroDivisionError` is caught, and the message "You cannot divide by zero!" is displayed.
- If the user enters something non-numeric, a `ValueError` is caught, and the message "Invalid input!" is shown.

### Use Case:
`try-except` blocks are great for handling unexpected errors, making your program more robust and user-friendly.




---------------






# 12.

What is Pandas, and how is it used in data analysis?
A3. Pandas is a Python library used for data manipulation and analysis. It provides data structures like DataFrame and Series, which allow for easy handling and analysis of tabular data

--------------



What is NumPy, and why is it used in data analysis?
A5. NumPy is a Python library used for numerical computing. It provides support for large, multi-dimensional arrays and matrices, along with a collection of mathematical functions to operate on these arrays efficiently.


----------

How do you create a NumPy array?
A6. You can create a NumPy array using the np.array() function by passing a Python list as an argument.

np.array([1,2,3,4,5])


-----


**Interviewer:** Can you explain the difference between a DataFrame and a Series in Pandas?

**Candidate:** Sure! A **Series** is like a single column of data, one-dimensional with a labeled index. You can think of it as a list with labels attached.

A **DataFrame**, on the other hand, is two-dimensional. It’s like a table with rows and columns, where each column is essentially a Series. A DataFrame can hold different types of data in each column, like numbers in one column and text in another.

For example:
- A **Series** might look like this:
  ```python
  0    10
  1    20
  2    30
  dtype: int64
  ```

- A **DataFrame** is more like:
  ```python
      Name  Age
  0  Alice   25
  1    Bob   30
  ```

If you’re working with single-dimensional data, you’d use a Series, but for anything tabular, a DataFrame is the way to go.

---------



**Interviewer:** How do you select specific rows and columns from a DataFrame in Pandas?

**Candidate:** You can select specific rows and columns using **indexing** and **slicing** in Pandas. There are several ways to do it:

1. **Selecting Columns:**  
   You can use the column name directly or a list of column names:
   ```python
   df["column_name"]  # Select one column
   df[["col1", "col2"]]  # Select multiple columns
   ```

2. **Selecting Rows:**  
   Use `.loc` for label-based indexing or `.iloc` for position-based indexing:
   ```python
   df.loc[0]  # Select row by index label
   df.iloc[0]  # Select row by position
   ```

3. **Selecting Specific Rows and Columns Together:**  
   Combine `.loc` or `.iloc` for rows and columns:
   ```python
   df.loc[1:3, ["col1", "col2"]]  # Rows 1 to 3, specific columns
   df.iloc[1:3, 0:2]  # Rows 1 to 3, first two columns
   ```

### Example:
```python
import pandas as pd

data = {"Name": ["Alice", "Bob", "Charlie"], "Age": [25, 30, 35], "City": ["NY", "LA", "SF"]}
df = pd.DataFrame(data)

# Select the 'Name' column
print(df["Name"])

# Select rows 0 and 1, and columns 'Name' and 'Age'
print(df.loc[0:1, ["Name", "Age"]])
```

This approach is very flexible and helps you work with the specific data you need.




-----
How do you create a line plot using Matplotlib?
A10. You can create a line plot using the plt.plot() function in Matplotlib
----

Q12. How do you check for missing values in a DataFrame using Pandas?
A12. You can use the isnull() method in Pandas to check for missing values in a DataFrame. For example:
-------
Q13. What are some common methods for handling missing values in a DataFrame?
A13. Common methods for handling missing values include removing rows or columns containing missing values (dropna()), filling missing values with a specified value (fillna()), or interpolating missing values based on existing data (interpolate()).
----

Q14. How do you calculate descriptive statistics for a DataFrame in Pandas?
A14. You can use the describe() method in Pandas to calculate descriptive statistics for a DataFrame, including count, mean, standard deviation, minimum, maximum, and percentiles.
---

Q25. How do you filter data in a DataFrame using Pandas?
A25. You can filter data in a DataFrame using boolean indexing in Pandas. 
```
 For example, to filter rows where the 'Score' is greater than 90:
filtered_df = df[df['score']>90]
```
Q24. What is the purpose of data filtering in data analysis?
A24.  to extract subsets of data that meet specified criteria or conditions. It is used to focus on relevant portions of the data for further analysis or visualization
-----

**Interviewer:** What is the purpose of data aggregation in data analysis?

**Candidate:** Data aggregation is used to summarize and condense large datasets into meaningful insights. It involves grouping data based on specific criteria, like categories or time periods, and then calculating summary statistics like sums, averages, or counts for each group.

### Why it’s useful:
- It makes large datasets easier to interpret.
- It highlights overall patterns and trends.
- It’s essential for generating summary reports or dashboards.

---

Q21. How do you perform data normalization using scikit-learn?
A21. You can perform data normalization using the MinMaxScaler, StandardScaler, or RobustScaler classes in scikit -learn. For example:

      from sklearn.preprocessing import MinMaxScaler
      scaler = MinMaxScaler()
      scaled_data = scaler.fit_transform(data)

--------
What is a histogram, and how is it used in data analysis?
A15. A histogram is a graphical representation of the distribution of numerical data. It consists of a series of bars, where each bar represents a range of values and the height of the bar represents the frequency of values within that range. Histograms are commonly used to visualize the frequency distribution of a dataset.
-----

**Interviewer:** What is the difference between `loc` and `iloc` in Pandas?

**Candidate:** The main difference between `loc` and `iloc` is how they index data in a DataFrame:

- **`loc`**: This is label-based indexing. You use the actual row and column labels to select data.
  ```python
  df.loc[2, "Name"]  # Select the value in row 2 with column label "Name"
  ```

- **`iloc`**: This is integer-based indexing. You use the numerical positions of rows and columns.
  ```python
  df.iloc[2, 1]  # Select the value at the 3rd row and 2nd column (0-based index)
  ```

### Example:
```python
import pandas as pd

data = {"Name": ["Alice", "Bob", "Charlie"], "Age": [25, 30, 35]}
df = pd.DataFrame(data)

# Using loc
print(df.loc[1, "Name"])  # Output: Bob

# Using iloc
print(df.iloc[1, 0])  # Output: Bob
```

### Summary:
- Use `loc` when you’re working with row/column labels.
- Use `iloc` when you’re working with their numeric positions.

- -------

What built-in data types are used in Python?
Python uses several built-in data types, including:

Number (int, float and complex)
String (str)
Tuple (tuple)
Range (range)
List (list)
Set (set)
Dictionary (dict)
------

How is a negative index used in Python?
Negative indexes are used in Python to assess and index lists and arrays from the end of your string, moving backwards towards your first value. For example, n-1 will show the last item in a list, while n-2 will show the second to last.
----


How would you find duplicate values in a dataset for a variable in Python?
You can check for duplicates using the Pandas duplicated() method. This will return a boolean series which is TRUE only for unique elements.

DataFrame.duplicated(subset=None,keep='last')

------

**Interviewer:** What is tuple unpacking, and why is it important?

**Candidate:** Tuple unpacking is the process of assigning the elements of a tuple to multiple variables in a single step. It’s a clean and concise way to work with grouped data, like tuples or lists, and can make code easier to read.

### Example:
Here’s how it works:
```python
coordinates = (10, 20)
x, y = coordinates  # Unpacking
print(f"x = {x}, y = {y}")
# Output: x = 10, y = 20
```

Tuple unpacking is a neat Python feature that simplifies working with structured data!


-----
14. What’s the difference between / and // in Python?
Both / and // are division operators. However, / does float division, dividing the first operand by the second. / returns the value in decimal form. // does floor division, dividing the first operand by the second, but returns the value in natural number form.

/ example: 9 / 2 returns 4.5
// example: 9 / 2 returns 4

---
What are arrays in Python?
Arrays store multiple values in one single variable. For example, you could create an array “faang” which included Facebook, Apple, Amazon, Netflix and Google.

Example:

faang = ["facebook", "apple", "amazon", "netflix", "google"]
print(faang)
Output:

['facebook', 'apple', 'amazon', 'netflix', 'google']
---------

Explain the zip() and enumerate() functions.
The enumerate() function returns the indexes of all items in lists, dictionaries, sets and other iterables. The zip() function combines multiple iterables.
----

**Interviewer:** Can you explain the difference between modules and packages in Python?

**Candidate:**  
Sure! 

A **module** is basically a single file that contains Python code. It can include functions, classes, and variables, and you can use it by importing it into other scripts. For example, a file called `math_operations.py` with functions for addition, subtraction, etc., is a module.

A **package** is a collection of related modules. It's like a folder that contains multiple Python files and usually includes an `__init__.py` file, which tells Python that the folder should be treated as a package. For instance, a package could include several modules for different math operations, like `addition.py`, `subtraction.py`, etc.

So, a module is one file, and a package is a collection of related files!
-------








**Interviewer:** Can you explain the difference between a list and an array?

**Candidate:**  
Sure!

A **list** in Python is a flexible data structure that can hold elements of different types (e.g., integers, strings, or even other lists). Lists are part of Python's built-in data types and can be modified easily. You can add, remove, or change elements within a list.

An **array**, on the other hand, is a more specialized data structure, usually from the `array` module or from libraries like NumPy. Arrays are typically used when you need to store large amounts of data of the same type (like all integers or all floats), making them more efficient in terms of memory and performance when handling numerical data.

To summarize:
- **List**: Can hold elements of different types, more flexible but slower for numerical operations.
- **Array**: Holds elements of the same type, more memory-efficient and faster for numerical computations.

For example:
```python
# List
my_list = [1, "two", 3.0]

# Array (from array module)
import array
my_array = array.array('i', [1, 2, 3])  # 'i' denotes integers


```

--------------
------


**Interviewer:** Can you explain the use of `self` in Python?

**Candidate:**  
Certainly! In Python, `self` is a reference to the current instance of a class. It's used to access the attributes and methods of the class within its own methods.

Whenever you define a method inside a class, the first parameter of that method is always `self`, which refers to the object calling the method. This allows you to work with the instance-specific data.

For example:
```python
class Car:
    def __init__(self, brand, model):
        self.brand = brand  # self refers to the current instance
        self.model = model  # self binds the attributes to the class

    def display_info(self):
        print(f"Car brand: {self.brand}, Model: {self.model}")

# Creating an instance of Car
my_car = Car("Toyota", "Corolla")
my_car.display_info()  # Outputs: Car brand: Toyota, Model: Corolla
```

Here, `self.brand` and `self.model` are instance variables, and `self` ensures that we're referring to the specific instance of the `Car` class, allowing us to access its data.


--------


Create a dataframe in Python.

We can create a dataframe in Python using the below code:

import pandas as pd
data = [['a', 1], ['b', 2], ['c', 3]]
df = pd.DataFrame(data, columns=['Alphabet', 'Number'])
print(df)
Output:

      Alphabet   Number
0          a              1
1          b              2
2          c              3
Question 12: Write a code to add a new column in the dataframe.

The new column in the dataframe can be added using the below code:

age = [27, 34, 56]
df['age'] = age
print(df)
-------

Write a code to delete a row from the dataframe.

The column ‘Number’ from the above-created dataframe can be deleted using code:

df.drop([‘Number’], axis = 1)

To drop 0th row, we can do it by:

df.drop(0)
--------


Write code to find the shape of an array in Python.

The shape of an array can be found using the command: arr.shape
-----


 Explain the difference between del and remove()

Del- It removes the item from a specified index.

Lst1 = [40, 30, 20, 10]
Del lst1[1]
Output:

[40, 20, 10]
Remove()- It removes the first matching value from the list.

Lst1 = [40, 30, 20, 10]
Lst1.remove(30)
Print(lst1)
Output:

[40, 20, 10]
-------


: Explain the usage of the strip() and lstrip().

Strip()- Used to remove all leading and trailing mentioned characters. Eg-

Str = “--analytics vidhya--“
Print(str.strip(‘-‘))
Output:

analytics vidhya
Lstrip()- Used to remove all leading mentioned characters.

print(str.lstrip(‘-‘))
Output:

Analytics vidhya--
--------







How would you merge two DataFrames in Pandas?
Answer:
In Pandas, merging two DataFrames can be done using the merge() function, similar to SQL joins. The function allows you to specify the type of join (inner, outer, left, right) and the key(s) to merge on. For example, pd.merge(df1, df2, on='key') merges df1 and df2 on the column key.

11. What is the use of the map() function in Python?
Answer:
The map() function in Python applies a given function to all items in an iterable (such as a list) and returns a map object (an iterator). It is commonly used for applying a function to each element of a list. For example, map(lambda x: x*2, [1, 2, 3, 4]) returns [2, 4, 6, 8].








--------
































































































































































