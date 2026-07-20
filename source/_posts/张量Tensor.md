---
title: 张量Tensor
author: MrKeanu
categories:
  - Incessant Coding-编程不辍
  - Deep Learning-深度学习
index_img: /image/index/pytorch.png
banner_img: /image/bg/flower_in_sky.jpg
banner_img_height: 70
banner_mask_alpha: 0.3
date: 2023-10-13 01:32:11
excerpt: Pytorch的基本数据结构——张量
tags: [Pytorch, Deep Learning]
archive: false
---
# 一、张量Tensor


## （一）简介

Tensor张量是一个多维数组，可以是标量、向量、矩阵或更高维度的数据结构。Tensor数据类型可类比于Numpy中的Numpy数组，除了在图像数据编码上存在差异外，最大的区别就是Numpy数组存储于CPU内存，而Pytorch为了使用GPU对训练进行加速使Tensor支持内存存储和显存存储。并且Pytorch为Tensor提供了更多的属性和功能，比如计算图和自动求导。因此使用Pytorch框架所有的与深度学习相关的计算，尤其是模型的训练，其数据都应使用Tensor类型。



## （二）初始化

#### 张量创建

|**方法**|**说明**|**示例代码**|
|:----|:----|:----|
|torch.tensor(data)|从 Python 列表或 NumPy 数组创建张量。|x = torch.tensor([[1, 2], [3, 4]])|
|torch.zeros(size)|创建一个全为零的张量。|x = torch.zeros((2, 3))|
|torch.ones(size)|创建一个全为 1 的张量。|x = torch.ones((2, 3))|
|torch.empty(size)|创建一个未初始化的张量。|x = torch.empty((2, 3))|
|torch.rand(size)|创建一个服从均匀分布的随机张量，值在 [0, 1)。|x = torch.rand((2, 3))|
|torch.randn(size)|创建一个服从正态分布的随机张量，均值为 0，标准差为 1。|x = torch.randn((2, 3))|
|torch.arange(start, end, step)|创建一个一维序列张量，类似于 Python 的 range。|x = torch.arange(0, 10, 2)|
|torch.linspace(start, end, steps)|创建一个在指定范围内等间隔的序列张量。|x = torch.linspace(0, 1, 5)|
|torch.eye(size)|创建一个单位矩阵（对角线为 1，其他为 0）。|x = torch.eye(3)|
|torch.from_numpy(ndarray)|将 NumPy 数组转换为张量。|x = torch.from_numpy(np.array([1, 2, 3]))|

## （三）转换与属性

#### 张量转换

|**操作**|**说明**|**示例代码**|
|:----|:----|:----|
|torch.from_numpy(ndarray)|将 NumPy 数组转换为张量。（**共享内存**）。|x = torch.from_numpy(np_array)|
|x.numpy()|将张量转换为 NumPy 数组（**仅限 CPU 张量**）。|np_array = x.numpy()|

#### 张量属性

|**属性**|**说明**|**示例**|
|:----|:----|:----|
|.shape|获取张量的形状|tensor.shape|
|.size()|获取张量的形状|tensor.size()|
|.dtype|获取张量的数据类型|tensor.dtype|
|.device|查看张量所在的设备 (CPU/GPU)|tensor.device|
|.dim()|获取张量的维度数|tensor.dim()|
|.ndim|获取张量的维度数|tensor.ndim|
|.requires_grad|是否启用梯度计算|tensor.requires_grad|
|.numel()|获取张量中的元素总数|tensor.numel()|
|.is_cuda|检查张量是否在 GPU 上|tensor.is_cuda|
|.T|获取张量的转置（适用于 2D 张量）|tensor.T|
|.item()|获取单元素张量的值|tensor.item()|
|.is_contiguous()|检查张量是否连续存储|tensor.is_contiguous()|

## （四）相关操作

#### 张量操作

|**操作**|**说明**|**示例代码**|
|:----|:----|:----|
|+, -, *, /|元素级加法、减法、乘法、除法。|z = x + y|
|torch.matmul(x, y)|矩阵乘法。|z = torch.matmul(x, y)|
|torch.dot(x, y)|向量点积（仅适用于 1D 张量）。|z = torch.dot(x, y)|
|torch.sum(x)|求和。|z = torch.sum(x)|
|torch.mean(x)|求均值。|z = torch.mean(x)|
|torch.max(x)|求最大值。|z = torch.max(x)|
|torch.min(x)|求最小值。|z = torch.min(x)|
|torch.argmax(x, dim)|返回最大值的索引（指定维度）。|z = torch.argmax(x, dim=1)|
|torch.softmax(x, dim)|计算 softmax（指定维度）。|z = torch.softmax(x, dim=1)|

|**操作**|**说明**|**示例代码**|
|:----|:----|:----|
|x.view(shape)|改变张量的形状（不改变数据）。|z = x.view(3, 4)|
|x.reshape(shape)|类似于 view，但更灵活。|z = x.reshape(3, 4)|
|x.t()|转置矩阵。|z = x.t()|
|x.unsqueeze(dim)|在指定维度添加一个维度。|z = x.unsqueeze(0)|
|x.squeeze(dim)|去掉指定维度为 1 的维度。|z = x.squeeze(0)|
|torch.cat((x, y), dim)|按指定维度连接多个张量。|z = torch.cat((x, y), dim=1)|



#### 示例代码

```python
import torch

# 创建一个 2D 张量
tensor = torch.tensor([[1, 2, 3], [4, 5, 6]], dtype=torch.float32)
print("原始张量:\n", tensor)

# 1. **索引和切片操作**
print("\n【索引和切片】")
print("获取第一行:", tensor[0])  # 获取第一行
print("获取第一行第一列的元素:", tensor[0, 0])  # 获取特定元素
print("获取第二列的所有元素:", tensor[:, 1])  # 获取第二列所有元素

# 2. **形状变换操作**
print("\n【形状变换】")
reshaped = tensor.view(3, 2)  # 改变张量形状为 3x2
print("改变形状后的张量:\n", reshaped)
flattened = tensor.flatten()  # 将张量展平成一维
print("展平后的张量:\n", flattened)

# 3. **数学运算操作**
print("\n【数学运算】")
tensor_add = tensor + 10  # 张量加法
print("张量加 10:\n", tensor_add)
tensor_mul = tensor * 2  # 张量乘法
print("张量乘 2:\n", tensor_mul)
tensor_sum = tensor.sum()  # 计算所有元素的和
print("张量元素的和:", tensor_sum.item())

# 4. **与其他张量的操作**
print("\n【与其他张量操作】")
tensor2 = torch.tensor([[1, 1, 1], [1, 1, 1]], dtype=torch.float32)
print("另一个张量:\n", tensor2)
tensor_dot = torch.matmul(tensor, tensor2.T)  # 张量矩阵乘法
print("矩阵乘法结果:\n", tensor_dot)

# 5. **条件判断和筛选**
print("\n【条件判断和筛选】")
mask = tensor > 3  # 创建一个布尔掩码
print("大于 3 的元素的布尔掩码:\n", mask)
filtered_tensor = tensor[tensor > 3]  # 筛选出符合条件的元素
print("大于 3 的元素:\n", filtered_tensor)

```



