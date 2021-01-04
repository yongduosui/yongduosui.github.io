---
layout:     post   				    # 使用的布局（不需要改）
title:      matplotlib常用函数（一） 				# 标题 
subtitle:   matplotlib常用函数 #副标题
date:       2019-12-05 				# 时间
author:     SYD 						# 作者
header-img: img/post-bg-2015.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - programming
---

```python
# 绘制曲线图
import matplotlib.pyplot as plt
x = np.linspace(0, 2, 100)  # 0-2之间取100个点（画图时取点越多越平滑）
plt.plot(x, x, label='linear')
plt.plot(x, x**2, label='quadratic')
plt.plot(x, x**3, label='cubic')
plt.xlabel('x label')
plt.ylabel('y label')
plt.title("Simple Plot")
plt.legend() # 显示图例
plt.show()
```

![](https://raw.githubusercontent.com/yongduosui/MyImageBed/master/img/20191205111529.png)

```python
import matplotlib.pyplot as plt

```

