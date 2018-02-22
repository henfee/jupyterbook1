## Introducing the multidimensional array in NumPy for fast array computations
## 在NumPy中引入多维数组进行快速数组计算

NumPy is the main foundation of the scientific Python ecosystem. This library offers a specific data structure for high-performance numerical computing: the multidimensional array. The rationale behind NumPy is the following: Python being a high-level dynamic language, it is easier to use but slower than a low-level language such as C. NumPy implements the multidimensional array structure in C and provides a convenient Python interface, thus bringing together high performance and ease of use. NumPy is used by many Python libraries. For example, pandas is built on top of NumPy.
NumPy是科学Python生态系统的主要基础。 该库为高性能数值计算提供了一个特定的数据结构：多维数组。 NumPy背后的基本原理如下：Python是一种高级动态语言，它使用起来更容易，但比C这样的低级语言慢。NumPy在C中实现了多维数组结构，因此提供了一个方便的Python接口。 汇集了高性能和易用性。 NumPy被许多Python库使用。 例如，pandas建立在NumPy之上。

In this recipe, we will illustrate the basic concepts of the multidimensional array. A more comprehensive coverage of the topic can be found in the book, Learning IPython for Interactive Computing and Data Visualization, Second Edition, Packt Publishing.
在这个小节中，我们将说明多维数组的基本概念。 关于这个话题的更全面的讲解可以在这本书中找到，Learning IPython for Interactive Computing and Data Visualization，Second Edition，Packt Publishing。


### **How to do it...如何做**

1. Let's import the built-in random Python module and NumPy:
让我们导入内置的随机Python模块和NumPy：

```Python
>>> import random
    import numpy as np
```

2. We generate two Python lists, x and y, each one containing 1 million random numbers between 0 and 1:
我们生成两个Python列表x和y，每个列表包含0和1之间的1百万个随机数字：

```Python
>>> n = 1000000
    x = [random.random() for _ in range(n)]
    y = [random.random() for _ in range(n)]
>>> x[:3], y[:3]
([0.926, 0.722, 0.962], [0.291, 0.339, 0.819])
```

3. Let's compute the element-wise sum of all of these numbers: the first element of x plus the first element of y, and so on. We use a for loop in a list comprehension:
让我们计算所有这些数字的元素总和：x的第一个元素加上y的第一个元素，依此类推。我们在列表中使用for循环来理解：

```Python
>>> z = [x[i] + y[i] for i in range(n)]
    z[:3]
[1.217, 1.061, 1.781]
```
4. How long does this computation take? IPython defines a handy `%timeit` magic command to quickly evaluate the time taken by a single statement:
这个计算需要多长时间？ IPython定义了一个方便的`％timeit` magic命令来快速评测单个语句花费的时间：

```Python
>>> %timeit [x[i] + y[i] for i in range(n)]
101 ms ± 5.12 ms per loop (mean ± std. dev. of 7 runs,
    10 loops each)
```
5. Now we will perform the same operation with NumPy. NumPy works on multidimensional arrays, so we need to convert our lists to arrays. The `np.array()` function does just that:
现在我们将使用NumPy执行相同的操作。 NumPy适用于多维数组，因此我们需要将我们的列表转换为数组。 `np.array()`函数是这样做的：

```Python
>>> xa = np.array(x)
    ya = np.array(y)
>>> xa[:3]
array([ 0.926,  0.722,  0.962])
```
The `xa` and `ya` arrays contain the exact same numbers that our original lists, `x` and `y`, contained. Those lists were instances of the list built-in class, while our arrays are instances of the `ndarray` NumPy class. These types are implemented very differently in Python and NumPy. In this example, we will see that using arrays instead of lists leads to drastic performance improvements.
`xa`和`ya`数组包含与我们原始列表`x`和`y`所包含的完全相同的数字。这些列表是列表内置类的实例，而我们的数组是`ndarray` NumPy类的实例。这些类型在Python和NumPy中的实现是非常不同。在这个例子中，我们将看到使用数组而不是列表会导致显著的性能改进。

6. To compute the element-wise sum of these arrays, we don't need to do a `for` loop anymore. In NumPy, adding two arrays means adding the elements of the arrays component-by-component. This is the standard mathematical notation in linear algebra (operations on vectors and matrices):
为了计算这些数组的元素总和，我们不需要再做一个for循环。在NumPy中，添加两个数组表示逐个添加数组的元素。这是线性代数中的标准数学符号（对矢量和矩阵的运算）：


```python
>>> za = xa + ya
    za[:3]
array([ 1.217,  1.061,  1.781])
```
We see that the `z` list and the `za` array contain the same elements (the sum of the numbers in `x` and `y`).
我们看到`z`列表和`za`数组包含相同的元素（x和y中的数字之和）。

> **TIP提示**

> Be careful not to use the + operator between vectors when they are represented as Python lists! This operator is valid between lists, so it would not raise an error and it could lead to subtle and silent bugs. In fact, `list1 + list2` is the concatenation of two lists, not the element-wise addition.
> 当它们被表示为Python列表时，请小心不要在向量之间使用+运算符！这个操作符在列表之间有效，所以它不会引发错误，并且可能导致细微和无声的错误。实际上，`list1 + list2`是两个列表的连接，而不是元素相加。

7. Let's compare the performance of this NumPy operation with the native Python loop:
我们来进行下使用NumPy操作与使用本地Python循环的性能比较:

```python
>>> %timeit xa + ya
1.09 ms ± 37.3 µs per loop (mean ± std. dev. of 7 runs,
    1000 loops each)
```

With NumPy, we went from 100 ms down to 1 ms to compute one million additions!
使用NumPy，计算一百万次加法，我们从100毫秒降低到1毫秒！

8. Now we will compute something else: the sum of all elements in `x` or `xa`. Although this is not an element-wise operation, NumPy is still highly efficient here. The pure Python version uses the built-in `sum()` function on an iterable. The NumPy version uses the `np.sum()` function on a NumPy array:
现在我们将计算其他东西：`x`或`xa`中所有元素的总和。虽然这不是一个元素操作，但NumPy在这里仍然非常高效。纯Python版本在迭代器上使用内置的`sum()`函数。 NumPy版本在NumPy数组上使用`np.sum()`函数：

```python
>>> %timeit sum(x)  # pure Python
3.94 ms ± 4.44 µs per loop (mean ± std. dev. of 7 runs
    100 loops each)
>>> %timeit np.sum(xa)  # NumPy
298 µs ± 4.62 µs per loop (mean ± std. dev. of 7 runs,
    1000 loops each)
```

We also observe a significant speedup here.
我们也观察到了显著的加速。

9. Let's perform one last operation: computing the arithmetic distance between any pair of numbers in our two lists (we only consider the first 1000 elements to keep computing times reasonable). First, we implement this in pure Python with two nested for loops:
让我们执行最后一个操作：计算两个列表中任意一对数字之间的算术距离（我们只考虑前1000个元素来保持计算时间合理）。首先，我们用两个嵌套的for循环在纯Python中实现它：

```python

>>> d = [abs(x[i] - y[j])
         for i in range(1000)
         for j in range(1000)]
>>> d[:3]
[0.635, 0.587, 0.106]
```

10. Now, we use a NumPy implementation, bringing out two slightly more advanced notions. First, we consider a **two-dimensional array** (or matrix). This is how we deal with the two indices, `i` and `j`. Second, we use **broadcasting** to perform an operation between a 2D array and 1D array. We will give more details in the *How it works...* section.
现在，我们使用NumPy实现，提出两个稍微更高级的概念。首先，我们考虑一个 **二维数组**（或矩阵）。这就是我们如何处理这两个指数，`i`和`j`。其次，我们使用 **广播** 来执行2D阵列和1D阵列之间的操作。我们将在 *工作原理* 一节中提供更多详细信息。

```python

>>> da = np.abs(xa[:1000, np.newaxis] - ya[:1000])
>>> da
array([[ 0.635,  0.587,  ...,  0.849,  0.046],
       [ 0.431,  0.383,  ...,  0.646,  0.158],
       ...,
       [ 0.024,  0.024,  ...,  0.238,  0.566],
       [ 0.081,  0.033,  ...,  0.295,  0.509]])
>>> %timeit [abs(x[i] - y[j]) \
             for i in range(1000) \
             for j in range(1000)]
134 ms ± 1.79 ms per loop (mean ± std. dev. of 7 runs,
    1000 loops each)
>>> %timeit np.abs(xa[:1000, np.newaxis] - ya[:1000])
1.54 ms ± 48.9 µs per loop (mean ± std. dev. of 7 runs
    1000 loops each)
```

Here again, we observe a significant speedup.
在这里我们再次观察到显著的加速。

## **How it works...如何运行**

A NumPy array is a homogeneous block of data organized in a multidimensional finite grid. All elements of the array share the same data type, also called `dtype` (integer, floating-point number, and so on). The shape of the array is an n-tuple that gives the size of each axis.
NumPy数组是在多维有限网格中组织的同质数据块。该数组的所有元素共享相同的数据类型，也称为`dtype`（整数，浮点数等）。数组的形状是一个n元组，它给出了每个轴的大小。
`
A 1D array is a **vector**; its shape is just the number of components.
一维数组是一个 **矢量**;它的形状只是组件的数量。


A 2D array is a **matrix**; its shape is (number of rows, number of columns).
2D阵列是一个 **矩阵**;它的形状是（行数，列数）。

The following diagram illustrates the structure of a 3D (3, 4, 2) array that contains 24 elements:
下图说明了包含24个元素的3D（3，4，2）数组的结构：
![](https://www.safaribooksonline.com/library/view/ipython-interactive-computing/9781785888632/graphics/B04857_01_18.jpg)

*A NumPy array*

*一个NumPy数组*

The slicing syntax in Python translates nicely to array indexing in NumPy. Also, we can add an extra dimension to an existing array, using `np.newaxis` in the index.
Python中的切片语法很好地转换为NumPy中的数组索引。另外，我们可以在索引中使用`np.newaxis`为现有数组添加额外的维度。


Element-wise arithmetic operations can be performed on NumPy arrays that have the same shape. However, broadcasting relaxes this condition by allowing operations on arrays with different shapes in certain conditions. Notably, when one array has fewer dimensions than the other, it can be virtually stretched to match the other array's dimension. This is how we computed the pairwise distance between any pair of elements in `xa` and `ya`.
可以对具有相同形状的NumPy数组上执行基于元素的算术运算。但是，通过允许在特定条件下对不同形状的阵列进行操作, 广播可以放宽此条件。
值得注意的是，当一个阵列的维数比另一个少时，它可以被虚拟拉伸以匹配另一个阵列的维度。这就是我们如何计算`xa`和`ya`中任何元素对之间的成对距离。

How can array operations be so much faster than Python loops? There are several reasons, and we will review them in detail in Chapter 4, *Profiling and Optimization*. We can already say here that:
数组操作如何比Python循环快得多？有几个原因，我们将在第4章 *“分析和优化”* 中详细介绍它们。我们可以在这里说：

In NumPy, array operations are implemented internally with C loops rather than Python loops. Python is typically slower than C because of its interpreted and dynamically-typed nature.
The data in a NumPy array is stored in a contiguous block of memory in RAM. This property leads to more efficient use of CPU cycles and cache.
在NumPy中，数组操作是用C循环而不是Python循环在内部实现的。由于Python的解释性和动态类型性质，Python通常比C慢。
NumPy数组中的数据存储在RAM中的连续内存块中。该属性可以更有效地使用CPU周期和缓存。

### **There's more...还有更多...**

There's obviously much more to say about this subject. The prequel of this book, Learning IPython for Interactive Computing and Data Visualization, Second Edition, Packt Publishing, contains more details about basic array operations. We will use the array data structure routinely throughout this book. Notably, Chapter 4, *Profiling and Optimization*, covers advanced techniques of using NumPy arrays.
关于这个问题显然有更多要说的。本书的前言，学习IPython for Interactive Computingand and Data Visualization，第二版，Packt Publishing，包含有关基本数组操作的更多细节。在本书中我们将常规使用数组数据结构。值得注意的是，第4章 *“分析和优化”* 包含了使用NumPy阵列的高级技术。

Here are some more references:
这里有更多的参考资料：

* Introduction to the ndarray on NumPy's documentation available at http://docs.scipy.org/doc/numpy/reference/arrays.ndarray.html
* Tutorial on the NumPy array available at https://docs.scipy.org/doc/numpy-dev/user/quickstart.html
* The NumPy array in the SciPy lectures notes, at http://scipy-lectures.github.io/intro/numpy/array_object.html
* NumPy for MATLAB users, at https://docs.scipy.org/doc/numpy-dev/user/numpy-for-matlab-users.html

### **See also 补充阅读**
* The Getting started with exploratory data analysis in the Jupyter Notebook recipe
* The Understanding the internals of NumPy to avoid unnecessary array copying recipe in Chapter 4, Profiling and Optimization
