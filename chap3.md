# 第三回：布局格式定方圆

## 一、子图

### 1. 使用 `plt.subplots` 绘制均匀状态下的子图

#### a.多个图有共同特点的时候  

```python
fig, axs = plt.subplots(2, 5, figsize=(10, 4), sharex=True, sharey=True)
```

第一个数字为行，第二个为列，不传入时默认值都为1

`figsize` 参数可以指定整个画布的大小

`sharex` 和 `sharey` 分别表示是否共享横轴和纵轴刻度

`tight_layout` 函数可以调整子图的相对大小使字符不会重叠

axs 是一个二维数组 

```python
fig, axs = plt.subplots(2, 5, figsize=(10, 4), sharex=True, sharey=True)
fig.suptitle('样例1', size=20)
for i in range(2):
    for j in range(5):
        axs[i][j].scatter(np.random.randn(10), np.random.randn(10))
        axs[i][j].set_title('第%d行，第%d列'%(i+1,j+1))
        axs[i][j].set_xlim(-5,5)
        axs[i][j].set_ylim(-5,5)
        if i==1: axs[i][j].set_xlabel('横坐标')
        if j==0: axs[i][j].set_ylabel('纵坐标')
fig.tight_layout()
```

<img src="C:\Users\Williams\Desktop\matplotlib\image-20220119004238880.png" alt="image-20220119004238880" style="zoom:67%;" />

#### b.单个图处理时

调用`subplot`时一般需要传入三位数字，分别代表总行数，总列数，当前子图的index

```python
plt.figure()
# 子图1
plt.subplot(2,2,1) 
plt.plot([1,2], 'r')
# 子图2
plt.subplot(2,2,2)
plt.plot([1,2], 'b')
#子图3
plt.subplot(224)  # 当三位数都小于10时，可以省略中间的逗号，这行命令等价于plt.subplot(2,2,4) 
plt.plot([1,2], 'g');
```

<img src="C:\Users\Williams\Desktop\matplotlib\image-20220119004342863.png" alt="image-20220119004342863" style="zoom:67%;" />

#### c.极坐标图

```python
N = 150
r = 2 * np.random.rand(N)
theta = 2 * np.pi * np.random.rand(N)
area = 200 * r**2
colors = theta


plt.subplot(projection='polar')
plt.scatter(theta, r, c=colors, s=area, cmap='hsv', alpha=0.75); # 角度 半径 颜色 面积
```

<img src="C:\Users\Williams\Desktop\matplotlib\image-20220119005149483.png" alt="image-20220119005149483" style="zoom:67%;" />

### 2. 使用 `GridSpec` 绘制非均匀子图

利用 `add_gridspec` 可以指定相对宽度比例 `width_ratios` 和相对高度比例参数 `height_ratios`

```python
fig = plt.figure(figsize=(10, 4))
spec = fig.add_gridspec(nrows=2, ncols=5, width_ratios=[1,2,3,4,5], height_ratios=[1,3])
fig.suptitle('样例2', size=20)
for i in range(2):
    for j in range(5):
        ax = fig.add_subplot(spec[i, j])
        ax.scatter(np.random.randn(10), np.random.randn(10))
        ax.set_title('第%d行，第%d列'%(i+1,j+1))
        if i==1: ax.set_xlabel('横坐标')
        if j==0: ax.set_ylabel('纵坐标')
fig.tight_layout()
```

![image-20220119012637120](C:\Users\Williams\Desktop\matplotlib\image-20220119012637120.png)

### 思考题

- 画出数据的散点图和边际分布

用 `np.random.randn(2, 150)` 生成一组二维数据，使用两种非均匀子图的分割方法，做出该数据对应的散点图和边际分布图

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from matplotlib.gridspec import GridSpec
plt.rcParams['font.sans-serif'] = ['SimHei']   #用来正常显示中文标签
plt.rcParams['axes.unicode_minus'] = False   #用来正常显示负号



data=np.random.randn(2,150)
x=data[0]
y=data[1]
# fig, ax = plt.subplots(figsize=(7,7))
gs = GridSpec(5,5)
fig = plt.figure()
ax_joint = fig.add_subplot(gs[1:5,0:4])
ax_marg_x = fig.add_subplot(gs[0,0:4])
ax_marg_y = fig.add_subplot(gs[1:5,4])

ax_joint.grid(True)
ax_joint.scatter(x,y)
ax_joint.set_xlim((-3, 3))
ax_joint.set_ylim((-3, 3))
ax_joint.set_xlabel('my_data_x')
ax_joint.set_ylabel('my_data_y')

ax_marg_x.hist(x)
ax_marg_y.hist(y,orientation="horizontal")
plt.show()
```

![image-20220119012714316](C:\Users\Williams\Desktop\matplotlib\image-20220119012714316.png)
