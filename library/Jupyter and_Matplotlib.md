## **🚀 Why Jupyter Notebook?**

Jupyter Notebook is widely used for data analysis and machine learning.

Advantages:
- 🌐 Runs in a web browser
- 🧠 User-friendly interface
- 📄 Easy documentation with code + text
- 🎯 Great for demonstration and visualization
- ✏️ Command mode allows easy editing and execution

---

## *📚 What is a Python Library?*

A Python library is a collection of pre-written code that helps solve common problems.

👉 Instead of writing everything from scratch, you can reuse functions.

```python
#Example:
import math
print(math.sqrt(16))
```
```python
✔ Output:

4.0
```

## *📈 Why Libraries Matter in Data Analytics*
- ⚡ Faster development
- 🔁 Reusability of code
- 📊 Standardized methods
- 📉 Efficient data handling

### 🧰 Core Data Analytics Stack
- Library       --       	Purpose
- NumPy           --   	Numerical computing
- Pandas           --  	Data manipulation
- Matplotlib       -- 	Data visualization


## **📊 Matplotlib Library**

Matplotlib is used for visualizing data using graphs.

Features:
Create plots, charts, histograms
Customize graphs (color, markers, labels)
Works well with NumPy & Pandas

#### Installation:
```bash
pip install matplotlib
```
#### Import:
```python
import matplotlib.pyplot as plt
```
#### 📉 Basic Line Plot Example
```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4]
y = [5, 6, 7, 8]

plt.plot(x, y)
plt.show()
```

---

### 📊 Types of Graphs in Matplotlib

Matplotlib provides multiple types of graphs to visualize different kinds of data effectively.

#### 📈 1. Line Plot

- Used to show trends or changes over time.
- ✔ Best for: Time-series data, trends

```python
import matplotlib.pyplot as plt
x = [2023,2024,2025,2026]
y =[25,23,16,23]
y1 = [20,22,18,21]
y2 = [25,32,48,31]

linestyles = {"marker": ".", "markersize": 10, "markerfacecolor": "red", "markeredgecolor": "red", "linestyle": "solid", "linewidth": 2}
plt.xlabel("Year",fontsize = 20,family = "Ariel",fontweight = "bold",color = "red")
plt.ylabel("Class Size",fontsize = 20,family = "Ariel",fontweight = "bold",color = "black")
plt.title("Class size",fontsize = 20,family = "Ariel",fontweight = "bold",color = "green")
plt.plot(x, y, color="blue", **linestyles)
plt.plot(x, y1, color="green", **linestyles)
plt.plot(x, y2, color="orange", **linestyles)
plt.xticks(x)
plt.grid(axis = "y", linestyle = "--", linewidth = 0.5 )
plt.show()
```
#### 2. Bar Chart

- Used to compare values across categories.
- ✔ Best for: Comparisons
```python
import matplotlib.pyplot as plt
category = ["Grains","fruit","Vegitable","Meat","Dairy"]

values = [10,20,40,30,10]
plt.bar(category, values, color=["blue","green","orange","red","purple"])
plt.title("Daily consumtion")
plt.xlabel("Food")
plt.ylabel("Quantity")
plt.show()      
```

#### 3. Histogram

- Used to show frequency distribution of data.
```
data = [1, 2, 2, 3, 3, 3, 4, 5]

plt.hist(data, bins=5)
plt.title("Histogram")
plt.show()
```
- ✔ Best for: Data distribution

