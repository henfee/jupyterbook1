## Introducing IPython and the Jupyter Notebook
## 介绍IPython和Jupyter Notebook

The Jupyter Notebook is a web-based interactive environment that combines code, rich text, images, videos, animations, mathematical equations, plots, maps, interactive figures and widgets, and graphical user interfaces, into a single document. This tool is an ideal gateway to high-performance numerical computing and data science in Python, R, Julia, or other languages. In this book, we will mostly use the Python language, although there are recipes introducing R and Julia.

Jupyter Notebook是一个基于网络的交互式环境，它将代码，富文本，图像，视频，动画，数学公式，图表，地图，交互式图形和小部件以及图形用户界面组合到一个文档中。该工具是通向Python，R，Julia或其他语言的高性能数值计算和数据科学的理想门户。在本书中，我们将主要使用Python语言，尽管有介绍R和Julia的用法。


In this recipe, we give an introduction to IPython and the Jupyter Notebook.
在这一部分中，我们介绍了IPython和Jupyter Notebook。

## Getting ready
准备

This chapter's introduction gives the instructions to install the Anaconda distribution, which comes with Jupyter and almost all Python libraries we will be using in this book.

本章的介绍给出了安装Anaconda发行版的说明，它附带了Jupyter以及我们将在本书中使用的几乎所有Python库。

Once Anaconda is installed, download the code from the book's website and open a Terminal in that folder. In the Terminal, type jupyter notebook. Your default web browser should open automatically and load the address http://localhost:8888 (a server that runs on your computer). You're ready to get started!

一旦安装了Anaconda，从本书的网站下载代码并在该文件夹中打开一个终端。在终端中，输入`jupyter notebook`。您的默认Web浏览器应自动打开并加载地址`http:// localhost:8888`（在您的计算机上运行的服务器）。你准备好开始了！

How to do it...

怎么做...

1. Let's create a new Jupyter notebook using an IPython kernel. We type the following command in a cell, and press *Shift + Enter* to evaluate it:

让我们使用IPython内核创建一个新的Jupyter notebook。我们在单元格中输入以下命令，然后按下Shift + Enter来执行它:

``` python
  >>> print("Hello world!")
  Hello world!
```
![](https://www.safaribooksonline.com/library/view/ipython-interactive-computing/9781785888632/graphics/B04857_01_01.jpg)

A notebook contains a linear succession of **cells** and **output** areas. A cell contains Python code, in one or multiple lines. The output of the code is shown in the corresponding output area.

一个notebook包含一系列单元格和输出区域。一个单元格包含一行或多行Python代码。代码的输出显示在相应的输出区域中。


> **TIP** 提示

> In this book, the prompt`>>>` means that you need to type everything that starts after it. The `>>>` characters themselves should not be typed.
> 在本书中，提示符>>>意味着你需要输入在它之后开始的所有内容。 >>>字符本身不应输入。

2. Now, we do a simple arithmetic operation:
2. 现在，我们做一个简单的算术运算：

```python
  >>> 2 + 2
  4
```

The result of the operation is shown in the output area. More precisely, the output area not only displays text that is printed by any command in the cell, but it also displays a text representation of the last returned object. Here, the last returned object is the result of `2 + 2`, that is, `4`.

该操作的结果显示在输出区域中。更确切地说，输出区域不仅显示由单元格中的任何命令打印的文本，而且还显示最后返回的对象的文本表示。这里，最后返回的对象是2 + 2的结果，即4。

3. In the next cell, we can recover the value of the last returned object with the _ (underscore) special variable. In practice, it might be more convenient to assign objects to named variables such as in `myresult = 2 + 2`.

在下一个单元格中，我们可以使用_（下划线）特殊变量恢复上次返回的对象的值。在实践中，将对象分配给命名变量（如myresult = 2 + 2）可能会更方便。

```python 
  >>> _ * 3
  12
```

4. IPython not only accepts Python code, but also shell commands. These commands are provided by the operating system. We first type `!` in a cell before typing the shell command. Here, assuming a Linux or macOS system, we get the list of all the notebooks in the current directory:

IPython不仅可以接受Python代码，还可以接受shell命令。这些命令由操作系统提供。我们先输入`！`在输入shell命令之前在单元格中。在这里，假设一个Linux或macOS系统，我们得到当前目录中所有notebook的列表：

```python
  >>> !ls
  my_notebook.ipynb
```

On Windows, one may replace `ls` by `dir`.

在Windows上，可以用`dir`替换`ls`。

5. IPython comes with a library of magic commands. These commands are convenient shortcuts to common actions. They all start with `%` (the percent character). We can get the list of all magic commands with `%lsmagic`:

IPython带有一个魔术命令库。这些命令是常用操作的便捷捷径。他们都以％（百分比字符）开头。我们可以用％lsmagic获得所有魔法命令的列表：

``` python
  >>> %lsmagic
  Available line magics:
  %alias  %alias_magic  %autocall  %automagic  %autosave  %bookmark  %cat  %cd  %clear  %colors  %config  %connect_info  %cp    %debug  %dhist  %dirs  %doctest_mode  %ed  %edit  %env  %gui  %hist  %history  %killbgscripts  %ldir  %less  %lf  %lk  %ll  %load  %load_ext  %loadpy  %logoff  %logon  %logstart  %logstate  %logstop  %ls  %lsmagic  %lx  %macro  %magic  %man  %matplotlib  %mkdir  %more  %mv  %notebook  %page  %pastebin  %pdb  %pdef  %pdoc  %pfile  %pinfo  %pinfo2  %popd  %pprint  %precision  %profile  %prun  %psearch  %psource  %pushd  %pwd  %pycat  %pylab  %qtconsole  %quickref  %recall  %rehashx  %reload_ext  %rep  %rerun  %reset  %reset_selective  %rm  %rmdir  %run  %save  %sc  %set_env  %store  %sx  %system  %tb  %time  %timeit  %unalias  %unload_ext  %who  %who_ls  %whos  %xdel  %xmode
  Available cell magics:
  %%!  %%HTML  %%SVG  %%bash  %%capture  %%debug  %%file  %%html  %%javascript  %%js  %%latex  %%markdown  %%perl  %%prun  %%pypy  %%python  %%python2  %%python3  %%ruby  %%script  %%sh  %%svg  %%sx  %%system  %%time  %%timeit  %%writefile

  Automagic is ON, % prefix IS NOT needed for line magics.
  Cell magics have a %% prefix; they target entire code cells.
```

6. For example, the `%%writefile` cell magic lets us create a text file. This magic command accepts a filename as an argument. All the remaining lines in the cell are directly written to this text file. Here, we create a `test.txt` file and `write Hello world!` into it:

例如，`%% writefile`单元格魔术让我们创建一个文本文件。这个神奇的命令接受一个文件名作为参数。单元格中的所有其余行都直接写入此文本文件。在这里，我们创建一个`test.txt`文件并写入`Hello world！`进去：

```python
  >>> %%writefile test.txt
     Hello world!
  Writing test.txt
  >>> # Let's check what this file contains.
      with open('test.txt', 'r') as f:
          print(f.read())
  Hello world!
```

7. As we can see in the output of `%lsmagic`, there are many magic commands in IPython. We can find more information about any command by adding `? `after it. For example, to get some help about the %run magic command, we type `%run?` as shown here:

正如我们在`％lsmagic`的输出中可以看到的那样，IPython中有许多魔术命令。我们可以通过添加找到有关任何命令的更多信息？之后。例如，要获得关于`％run magic`命令的一些帮助，我们输入`％run？`如下所示：

```python
  >>> %run?
```

![](https://www.safaribooksonline.com/library/view/ipython-interactive-computing/9781785888632/graphics/B04857_01_02.jpg)

The pager (a text area at the bottom of the screen) opens and shows the help of the `%run` magic command.

pager(屏幕底部的文本区域）打开并显示％run magic命令的帮助。

8. We covered the basics of IPython and the Notebook. Let's now turn to the rich display and interactive features of the Notebook. Until now, we have only created code cells (containing code). Jupyter supports other types of cells. In the Notebook toolbar, there is a drop-down menu to select the cell's type. The most common cell type after the code cell is the Markdown cell.

8. 我们介绍了IPython和Notebook的基础知识。现在让我们谈谈Notebook的丰富的显示和交互功能。到现在为止，我们只创建了代码单元（包含代码）。 Jupyter支持其他类型的单元格。在笔记本工具栏中，有一个下拉菜单用于选择单元格的类型。代码单元之后最常见的单元类型是Markdown单元。

Markdown cells contain rich text formatted with Markdown, a popular plain text- formatting syntax. This format supports normal text, headers, bold, italics, hypertext links, images, mathematical equations in LaTeX (a typesetting system adapted to mathematics), code, HTML elements, and other features, as shown here:

Markdown单元格包含用Markdown格式化的富文本格式，这是一种流行的纯文本格式语法。这种格式支持LaTeX（一种适用于数学的排版系统），代码，HTML元素和其他特性中的普通文本，标题，粗体，斜体，超文本链接，图像，数学公式，如下所示：


![](https://www.safaribooksonline.com/library/view/ipython-interactive-computing/9781785888632/graphics/B04857_01_03.jpg)

*Markdown cell* 

Running a Markdown cell (by pressing `Shift + Enter`, for example) displays the output, as shown in the bottom panel of the preceding screenshot.

运行Markdown单元格（例如，通过按下`Shift + Enter`键）显示输出，如前面屏幕截图的底部面板所示。


By combining code cells and Markdown cells, we create a standalone interactive document that combines computations (code), text, and graphics.

通过组合代码单元和Markdown单元，我们创建了一个独立的交互式文档，它结合了计算（代码），文本和图形。

9. The Jupyter Notebook also comes with a sophisticated display system that lets us insert rich web elements in the Notebook. Here, we show how to add HTML, Scalable Vector Graphics (SVG), and even YouTube videos in a notebook. First, we need to import some classes:

Jupyter Notebook还配备了一个复杂的显示系统，可让我们在笔记本中插入丰富的网页元素。在这里，我们展示如何在笔记本中添加HTML，可缩放矢量图形（SVG），甚至是YouTube视频。首先，我们需要导入一些类：

```python
  >>> from IPython.display import HTML, SVG, YouTubeVideo
```
10. We create an HTML table dynamically with Python, and we display it in the (HTML-based) notebook.

10. 我们使用Python动态创建HTML表格，并将其显示在（基于HTML的）笔记本中。

```python
  >>> HTML('''
     <table style="border: 2px solid black;">
      ''' +
           ''.join(['<tr>' +
                    ''.join([f'<td>{row},{col}</td>'
                             for col in range(5)]) +
                    '</tr>' for row in range(5)]) +
           '''
      </table>
     ''')
```

![](https://www.safaribooksonline.com/library/view/ipython-interactive-computing/9781785888632/graphics/B04857_01_04.jpg)

11. Similarly, we create an SVG image dynamically:

11. 同样，我们动态创建一个SVG图像：

```python
>>> SVG('''<svg width="600" height="80">''' +
        ''.join([f'''<circle
                  cx="{(30 + 3*i) * (10 - i)}"
                  cy="30"
                  r="{3. * float(i)}"
                  fill="red"
                  stroke-width="2"
                  stroke="black">
            </circle>''' for i in range(10)]) +
        '''</svg>''')
```


![](https://www.safaribooksonline.com/library/view/ipython-interactive-computing/9781785888632/graphics/B04857_01_05.jpg)

12. We display a YouTube video by giving its identifier to YoutubeVideo:

12. 我们通过将其标识符提供给YoutubeVideo来显示YouTube视频：

```python
>>> YouTubeVideo('VQBZ2MqWBZI')
```
![](https://www.safaribooksonline.com/library/view/ipython-interactive-computing/9781785888632/graphics/B04857_01_06.jpg)

## There's more 还有更多...

Notebooks are saved as structured text files (JSON format), which makes them easily shareable. Here are the contents of a simple notebook:

Notebook被保存为结构化文本文件（JSON格式），这使得它们可以轻松共享。这里是一个简单的笔记本的内容：

```json
{
 "cells": [
  {
   "cell_type": "code",
   "execution_count": 1,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Hello world!\n"
     ]
    }
   ],
   "source": [
    "print(\"Hello world!\")"
   ]
  }
 ],
 "metadata": {},
 "nbformat": 4,
 "nbformat_minor": 2
}
```

Jupyter comes with a special tool, **nbconvert**, which converts notebooks to other formats such as HTML and PDF (https://nbconvert.readthedocs.io/en/stable/).

Jupyter附带了一个特殊工具**nbconvert**，它可以将笔记本转换为其他格式，如HTML和PDF（https://nbconvert.readthedocs.io/en/stable/）。


Another online tool, **nbviewer** (http://nbviewer.jupyter.org), allows us to render a publicly-available notebook directly in the browser.

另一个在线工具**nbviewer**（http://nbviewer.jupyter.org), 允许我们直接在浏览器中呈现公开可用的notebook。

We will cover many of these possibilities in subsequent chapters, notably in Chapter 3, Mastering the Jupyter Notebook.

我们将在后面的章节中介绍其中许多可能性，特别是第3章*掌握Jupyter Notebook*。


There are other implementations of Jupyter Notebook frontends that offer different ways of interacting with the same notebook documents. JupyterLab, an IDE for interactive computing and data science, is the future of the Jupyter Notebook. It is introduced in Chapter 3, Mastering the Jupyter Notebook. **nteract** is a desktop application that lets the user open a notebook file by double-clicking on it, without using the Terminal and using a web browser. Hydrogen is a plugin of the Atom text editor that provides rich interactive capabilities when opening notebook files. Juno is a Jupyter Notebook client for iPad.

还有Jupyter Notebook前端的其他实现提供了与相同notebook文档进行交互的不同方式。 JupyterLab是一款用于交互式计算和数据科学的IDE，是Jupyter Notebook的未来。它在第3章*掌握Jupyter Notebook*介绍。 **nteract**是一个桌面应用程序，可让用户通过双击打开notebook文件，而无需使用终端并使用Web浏览器。 Hydrogen是Atom文本编辑器的插件，可在打开notebook文件时提供丰富的交互功能。 Juno是iPad的Jupyter Notebook客户端。

Here are a few references about the Notebook:

以下是关于Notebook的一些参考资料：

* Installing Jupyter, available at [http://jupyter.org/install.html](http://jupyter.org/install.html)
* Documentation of the Notebook available at [http://jupyter.readthedocs.io/en/latest/index.html](http://jupyter.readthedocs.io/en/latest/index.html)
* Security in Jupyter notebooks, at [https://jupyter-notebook.readthedocs.io/en/stable/security.html#Security-in-notebook-documents](https://jupyter-notebook.readthedocs.io/en/stable/security.html#Security-in-notebook-documents)
* User-curated gallery of interesting notebooks available at [https://github.com/jupyter/jupyter/wiki/A-gallery-of-interesting-Jupyter-Notebooks](https://github.com/jupyter/jupyter/wiki/A-gallery-of-interesting-Jupyter-Notebooks)
* JupyterLab at [https://github.com/jupyterlab/jupyterlab](https://github.com/jupyterlab/jupyterlab)
* nteract at [https://nteract.io](https://nteract.io)
* Hydrogen at https:/
* Juno at [https://juno.sh/](https://juno.sh/)

## See also 也可以看看

* The Getting started with exploratory data analysis in the Jupyter Notebook recipe
* The Introducing JupyterLab recipe in Chapter 3, Mastering the Jupyter Notebook


