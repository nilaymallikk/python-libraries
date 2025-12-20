# Matplotlib Complete Guide (Beginner to Advanced)

Matplotlib is a Python library used for data visualization. It allows you to convert raw numerical data into meaningful visual representations such as line plots, bar charts, scatter plots, histograms, and more. It is widely used in data science, machine learning, research, and analytics because it provides full control over every element of a plot.

To install Matplotlib, use:
pip install matplotlib

To import it in Python:
import matplotlib.pyplot as plt

A basic line plot is the foundation of Matplotlib. You provide x and y values, and Matplotlib draws a line connecting the points.

Example:
import matplotlib.pyplot as plt
x = [1, 2, 3, 4]
y = [10, 20, 30, 40]
plt.plot(x, y)
plt.show()

Adding labels and titles is essential for readability. Without labels, plots are meaningless to others.

plt.plot(x, y)
plt.xlabel("X Axis")
plt.ylabel("Y Axis")
plt.title("Basic Line Plot")
plt.grid(True)
plt.show()

Figure size and DPI control how large and clear your plot appears, especially when exporting images.

plt.figure(figsize=(8, 5), dpi=100)
plt.plot(x, y)
plt.show()

You can plot multiple lines on the same graph to compare datasets.

y2 = [5, 15, 25, 35]
plt.plot(x, y, label="Dataset 1")
plt.plot(x, y2, label="Dataset 2")
plt.legend()
plt.show()

Matplotlib allows customization of line style, markers, and colors to improve clarity.

plt.plot(x, y, linestyle="--", marker="o", color="blue")
plt.show()

Scatter plots are useful when analyzing relationships or distributions of points, especially in machine learning datasets.

plt.scatter(x, y)
plt.xlabel("X")
plt.ylabel("Y")
plt.title("Scatter Plot")
plt.show()

Bar charts are ideal for categorical data comparison.

names = ["A", "B", "C"]
scores = [80, 70, 90]
plt.bar(names, scores)
plt.title("Bar Chart")
plt.show()

Histograms help visualize the distribution of numerical data.

import random
data = [random.randint(1, 100) for _ in range(100)]
plt.hist(data, bins=10)
plt.title("Histogram")
plt.show()

Pie charts represent proportions but should be used sparingly.

labels = ["Python", "Java", "C++"]
sizes = [50, 30, 20]
plt.pie(sizes, labels=labels, autopct="%1.1f%%")
plt.title("Pie Chart")
plt.show()

Subplots allow multiple plots within the same figure.

plt.subplot(1, 2, 1)
plt.plot(x, y)
plt.title("Plot 1")
plt.subplot(1, 2, 2)
plt.plot(x, y2)
plt.title("Plot 2")
plt.show()

Saving figures is important for reports, GitHub repositories, and presentations.

plt.plot(x, y)
plt.savefig("plot.png")
plt.show()

The object-oriented approach is the professional and scalable way to use Matplotlib.

fig, ax = plt.subplots()
ax.plot(x, y)
ax.set_title("Object Oriented Plot")
ax.set_xlabel("X Axis")
ax.set_ylabel("Y Axis")
plt.show()

You can control axis limits and ticks to focus attention on specific data ranges.

plt.plot(x, y)
plt.xlim(0, 5)
plt.ylim(0, 50)
plt.xticks([1, 2, 3, 4])
plt.show()

Common beginner mistakes include forgetting plt.show(), not labeling axes, overusing colors, misusing pie charts, and failing to save plots properly.

Matplotlib should be used when full control over visual output is required, especially in machine learning, scientific research, or publication-quality plots.

Practice ideas include plotting daily study hours, visualizing exam score distributions, comparing actual vs predicted values in ML models, and building multi-plot dashboards.

Matplotlib may feel verbose initially, but once its structure is understood, it becomes a powerful tool capable of visualizing any dataset clearly and professionally.
