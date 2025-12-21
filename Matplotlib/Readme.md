## 1\. What Matplotlib REALLY is (mental model first)

Matplotlib is a **plotting engine** for Python.

At its core, it works like this:

> **Figure → Axes → Plot elements**

*   **Figure** = the whole canvas (the window/image)
    
*   **Axes** = the actual chart area (x–y system)
    
*   **Plot elements** = lines, dots, bars, text, etc.
    

Most beginners struggle because they jump straight into code without understanding this structure.

* * *

## 2\. Installation & setup (1-time thing)

    pip install matplotlib
    

Basic import (this matters):

    import matplotlib.pyplot as plt
    

`plt` is a **state-machine interface**.  
It keeps track of the “current figure” and “current axes” for you.

* * *

## 3\. Your FIRST plot (absolute beginner)

    import matplotlib.pyplot as plt
    
    x = [1, 2, 3, 4]
    y = [10, 20, 25, 30]
    
    plt.plot(x, y)
    plt.show()
    

What happened internally?

*   Matplotlib created a **Figure**
    
*   Added **one Axes**
    
*   Drew a **line**
    
*   Displayed it
    

That’s it.

* * *

## 4\. Customizing the plot (labels, title, grid)

This is where people start to feel powerful.

    plt.plot(x, y)
    plt.xlabel("X values")
    plt.ylabel("Y values")
    plt.title("My First Line Plot")
    plt.grid(True)
    plt.show()
    

These are not decorations — they are **metadata for humans**.

* * *

## 5\. Line styles, markers, colors (control aesthetics)

    plt.plot(
        x, y,
        color="red",
        line,
        marker="o",
        linewidth=2
    )
    plt.show()
    

Common values:

*   colors: `"red"`, `"blue"`, `"black"`, `"#FF5733"`
    
*   linestyle: `"-"`, `"--"`, `":"`
    
*   marker: `"o"`, `"s"`, `"^"`
    

* * *

## 6\. Multiple lines on one graph

    y2 = [5, 15, 20, 25]
    
    plt.plot(x, y, label="Dataset 1")
    plt.plot(x, y2, label="Dataset 2")
    
    plt.legend()
    plt.show()
    

Legend exists **only if you label things**.

* * *

## 7\. Scatter plots (points instead of lines)

Use scatter when order doesn’t matter.

    plt.scatter(x, y)
    plt.show()
    

With customization:

    plt.scatter(x, y, s=100, alpha=0.7)
    

*   `s` = size
    
*   `alpha` = transparency (0–1)
    

* * *

## 8\. Bar charts (very common in ML & reports)

    names = ["A", "B", "C"]
    scores = [80, 65, 90]
    
    plt.bar(names, scores)
    plt.show()
    

Horizontal bars:

    plt.barh(names, scores)
    

* * *

## 9\. Histograms (distribution visualization)

Extremely important for data science.

    import random
    
    data = [random.randint(1, 100) for _ in range(1000)]
    
    plt.hist(data, bins=20)
    plt.show()
    

This shows **frequency distribution**.

* * *

## 10\. Figure size & DPI (important for reports & GitHub)

    plt.figure(figsize=(8, 6), dpi=100)
    plt.plot(x, y)
    plt.show()
    

*   `figsize` → inches
    
*   `dpi` → resolution
    

* * *

## 11\. Subplots (multiple charts in one figure)

This is where people level up.

    fig, ax = plt.subplots(2, 1)
    
    ax[0].plot(x, y)
    ax[0].set_title("First Plot")
    
    ax[1].plot(x, y2)
    ax[1].set_title("Second Plot")
    
    plt.tight_layout()
    plt.show()
    

Now you’re **explicitly controlling Axes** instead of relying on `plt`.

This is the **recommended way** for serious work.

* * *

## 12\. Object-Oriented Matplotlib (IMPORTANT)

This is how professionals use it.

    fig, ax = plt.subplots()
    
    ax.plot(x, y)
    ax.set_xlabel("X")
    ax.set_ylabel("Y")
    ax.set_title("OOP Style Plot")
    
    plt.show()
    

Why this matters:

*   Better control
    
*   Cleaner code
    
*   Required for complex dashboards
    

* * *

## 13\. Annotations (text on graphs)

    ax.annotate(
        "Peak",
        xy=(3, 25),
        xytext=(2, 30),
        arrowprops=dict(arrow)
    )
    

Great for explaining insights.

* * *

## 14\. Saving plots (GitHub / reports)

    plt.savefig("plot.png", bbox_inches="tight")
    

Use this **before** `plt.show()`.

Formats:

*   PNG
    
*   JPG
    
*   PDF
    
*   SVG (best for quality)
    

* * *

## 15\. Styling & themes

    plt.style.use("ggplot")
    

Other styles:

*   `"seaborn"`
    
*   `"classic"`
    
*   `"dark_background"`
    

* * *

## 16\. Real-world ML example (important for you)

    plt.scatter(y_test, y_pred)
    plt.xlabel("Actual")
    plt.ylabel("Predicted")
    plt.title("Actual vs Predicted")
    
    plt.plot(
        [y_test.min(), y_test.max()],
        [y_test.min(), y_test.max()]
    )
    
    plt.show()
    

That diagonal line means:

> **Perfect prediction line**

Points near the line = good model.

* * *

## 17\. Common beginner mistakes (read this twice)

*   Forgetting `plt.show()`
    
*   Mixing `plt` and `ax` styles randomly
    
*   Not labeling axes
    
*   Using default sizes for reports
    
*   Overcrowding one plot with too much data
    

* * *
