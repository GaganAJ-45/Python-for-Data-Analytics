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

#### 4. Scatter Plot

- Used to show relationship between two variables.
- ✔ Best for: Correlation analysis
```
import matplotlib.pyplot as plt
import numpy as np

x1 = np.array([0,1,2,3,4,5])
y1 = np.array([20,52,45,56,23,45])
x2 = np.array([0,1,2,3,4,5])
y2 = np.array([65,54,23,65,12,32])


plt.scatter(x1,y1, color="red",
             marker="o",
             s=100,
             label = "Class A")
plt.scatter(x2,y2, color="blue",
             marker="s",
             label = "Class B")

plt.title("Test score")
plt.xlabel("Hours Studied")
plt.ylabel('Grades')
plt.legend()
plt.show()
```
#### 5.Pie Chart

- Used to represent proportions.
- ✔ Best for: Percentage distribution
```
import matplotlib.pyplot as plt
categories = ["Gagan","aj","Sahil","Rohit","Satyarth"]
values =[10,20,40,30,10]
plt.pie(values, labels=categories,autopct = "%1.1f%%",shadow= True,startangle=90,explode = [0,0,0,0.1,0])
plt.show()
```

#### 5.subplot

```
import matplotlib.pyplot as plt
import numpy as np
#Figure = the entire canvas
#Axes  =  A single plot (Subplot)
x = np.array([1,2,3,4,5])

figure, axes =plt.subplots(2,2)
axes[0,0].plot(x,x**2,color ="red")
axes[0,0].set_title("x**2")

axes[0,1].bar(x,x**2,color="blue")
axes[0,1].set_title("x**2")

axes[1,0].scatter(x,x**3,color="green")
axes[1,0].set_title("x**3")

axes[1,1].plot(x,x**4,color="orange")
axes[1,1].set_title("x**4")

plt.tight_layout()
plt.show()
```

### 🎨 Customization in Matplotlib

Customization helps make graphs more readable and visually appealing.

🔧 1. Line Customization
```
plt.plot(x, y, color='blue', linestyle='dashed', linewidth=2, marker='o')
```
- color → Line color
- linestyle → solid, dashed, dotted
- linewidth → Thickness
- marker → Point symbol

🎯 2. Labels and Title
```
plt.title("Graph Title")
plt.xlabel("X-axis Label")
plt.ylabel("Y-axis Label")
```
🌈 3. Grid and Style
```
plt.grid(True)
```
- ✔ Helps in better readability

📌 4. Legend
```
plt.plot(x, y, label="Data 1")
plt.legend()
```
- ✔ Used when multiple plots are present

🎨 5. Colors and Transparency
```
plt.bar(x, y, color='green', alpha=0.7)
```
- alpha → Transparency (0 to 1)

📏 6. Figure Size
```
plt.figure(figsize=(8, 5))
```
✔ Controls graph size
