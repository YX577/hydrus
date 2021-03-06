# Google Cloud 

google为了推广自己的云服务，有google cloud + colab + tensorflow + google earth engine的套装操作。另外，如果自己的数据量不是特别大，那么拿到这个平台上试运行也会死一个不错的选择。本文主要参考了：[Google Colab Free GPU Tutorial](https://medium.com/deep-learning-turkey/google-colab-free-gpu-tutorial-e113627b9f5d)，[苦逼学生党的Google Colab使用心得](https://zhuanlan.zhihu.com/p/54389036),[3 个相见恨晚的 Google Colaboratory 奇技淫巧！](https://zhuanlan.zhihu.com/p/56581879)等资料，以了解这套工具的一些基本内容。

## Introduction to Colab

直接抄一段：
Google Colab is a free cloud service and now it supports free GPU!
You can;
improve your Python programming language coding skills.
develop deep learning applications using popular libraries such as Keras, TensorFlow, PyTorch, and OpenCV.

简而言之，就是一个带GPU的云端开发环境。

因为Cloab是在Google drive上工作的，因此首先，在Google drive上创建一个文件夹来让其使用，比如我创建了一个Colab Notebooks文件夹。

在该文件夹下，右键，选择“更多”－“关联更多应用”，搜索colab，并关联。如果关联上了还看不到，可参考以下引用的评论中的表述：

```
何笑鸥修改时间：2019年9月5日
看到有小伙伴即使关联本应用，在谷歌云端硬盘的新建目录下仍然看不到它。我的办法是：
1. 转到页面：https://colab.research.google.com/notebooks/welcome.ipynb
2. 单击菜单栏偏下方的“复制到云端硬盘”
3. 进入自己的谷歌云端硬盘(drive.google.com)，可以看到出现一个黄色的文件夹，叫做Colab Notebooks，双击打开，里面有文件名为'“欢迎使用Colaboratory”的副本‘
4. 这时候再单击云端硬盘的“新建”-“更多”，就能看到“Google Colaboratory”项了。
```

如果还不行，就用新文件夹，留一个空白的colab文件用来复制粘贴即可。


### Running Python Codes

其使用方法和jupyter notebook是很像的。在左上角选择“+代码”，“+文本”可以分别添加代码和文本。注意colab貌似对中文的支持并不友好，所以尽量使用英文。

简单的代码可以直接运行即可。这里重点说下关于导入第三方模块和从github clone代码等操作。

### 选择GPU

然后选择硬件，直接 Edit（修改） > Notebook settings（笔记本设置） 或 Runtime>Change runtime type，然后选择GPU作为Hardware accelerator（硬件加速器）即可。

### 安装库

因为Tensorflow本身就是Google的，所以不用安装，可以直接用。直接使用tensorflow官方文档给的[初学者教程](https://www.tensorflow.org/tutorials/quickstart/beginner)即可。

因此,这里以pytorch的安装为例,不过colab上也有torch已经安装了.不过依然可以自己安装,这部分参考了:[使用Google Colab训练PyTorch神经网络](https://tiangexiao.github.io/2019/01/06/%E4%BD%BF%E7%94%A8Google-Colab%E8%AE%AD%E7%BB%83PyTorch%E7%A5%9E%E7%BB%8F%E7%BD%91%E7%BB%9C/),可以查看云端的系统/python版本/cuda版本,然后再根据pytorch官网上的推荐进行安装,可以发现,以 !开头的命令是可以执行操作系统的指令,以 %开头的命令表示魔法指令.colab没有原装conda,不过有pip和apt包管理器.

### 上传并使用数据文件

可以使用以下命令调用笔记本中的文件选择器：

``` python
from google.colab import files
uploaded = files.upload()
```

运行之后，我们就会发现单元 cell 下出现“选择文件”按钮.

也可以直接传入谷歌云盘。

在指定之前先用!ls命令查看一下云端自动分配的默认文件目录，云端默认的文件根目录是datalab.

```
! ls
```

详细的操作可以参考[官方文档](https://colab.research.google.com/notebooks/welcome.ipynb)。

### Clone github文件到Colab

clone文件到colab中直接使用!git clone命令即可，不过colab上运行的都是jupyter notebook文件，因此，对于工程性质的python项目，需要采用另外的方式。其实，Colab就是一个云端运行机器学习算法的jupyter文件的平台。

### Debug in Colab

在colab中的debug和在jupyter notebook中的类似，

## 使用Google Cloud Platform

虽然colab很好,但是还是在一个电脑上操作可能更舒服一些,这里从GCP的安装开始,这部分主要参考了:[薅羊毛，Google Cloud免费使用一年以及详细教程说明](https://www.luofan.net/post/112.html).

先完成第一个步骤－－试用GCP。然后创建一个项目。

接下来可以参考官方的[tensorflow文档](https://cloud.google.com/ml-engine/docs/tensorflow/getting-started-training-prediction?hl=zh-cn)，确保GCP已启动结算功能，并启用AIPlatform。

进入项目，首先，进入实例创建页面，点击快速入门简介，边看边操作，按照官方的提示要求做即可。

接下来参考[视频](https://www.bilibili.com/video/av31141381/)快速搭建深度学习环境，首先要升级下账号（免费的），才能在“IAM和管理”界面修改配额（quotas）。然后参考视频介绍即可。申请GPU配额的话，需要等两天才有回复，所以就先耐心等待了。可以通过配额页面的当前使用量看自己的机器配额情况。

在等待GPU申请的过程中，可以下载安装Google Cloud SDK来使用，这是一个用于管理托管在GCP上的资源和应用的工具。

## Google Earth Engine介绍

这部分主要参考官网[指南](https://developers.google.com/earth-engine)。根据视频介绍，google earth engine（以下简称GEE）提供了对空间大数据访问和分析的API，其核心组件主要包括Datasets、Computer Power、APIs和Code Editor。

其包括的数据主要有：Landsat & Sentinel2（10-30m， 14d）， MODIS（250m daily），Sentinel1（Radar）， Terrain & Land Cover， 以及Weather & Climate（NOAA NCEP， OMI， ……），API可以做的事情包括：monitoring land cover changing、detecting surface water等。

API的主要使用方式是：通过GEE的[网站](https://code.earthengine.google.com/)（一个在线的Code Editor），可以利用JavaScript代码来完成api的调用。网站有四个panel组成，左上角是sample代码和docs等，中间的是写代码的地方，右边是控制台，下方是可以展示计算结果的地图显示器。API也有python版本，不过在这个网页上，只能执行JavaScript脚本。

官网给出了一个GEE的演讲，可以对GEE有更进一步的认识。演讲中的主要内容，这里简单记录下：

首先，对卫星数据的情况做了简单介绍，介绍了GEE如何将过去的数据数字化处理并为科研提供价值。GEE的数据集的mission就是组织世界上所有地球科学数据，使得其更容易获取和使用，因此组开发了基于web的访问接口，可以使用JavaScript访问，也可以使用python。

然后介绍了一些例子，比如forest cover的相关论文，其提供了新的数据，因此引用也很高，再比如global surface water的文献及数据等。还有一些应用，比如在东南亚的科研工作者使用GEE，比如climate engine用GEE的数据分析全球温度异常的地区等。

接着介绍了vector data的情况，数据除了map数据，还有很多vector数据，GEE平台允许上传table数据，现在GEE可以直接上传shapefile文件，直接加载到GEE中，后续可能支持其他数据格式的数据的添加。

接下来，对Cloud Platform + Earth Engine做了一些介绍，举了一个例子，Cloud Data Program，通过GCP来免费访问Landsat和Sentinel-2的数据，包括完整的USGS Landsat 4/5/7/8的400万景的图像，1.3pb的大小，还有完整的Sentinel-2,97万张图片超过430tb数据量，这些数据还在每日更新中。 GCP和GEE的整合包括用Cloud Storage和GEE做integration，还有GEE和其他GCE（通过computer engine来调用GEE）等的整合。还有本文一开始提到的GEE+GCP+Tensorflow。

接下来，介绍一些GEE的基本入门操作，主要是管饭文档的第一大节的内容，更详细地内容参考后续章节。

### 快速上手

快速使用JavaScript API来访问GEE。

关于官方文档：文档结构是按照data type组织的。左边导航栏下的结构就是按照Image、ImageCollection等data types组织的。还有一些其他比如machine learning等的说明，这里先不展开。

先看Code Editor环节。
按照官网实操一下，很容易理解。这里值得一提的是脚本可以复用的，通过exports可以让某个function对其他脚本可用。


接下来是一些基本用法。

首先简单记录下EE的数据结构和算法。

EE中最基础的两个图像数据结构是Image和Feature，分别对应栅格数据和向量数据类型。栅格数据Image由bands和属性字典构成，Features则由Geometry数据和属性字典构成。images组成的栈由FeatureCollection处理。其他数据结构还有Dictionary, List, Array, Date, Number and String等。这里简单补充下一些相关的GEE中的基本知识：

- Javascript几种基本的数据结构：String,Number,List,Object(字典数据类型)和Function.
- Clent vs. Server:EE的objects和Javascript的objects要区分开，比如一个JavaScript的string要送到EE服务端计算，需要将其包入一个EE的string对象中，包含其的容器就是proxy object，不过print函数还是可以直接给出其内容的。在EE中，尽量面向server端写程序，因为client是不知道server段的objects的。所有的ee.Thing初始化的都是server对象，所有ee.Thing的method都是server 函数，没有ee的就是client的。client的变server的需要容器。尽量避免混合使用client和server的对象和方法。

有几种运行EE API的函数的方法：

- 调用对象的方法
- 调用算法
- 调用Code Editor内的函数
- 定义新的函数


GEE一个重要的内容就是可以很容易的导入数据，关于数据部分的内容，后续“科研数据”章节有补充。这里只介绍工具配置方面的内容。导入的数据一般是数据集，即ImageCollection的数据结构，为了按照自己的目标使用，还需要filer（by space and time）以及sort等。对于图像的处理，一般的数学运算都是使用Image的方法，包括：band recombinations (spectral indices), image differencing or mathematical operations such as multiplication by a constant.在运算中，会常用到map和reduce计算，和python中的语法类似，在GEE中，map操作可以用来代替for循环，reduce可以实现对多图像共同操作。

最后，每个ee.Image都有一个值和一个mask（取值范围0到1），被masked的pixels值可视为0。使用mask可以控制哪些pixels参与分析计算。

### Python+GEE

使用Python访问GEE，相关的python的installation可以在本地进行，也可以在云端以jupyter notebook的形式，两者各有利弊，简单来说，本地的部署访问本地文件比较方便，执行脚本等也比较方便，不足是创建环境比较麻烦一些；colab上比较好的地方是不用装任何软件，文档实时在云端，不足是访问本地文件比较麻烦，并且因为colab是在虚拟机上运行，每次运行后会清空结果，所以每次启动程序时都需要重新安装一些必要的软件包，比如这里每次一个session都要重新安装GEE的api，并获取credentials。按照官网给的顺序，先在colab上运行，这样也比较容易上手。

前面已经试用过colab了，因此这里直接安装API并获取credentials。官网有相关的colab程序，按步骤进行即可。

在本地安装的话，只要安装了anaconda即可用conda来安装GEE API。安装按照官网说明从api的安装开始即可。然后每次重新使用GEE时，用conda activate ee激活ee环境即可。

以上就是GEE的简单介绍，更多教材可以参考：[Earth Engine resources for higher education](https://developers.google.com/earth-engine/edu)，有中文教材可学习。

GEE并不是一个面向程序员的工具，掌握GEE更多需要的是GIS以及使用ArcGIS的思维方式，这样才能更好地使用这一强大的工具。

## GEE+Tensorflow

最后一小节，简单记录下GEE和机器学习的结合。