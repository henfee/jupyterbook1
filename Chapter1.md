
## 第一章 使用Jupyter和IPython进行交互式计算简介
---
在本章中，我们将介绍以下主题：

* 介绍IPython和Jupyter Notebook
* 开始使用Jupyter Notebook进行探索性数据分析
* 在NumPy中引入多维数组进行快速数组计算
* 使用自定义魔术命令创建IPython扩展
* 掌握IPython的配置系统
* 为Jupyter创建一个简单的内核

## 简介

在这篇介绍中，我们将对Python，IPython，Jupyter和科学Python生态系统进行全面的介绍。

### 什么是Python？

Python是一种高级的，开源的，通用的编程语言，最初由Guido van Rossum在20世纪80年代后期构想出来（这个名字的灵感来自英国喜剧巨星Python的飞行马戏团）。这种易于使用的语言通常被系统管理员用作[粘合剂语言][1]（glue language），将各种系统组件连接在一起。它也是大规模软件开发的强大语言。此外，Python还带有一个非常丰富的标准库([自带电池哲学][2]:the batteries included  philosopy），涵盖了字符串处理，网络协议，操作系统接口以及许多其他领域。

在过去的二十年中，Python越来越多地用于科学计算和数据分析。其他竞争平台包括商业软件，如MATLAB，Maple，Mathematica，Excel，SPSS，SAS，和其他等，竞争的开源平台包括Julia，R，Octave和Scilab。这些工具专门用于科学计算，而Python是一种通用编程语言，最初并不是为科学计算而设计的。

然而，一个广泛的工具生态系统已经被开发出来以便将Python带入这些其他科学计算系统的水平。今天，Python的主要优势以及它如此受欢迎的主要原因之一是，它将科学计算功能带给了一个在许多研究领域和行业中使用的通用语言。这使得从研究到生产的过渡变得更容易。

### 什么是IPython？

**IPython**是一个Python库，最初旨在改进Python提供的默认交互式控制台，并使其对科学家友好。在2011年，IPython首次发布10年后，**IPython Notebook**被引入。这个基于Web的IPython界面将代码，文本，数学表达式，内联图，交互式图形，小部件，图形界面和其他丰富的媒体结合在一个独立的可共享的Web文档中。该平台为交互式科学计算和数据分析提供了理想的门户。 IPython已经成为研究人员，工程师，数据科学家，教师及其学生必不可少的组成部分。

### 什么是Jupyter？

几年后，IPython在科学界和工程界获得了不可思议的盛誉。IPython Notebook开始支持越来越多的Python以外的编程语言。 2014年，IPython开发者宣布了**Jupyter**项目，该项目旨在改进Notebook的实现并通过设计使其与语言无关。该项目的名称反映了Notebook支持的三种主要科学计算语言：Julia，Python和R的重要意义。

今天，Jupyter本身就是一个生态系统，它可以理解为多种可供选择的Notebook界面（JupyterLab，nteract，Hydrogen等）、交互式可视化库以及与Notebook兼容的创作工具。 Jupyter有自己的会议JupyterCon。该项目得到了几家公司以及Alfred P. Sloan基金会和Gordon和Betty Moore基金会的资助。

### 什么是SciPy生态系统？

SciPy是用于科学计算的Python软件包的名称，但它也更一般地指向为Python带来科学计算功能而开发的所有Python工具的集合。

在20世纪90年代后期，Travis Oliphant和其他人开始构建高效的工具来处理Python中的数值数据：Numeric，Numarray，最后是**NumPy**。实现了许多数值计算算法的**SciPy**也是在NumPy之上创建的。在二十一世纪初，John Hunter创建了**Matplotlib**以将科学图形带入Python。同时，Fernando Perez创建了**IPython**，以提高Python的交互性和生产力。在二十世纪二十年代末，Wes McKinney为数字表格和时间序列的操作和分析创建了**pandas**。从那时起，数百名工程师和研究人员合作开发该平台，使SciPy成为领先的科学计算和数据科学开源平台之一。


> **备注**

> 许多SciPy工具都得到了NumFOCUS的支持，NumFOCUS是一个非营利组织，被创建为促进生态系统可持续发展的合法结构。 NumFOCUS由几家大公司支持，包括微软，IBM和英特尔。


SciPy也有自己的会议：SciPy（在美国）和EuroSciPy（在欧洲）（参见[https://conference.sci](https://conference.sci)）。

### SciPy生态系统有哪些新功能？

自2014年出版本书第一版以来，SciPy生态系统的一些主要变化是什么？我们在这里给出一个简短的选择。

在编写本文时，IPython的最后一个版本是IPython 6.0，它于2017年4月发布。它是IPython的第一个版本，它不再与Python 2兼容。此决定允许开发人员使内部代码更简单，并使其更好使用该语言的新功能。

**IPython**现在有一个基于Web的终端界面，可以和notebook一起使用。键盘快捷键可以直接从Notebook界面进行编辑。可以选择多个单元并在笔记本之间复制/粘贴。Notebook中有一个新的重新启动和全部运行按钮以及一个查找和替换选项。有关更多详细信息，请参见[http://ipython.readthedocs.io/en/stable/whatsnew/version6.html](http://ipython.readthedocs.io/en/stable/whatsnew/version6.html)。

**NumPy**，最新版本1.13于2017年6月发布，现在支持矩阵之间的@ matrix 乘法运算符（它以前可通过np.dot()函数访问）。诸如a+b+c之类的操作使用较少的内存，并且在某些系统上更快（临时省略）。新的np.block()函数允许定义块矩阵。新的np.stack()函数沿着一个新的轴加入一系列数组。有关更多详细信息，请参阅[https://docs.scipy.org/doc/numpy-1.13.0/release.html](https://docs.scipy.org/doc/numpy-1.13.0/release.html)。

**SciPy** 1.0于2017年10月发布。对于开发者来说，1.0版本意味着库经过16年的发展已经达到了一定的稳定性和成熟度。有关更多详细信息，请参见[https://docs.scipy.org/doc/scipy/reference/release.html](https://docs.scipy.org/doc/scipy/reference/release.html)。

**Matplotlib**，其中版本2.1于2017年10月发布，具有改进的样式和更好的默认颜色调色板，其中*viridis* 颜色地图代替*jet*。有关更多详细信息，请参阅[https://github.com/matplotlib/matplotlib/releases](https://github.com/matplotlib/matplotlib/releases)。

**pandas** 0.21于2017年10月发布。pandas现在支持分类数据。在过去的几年中，一些实现方法已经弃用，比如.ix语法和Panels（可能通过xarray库进行代替）。有关更多详细信息，请参阅[https://pandas.pydata.org/pandas-docs/stable/release.html](https://pandas.pydata.org/pandas-docs/stable/release.html)。

### 如何安装Python

在本书中，我们使用**Anaconda**发行版，该发行版在[https://www.anaconda.com/download/](https://www.anaconda.com/download/)上提供。 Anaconda适用于Linux，macOS和Windows。在编写本文时，您应该使用最新的64位版本的Python（在编写本文时为3.6）安装最新版本的Anaconda（5.0.1）。 Python 2.7是一个旧版本，到2020年将不会得到官方支持。

Anaconda提供了Python，IPython，Jupyter，NumPy，SciPy，pandas，Matplotlib以及我们将在本书中使用的几乎所有其他科学软件包。所有软件包的列表可在[https://docs.anaconda.com/anaconda/packages/pkg-docs](https://docs.anaconda.com/anaconda/packages/pkg-docs)上找到。

  >
  > **备注**

  > Miniconda是Anaconda的一个轻量版本，只有Python和一些其他基本软件包。您只能使用Anaconda的conda软件包管理器逐一安装所需的软件包。
  >

本书不会涵盖安装科学Python发行版的各种其他方式。

Anaconda网站应该为您提供在系统上安装Anaconda的所有说明。要安装新软件包，您可以使用Anaconda附带的conda软件包管理器。例如，要安装```ipyparallel```软件包（默认情况下当前未在Anaconda中安装），请在系统shell中键入```conda install ipyparallel```。

  >
  > **提示**

  > 第2章“交互式计算中的最佳实践”的Unix shell部分的基础知识中给出了系统shell的简短介绍。
  >


另一种安装软件包的方式是使用conda-forge，可在[https://conda-forge.org/](https://conda-forge.org/)上找到。这是一个社区驱动的工作以便在Github上自动构建最新版本的软件包，并使它们可以与conda一起使用。如果一个软件包不能用```conda install somepackage```来安装，如果软件包被conda-forge支持的话可以使用```conda install --channel conda-forge somepackage```来代替，。

  >
  > **提示**

  > GitHub是一个商业服务，为软件存储库提供免费和付费托管。它是开源协作开发最流行的平台之一。
  >


**pip**是Python系统管理工具。与conda比较，pip适用于任何Python发行版，而不仅限于Anaconda。可通过pip安装的软件包存储在[https://pypi.python.org/pypi](https://pypi.python.org/pypi)上的Python软件包索引（PyPI，Python Package Index）中。

几乎所有可用于conda的Python软件包都可用pip提供，但相反的情况并非如此。实际上，如果一个软件包在conda或conda-forge中不可用，它应该可以通过```pip install somepackage```来使用。 conda软件包通常包含为最常见的平台编译的二进制文件，而pip软件包并不一定是这种情况。 pip包可能包含必须在本地编译的源代码（这需要安装和配置兼容的编译器），但它们也可能包含已编译的二进制文件。

### 参考

这里有几个参考文献：

* [Python网站](https://www.python.org)

* [维基百科上的Python](https://en.wikipedia.org/wiki/Python_%28programming_language%29)

* [Python的标准库](https://docs.python.org/3/library/)

* [Guido van Rossum谈Python的诞生](http://www.artima.com/intv/pythonP.html)
* [科学Python的历史](http://fr.slideshare.net/shoheihido/sci-pyhistory)

* [Jupyter Notebook的历史](http://blog.fperez.org/2012/01/ipython-notebook-historical.html)

* [JupyterCon](https://conferences.oreilly.com/jupyter/jup-ny)

以下是关于科学Python的一些资源：

* [Introduction to Python for Computational Science and Engineering](https://github.com/fangohr/introduction-to-python-for-computational-science-and-engineering)
* [Statistical Computing and Computation](http://people.duke.edu/~ccc14/sta-663-2017/)
* [SciPy 2017视频](https://www.youtube.com/playlist?list=PLYx7XA2nY)


---
[1]: glue language，胶水语言，粘合剂语言

[2]: the batteries included  philosopy,自带电池哲学



