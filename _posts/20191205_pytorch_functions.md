---
layout:     post   				    # 使用的布局（不需要改）
title:      pytorch常用函数（一） 				# 标题 
subtitle:   pytorch常用函数 #副标题
date:       2019-12-05 				# 时间
author:     SYD 						# 作者
header-img: img/post-bg-2015.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - programming
---

```python
torch.randn(2, 5) # 随机生成2行5列的矩阵
torch.item() # 将只有一个元素的tensor的值输出成一个数字
torch.max(input=matrix, dim=1) # 返回的是一个tuple（值，下标），每行中最大元素对应的下标
torch.squeese() # 去掉tenor维度为1的部分
torch.unsqueese() # 在某一维度增加维度为1 
torch.sum() # 统计tensor中为真的个数，返回值是只有一个元素的tensor
torch.item() # 将tensor的元素取出来，是个值
torch.size() # 返回的是tensor的大小，是一个tensor.Size类型
torch.size(n) # 返回的是tensor的大小，是一个具体数字，n表示第n个维度大小

Data.DataLoader(dataset=train_data, batch_size=BATCH_SIZE, shuffle=True) # 将数据集转化成batch


```

