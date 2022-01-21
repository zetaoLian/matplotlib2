# 第四回：文字图例尽眉目

```python
import matplotlib
import matplotlib.pyplot as plt
import numpy as np
import matplotlib.dates as mdates
import datetime
```



## 一、Figure和Axes上的文本

OO模式

```python
#二选一
fig = plt.figure(figsize=(10,3)) #设置每个图的大小
axes = fig.add_subplot(1,2)  #1行2列

fig, axes = plt.subplots(1, 2, figsize=(5, 3), tight_layout=True)

# 分别为figure和ax设置标题，注意两者的位置是不同的
fig.suptitle('bold figure suptitle', fontsize=14, fontweight='bold')
axes.set_title('axes title')

# 设置x和y轴标签
axes[0].set_xlabel('xlabel')
axes[0].set_ylabel('ylabel')

# 设置x和y轴显示范围均为0到10
axes[0].axis([0, 10, 0, 10])

# 在子图上添加文本
axes[0].text(3, 8, 'boxed italics text in data coords', style='italic',
        bbox={'facecolor': 'red', 'alpha': 0.5, 'pad': 10})

# 在画布上添加文本，一般在子图上添加文本是更常见的操作，这种方法很少	用
fig.text(0.4,0.8,'This is text for figure')

axes[0].plot([2], [1], 'o')
# 添加注解
axes[0].annotate('annotate', xy=(2, 1), xytext=(3, 4),arrowprops=dict(facecolor='black', shrink=0.05));
```

<img src="C:\Users\Williams\Desktop\matplotlib\image-20220121231957767.png" alt="image-20220121231957767" style="zoom:67%;" />

## 二、Tick上的文本

## 三、legend（图例）

```python
fig, ax = plt.subplots()
line_up, = ax.plot([1, 2, 3], label='Line 2')
line_down, = ax.plot([3, 2, 1], label='Line 1')
ax.legend(handles = [line_up, line_down], labels = ['Line Up', 'Line Down']);
```

<img src="C:\Users\Williams\Desktop\matplotlib\image-20220122004729484.png" alt="image-20220122004729484" style="zoom:67%;" />

**设置图例边框及背景**

```python
fig = plt.figure(figsize=(10,3))
axes = fig.subplots(1,3)
for i, ax in enumerate(axes):
    ax.plot([1,2,3],label=f'ax {i}')
axes[0].legend(frameon=False) #去掉图例边框
axes[1].legend(edgecolor='blue') #设置图例边框颜色
axes[2].legend(facecolor='gray'); #设置图例背景颜色,若无边框,参数无效
```

<img src="C:\Users\Williams\Desktop\matplotlib\image-20220122004818903.png" alt="image-20220122004818903" style="zoom:67%;" />

**设置图例标题**

```python
fig,ax =plt.subplots()
ax.plot([1,2,3],label='label')
ax.legend(title='legend title');
```

<img src="C:\Users\Williams\Desktop\matplotlib\image-20220122004844298.png" alt="image-20220122004844298" style="zoom:67%;" />

## 思考题

请尝试使用两种方式模仿画出下面的图表(重点是柱状图上的标签)，本文学习的text方法和matplotlib自带的柱状图标签方法bar_label

<img src="C:\Users\Williams\Desktop\matplotlib\image-20220122004900652.png" alt="image-20220122004900652" style="zoom:67%;" />

