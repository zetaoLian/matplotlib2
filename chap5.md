# 第五回：样式色彩秀芳华

```python
import matplotlib as mpl
import matplotlib.pyplot as plt
import numpy as np
```

## 一、matplotlib的绘图样式（style）

```python
plt.style.use('ggplot')
plt.plot([1,2,3,4],[2,3,4,5]);
```

<img src="C:\Users\Williams\Desktop\matplotlib\image-20220124005134938.png" alt="image-20220124005134938" style="zoom: 50%;" />

### 1.matplotlib预先定义样式

### 2.用户自定义stylesheet

在任意路径下创建一个后缀名为mplstyle的样式清单，编辑文件添加以下样式内容

> axes.titlesize : 24
> axes.labelsize : 20
> lines.linewidth : 3
> lines.markersize : 10
> xtick.labelsize : 16
> ytick.labelsize : 16

引用自定义stylesheet后观察图表变化。

```python
plt.style.use('file/presentation.mplstyle')
plt.plot([1,2,3,4],[2,3,4,5]);
```

<img src="C:\Users\Williams\Desktop\matplotlib\image-20220124005431420.png" alt="image-20220124005431420" style="zoom: 50%;" />

### 3.设置rcparams

通过rc来改变默认的样式中的某一部分

```python
plt.style.use('default') # 恢复到默认样式
mpl.rc('lines', linewidth=4, linestyle='-.')
plt.plot([1,2,3,4],[2,3,4,5]);
```

<img src="C:\Users\Williams\Desktop\matplotlib\image-20220124005635017.png" alt="image-20220124005635017" style="zoom:50%;" />

## 二、matplotlib的色彩设置（color）

从可视化编码的角度对颜色进行分析，可以将颜色分为`色相、亮度和饱和度`三个视觉通道。通常来说：
`色相`： 没有明显的顺序性、一般不用来表达数据量的高低，而是用来表达数据列的类别。
`明度和饱和度`： 在视觉上很容易区分出优先级的高低、被用作表达顺序或者表达数据量视觉通道。

### 1.RGB或RGBA

```
# 颜色用[0,1]之间的浮点数表示，四个分量按顺序分别为(red, green, blue, alpha)，其中alpha透明度可省略
plt.plot([1,2,3],[4,5,6],color=(0.1, 0.2, 0.5))
plt.plot([4,5,6],[1,2,3],color=(0.1, 0.2, 0.5, 0.5));
```

<img src="C:\Users\Williams\Desktop\matplotlib\image-20220124005745667.png" alt="image-20220124005745667" style="zoom:50%;" />

### 3.灰度色阶

<img src="C:\Users\Williams\Desktop\matplotlib\image-20220124005917671.png" alt="image-20220124005917671" style="zoom:50%;" />

```
# 当只有一个位于[0,1]的值时，表示灰度色阶
plt.plot([1,2,3],[4,5,6],color='0.5');
```

### 4.单字符基本颜色

```
# matplotlib有八个基本颜色，可以用单字符串来表示，分别是'b', 'g', 'r', 'c', 'm', 'y', 'k', 'w'，对应的是blue, green, red, cyan, magenta, yellow, black, and white的英文缩写
plt.plot([1,2,3],[4,5,6],color='m');
```

<img src="C:\Users\Williams\Desktop\matplotlib\image-20220124005957646.png" alt="image-20220124005957646" style="zoom:50%;" />

### 5.颜色名称

```
# matplotlib提供了颜色对照表，可供查询颜色对应的名称
plt.plot([1,2,3],[4,5,6],color='tan');
```

<img src="C:\Users\Williams\Desktop\matplotlib\image-20220124010010088.png" alt="image-20220124010010088" style="zoom:50%;" />

### 6.使用colormap设置一组颜色

```
x = np.random.randn(50)
y = np.random.randn(50)
plt.scatter(x,y,c=x,cmap='RdPu');
```

<img src="C:\Users\Williams\Desktop\matplotlib\image-20220124010109024.png" alt="image-20220124010109024" style="zoom:50%;" />

在matplotlib中，colormap共有五种类型:

- 顺序（Sequential）。通常使用单一色调，逐渐改变亮度和颜色渐渐增加，用于表示有顺序的信息
- 发散（Diverging）。改变两种不同颜色的亮度和饱和度，这些颜色在中间以不饱和的颜色相遇;当绘制的信息具有关键中间值（例如地形）或数据偏离零时，应使用此值。
- 循环（Cyclic）。改变两种不同颜色的亮度，在中间和开始/结束时以不饱和的颜色相遇。用于在端点处环绕的值，例如相角，风向或一天中的时间。
- 定性（Qualitative）。常是杂色，用来表示没有排序或关系的信息。
- 杂色（Miscellaneous）。一些在特定场景使用的杂色组合，如彩虹，海洋，地形等。

在以下官网页面可以查询上述五种colormap的字符串表示和颜色图的对应关系
https://matplotlib.org/stable/tutorials/colors/colormaps.html

## 思考题

- 学习如何自定义colormap，并将其应用到任意一个数据集中，绘制一幅图像，注意colormap的类型要和数据集的特性相匹配，并做简单解释

暂无