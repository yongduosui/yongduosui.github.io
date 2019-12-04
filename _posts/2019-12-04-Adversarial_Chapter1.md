---
layout:     post   				    # 使用的布局（不需要改）
title:      对抗攻击学习（一） 				# 标题 
subtitle:   定义与基本概念 #副标题
date:       2019-12-04 				# 时间
author:     SYD 						# 作者
header-img: img/post-bg-2015.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - Adversarial
---
# 对抗攻击学习（一）定义和基本概念

## 1. 对抗样本

（1）对抗样本的存在表明模型倾向于依赖不可靠的特征来最大限度的提高性能，如果受到干扰，可能会导致错误分类。  （2）对抗性样本的非正式定义可以认为是，输入被以一种人类难以察觉的方式修改后，机器学习系统会将它们错误分类，而没有修改的原始输入却能被正确分类。

## 2. 分类

（1）有目标攻击，无目标攻击   
（2）黑盒攻击，白盒攻击

## 3 攻击原理

（1）神经网络正常训练：输入的图像x固定，训练网络参数θ，使得Loss最小  
（2）无目标攻击：网络参数θ固定，找到x‘使得Loss最大  
（3）有目标攻击：网络参数θ固定，找到x‘使得Loss最大，同时使得与虚假标签的差异更小  
（4）限制条件：使得修改之后的图像与原始图像差异不太大

## 4. 限制条件

（1）L2范数  
（2）无穷范数  
（3）原理理解：很大的L2范数可以对应很小的无穷范数或者很大的无穷范数，因此无穷范数效果更好（可以不被发现的同时修改更多信息）

<img src="https://raw.githubusercontent.com/yongduosui/MyImageBed/master/img/20191204102134.png" style="zoom:80%;" />

## 5. 存在对抗样本的原因

虽然高维向量X0在某些随机的方向上变化，对应类别的分布如下图所示

<img src="https://raw.githubusercontent.com/yongduosui/MyImageBed/master/img/20191204102354.png" style="zoom:80%;" />

但是可能在某些特定的方向上范围非常小，因此很脆弱，如下图所示。

<img src="https://raw.githubusercontent.com/yongduosui/MyImageBed/master/img/20191204102408.png" style="zoom:80%;" />

## 6. 黑盒攻击方法

（1）已知条件：拥有目标网络的训练样本，或者利用这个目标网络，收集一些输入输出的pairs  
（2）方法：利用以上收集的训练数据来训练一个proxy网络，进行白盒攻击即可。  
（3）有效性：下图展示的就是利用黑盒攻击方法来攻击一些经典的CNN网络取得的效果。

<img src="https://raw.githubusercontent.com/yongduosui/MyImageBed/master/img/20191204103543.png" style="zoom:67%;" />

## 7. 防御

（1）对抗攻击不是因为overfitting，因此通过正则化、dropout、以及模型集成无效，attack是可以跨model的。  
（2）分类：主动防御和被动防御

## 8. 被动防御

（1）filter：比如平滑化的滤波器。feature squeeze（好多个filter，多个支路结果不一样说明被攻击），randomization at inference phase（加padding）  
（2）原理：只在某个方向上的某个特定信号才可以让攻击成功，平滑后这个信号改变了，那攻击就失效了，但是这种滤波并不会伤害到原始图像，因此防御成功。  
（3）缺点：filter（想像成是一个layer）的方法以及缩放的方法如果被泄露出去攻击也有可能是成功的。

## 9. 主动防御

（1）思想：找出漏洞，补起来，循环T次  
（2）方法：  

1. 在每一个大循环中，利用某个攻击算法A来找到N个对抗样本
2. 对这N个对抗样本进行打标签（类似数据增强）
3. 重新对他们进行训练（漏洞修补）

（3）为什么要循环T次： 由于找到漏洞以后，重新训练后可能会产生新的漏洞。  
（4）缺点： 如果利用A方法来找漏洞，可以防御A方法，但是对于B方法无法进行有效的防御。  
（5）算法如下图：  

<img src="https://raw.githubusercontent.com/yongduosui/MyImageBed/master/img/20191204104002.png" style="zoom:80%;" />
