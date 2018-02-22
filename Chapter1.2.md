## Getting started with exploratory data analysis in the Jupyter Notebook
开始使用Jupyter Notebook中的探索性数据分析


In this recipe, we will give an introduction to IPython and Jupyter for data analysis. Most of the subject has been covered in the prequel of this book, Learning IPython for Interactive Computing and Data Visualization, Second Edition, Packt Publishing, but we will review the basics here.

在这个部分，我们将介绍使用IPython和Jupyter进行数据分析。 这个主题的大部分内容已经在本书(Learning IPython for Interactive Computing and Data Visualization, Second Edition, Packt Publishing)的前言中介绍过，但我们将在这里回顾一下基础知识。

We will download and analyze a dataset about attendance on Montreal's bicycle tracks. This example is largely inspired by a presentation from Julia Evans (available at https://github.com/jvns/talks/blob/master/2013-04-mtlpy/pistes-cyclables.ipynb). Specifically, we will introduce the following:

我们将下载并分析一个关于蒙特利尔自行车道出行率的数据集。 这个例子很大程度上收到Julia Evans（https://github.com/jvns/talks/blob/master/2013-04-mtlpy/pistes-cyclables.ipynb）对此介绍而激发。 具体来说，我们将介绍以下内容：

* Data manipulation with pandas
* Data visualization with Matplotlib
* Interactive widgets

* 使用pandas进行数据处理
* 使用Matplotlib进行数据可视化
* 交互式小部件


### **How to do it... 如何做...**

1. The very first step is to import the scientific packages we will be using in this recipe, namely NumPy, pandas, and Matplotlib. We also instruct Matplotlib to render the figures as inline images in the Notebook:

第一步是导入我们将在此小节中使用的科学软件包，即NumPy，pandas和Matplotlib。 我们还需设置Matplotlib在Notebook中将图形呈现为内联图像：

```python
  >>> import numpy as np
      import pandas as pd
      import matplotlib.pyplot as plt
      %matplotlib inline
```

> **TIP 提示**

> We can enable high-resolution Matplotlib figures on Retina display systems with the following commands:我们可以使用以下命令在Retina显示系统上启用高分辨率Matplotlib数字：

>  ```python
>      from IPython> .display import set_matplotlib_formats
>      set_matplotlib  _formats('retina')
>   ```

2. Now, we create a new Python variable called url that contains the address to a Comma-separated Values (CSV) data file. This standard text-based file format is used to store tabular data:
现在，我们创建一个名为url的新Python变量用来保存一个逗号分隔值（CSV）数据文件的地址。 这种标准的基于文本的文件格式用于存储表格数据：

```python
  >>> url = ("https://raw.githubusercontent.com/"
            "ipython-books/cookbook-2nd-data/"
            "master/bikes.csv")
```

3. pandas defines a `read_csv()` function that can read any CSV file. Here, we pass the URL to the file. pandas will automatically download the file, parse it, and return a DataFrame object. We need to specify a few options to make sure that the dates are parsed correctly:
pandas定义了一个可以读取任何CSV文件的`read_csv（）`函数。 在这里，我们将URL传递给文件。 pandas将自动下载文件，解析它，并返回一个DataFrame对象。 我们需要指定几个选项来确保正确解析日期：

```python
  >>> df = pd.read_csv(url, index_col='Date',
                      parse_dates=True, dayfirst=True)
```

4. The `df` variable contains a DataFrame object, a specific pandas data structure that contains 2D tabular data. The `head(n)` method displays the first n rows of this table. In the Notebook, pandas displays a DataFrame object in an HTML table, as shown in the following screenshot:
这个`df`变量包含一个DataFrame对象，一个包含2D表格数据的特定pandas数据结构。 `head(n)`方法显示此表的前n行。 在Notebook中，pandas在HTML表格中显示DataFrame对象，如以下屏幕截图所示：

```python

  >> df.head(2)
```

![](https://www.safaribooksonline.com/library/view/ipython-interactive-computing/9781785888632/graphics/B04857_01_07.jpg)

Here, every row contains the number of bicycles on every track of the city, for every day of the year.
在这里，每一行都包含这个城市每年每一天每条自行车道的自行车数量。

5. We can get some summary statistics of the table with the `describe()` method:
我们可以使用`describe()`方法得到表格的一些总结性统计信息：

```python
  >>> df.describe()
```
![](https://www.safaribooksonline.com/library/view/ipython-interactive-computing/9781785888632/graphics/B04857_01_08.jpg)

6. Let's display some figures. We will plot the daily attendance of two tracks. First, we select the two columns, `Berri1` and `PierDup`. Then, we call the `plot()`` method:
让我们来展示一些图表。 我们将绘制两条自行车道的每日自行车数量情况。 首先，我们选择两列，`Berri1`和`PierDup`。 然后，我们调用`plot()`方法：


```python
>>> df[['Berri1', 'PierDup']].plot(figsize=(10, 6),
                                   style=['-', '--'],
                                   lw=2)
```

![](https://www.safaribooksonline.com/library/view/ipython-interactive-computing/9781785888632/graphics/B04857_01_09.jpg)


7. Now, we move to a slightly more advanced analysis. We will look at the attendance of all tracks as a function of the weekday. We can get the weekday easily with pandas: the `index` attribute of the DataFrame object contains the dates of all rows in the table. This index has a few date-related attributes, including `weekday_name`:
现在，我们进行一个稍微更高级的分析。 我们希望将所有自行车道的出行率情况看作weekday的函数。 我们可以通过pandas轻松获得工作日：DataFrame对象的索引属性(`index`)包含表中所有行的日期。 该索引有几个与日期相关的属性，包括weekday_name：


```python
>>> df.index.weekday_name
Index(['Tuesday', 'Wednesday', 'Thursday', 'Friday',
       'Saturday', 'Sunday', 'Monday', 'Tuesday',
       ...
       'Friday', 'Saturday', 'Sunday', 'Monday',
       'Tuesday', 'Wednesday'],
      dtype='object', name='Date', length=261)
```

8. To get the attendance as a function of the weekday, we need to group the table elements by the weekday. The `groupby()` method lets us do just that. We use `weekday` instead of `weekday_name` to keep the weekday order (Monday is `0`, Tuesday is `1`, and so on). Once grouped, we can sum all rows in every group:
为了将出行率作为weekday的函数，我们需要按weekday对表格元素进行分组。 `groupby()`方法可以让我们做到这一点。 我们使用`weekday`而不是`weekday_name`来让weekday排序（星期一为`0`，星期二为`1`，依此类推）。 一旦分组，我们可以对每组中的所有行进行求和：

```python
>>> df_week = df.groupby(df.index.weekday).sum()
>>> df_week
```
![](https://www.safaribooksonline.com/library/view/ipython-interactive-computing/9781785888632/graphics/B04857_01_10.jpg)


9. We can now display this information in a figure. We create a Matplotlib figure, and we use the `plot()` method of DataFrame to create our plot:
我们现在可以在一个图表中显示这些信息。 我们创建一个Matplotlib图，我们使用DataFrame的`plot()`方法来创建我们的图表：

```python
>>> fig, ax = plt.subplots(1, 1, figsize=(10, 8))
    df_week.plot(style='-o', lw=3, ax=ax)
    ax.set_xlabel('Weekday')
    # We replace the labels 0, 1, 2... by the weekday
    # names.
    ax.set_xticklabels(
        ('Monday,Tuesday,Wednesday,Thursday,'
         'Friday,Saturday,Sunday').split(','))
    ax.set_ylim(0)  # Set the bottom axis to 0.

```
![](https://www.safaribooksonline.com/library/view/ipython-interactive-computing/9781785888632/graphics/B04857_01_11.jpg)

10. Finally, let's illustrate the interactive capabilities of the Notebook. We will plot a smoothed version of the track attendance as a function of time (rolling mean). The idea is to compute the mean value in the neighborhood of any day. The larger the neighborhood, the smoother the curve. We will create an interactive slider in the Notebook to vary this parameter in real time in the plot. All we have to do is add the `@interact` decorator above our plotting function:
最后，让我们来说明Notebook的交互功能。 我们将绘制一个自行车道出行率作为时间的函数（滚动平均值）的平滑版本。 这个想法是计算任何一天的领域的平均值。 邻域越大，曲线越平滑。 我们将在Notebook中创建一个交互式滑块，以实时更改该图中的这个参数。 我们所要做的就是在绘图函数上面添加`@interact`装饰器：


```python
>>> from ipywidgets import interact

    @interact
    def plot(n=(1, 30)):
        fig, ax = plt.subplots(1, 1, figsize=(10, 8))
        df['Berri1'].rolling(window=n).mean().plot(ax=ax)
        ax.set_ylim(0, 7000)
        plt.show()
```

![](https://www.safaribooksonline.com/library/view/ipython-interactive-computing/9781785888632/graphics/B04857_01_12.jpg)

## **How it works...如何工作**

To create Matplotlib figures, it is good practice to create a Figure (`fig`) and one or several Axes (subplots, `ax` object) objects with the `plt.subplots()` command. The figsize keyword argument lets us specify the size of the figure, in inches. Then, we call plotting methods directly on the Axes instances. Here, for example, we set the y limits of the axis with the `set_ylim()` method. If there are existing plotting commands, like the `plot()` method provided by pandas on DataFrame instances, we can pass the relevant Axis instance with the `ax` keyword argument.
要创建Matplotlib图表，最好使用`plt.subplots()`命令创建一个图（`fig`）和一个或多个Axes（subplots，`ax`对象）对象。 figsize关键字参数让我们指定图的大小，以英寸为单位。 然后，我们直接在Axes实例上调用绘图方法。 在这里，例如，我们用`set_ylim（）`方法设置轴的y轴限制。 如果有现有的绘图命令，比如在DataFrame实例上由pandas提供的`plot（）`方法，我们可以通过`ax`关键字参数传递相关的Axis实例。

## **There's more... 更多**

pandas is the main data wrangling library in Python. Other tools and methods are generally required for more advanced analyses (signal processing, statistics, and mathematical modeling). We will cover these steps in the second part of this book, starting with Chapter 7, Statistical Data Analysis.
pandas是Python中主要的数据wrangling库。 其他工具和方法通常需要进行更高级的分析（信号处理，统计和数学建模）。 我们将在本书的第二部分介绍这些步骤，从第7章统计数据分析开始。

Here are some more references about data manipulation with pandas:
这里有更多关于pandas数据处理的参考资料：

* Learning IPython for Interactive Computing and Data Visualization, Second Edition, Packt Publishing, the prequel of this book
* Python for Data Analysis, O'Reilly Media, by Wes McKinney, the creator of pandas, at http://shop.oreilly.com/product/0636920023784.do
* Python Data Science Handbook, O'Reilly Media, by Jake VanderPlas, at http://shop.oreilly.com/product/0636920034919.do
* The documentation of pandas available at http://pandas.pydata.org/pandas-docs/stable/
* Usage guide of Matplotlib, at https://matplotlib.org/tutorials/introductory/usage.html

## **See also 补充阅读**
* The Introducing the multidimensional array in NumPy for fast array computations recipe
