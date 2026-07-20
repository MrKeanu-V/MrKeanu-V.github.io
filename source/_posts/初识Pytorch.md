---
title: 初识Pytorch
author: MrKeanu
categories:
  - Incessant Coding-编程不辍
  - Deep Learning-深度学习
index_img: /image/index/pytorch.png
banner_img: /image/bg/flower_in_sky.jpg
banner_img_height: 70
banner_mask_alpha: 0.3
date: 2023-09-05 19:52:39
excerpt: Pytorch框架的初识
tags: [Pytorch, Deep Learning]
archive: false
---
# 一、初识Pytorch

![深度学习框架](/image/深度学习框架.png)
事实上有许多的[机器学习框架]( https://www.bilibili.com/video/BV1gGjBz2Ecc)，比如Google的TensorFlow，FaceBook的PyTorch等。目前，工业界应用最为广泛的依然是TensorFlow，新版的TensorFlow已经支持动态计算图；学术界则更为流行Pytorch框架。

## （一）发展历程

Pytorch前身是Torch，Torch是一个开源的机器学习框架，其编程语言是C和Lua。Torch早在2002年就发布了其初版，如今Torch依旧是比较热门的深度学习框架之一。因此，Pytorch底层依然使用C++实现，并提供了C++接口，如libtorch。

由于Torch编程语言本身的限制（Ｃ使用起来过于繁琐，而Lua使用者少并且现在几乎已经停止迭代了），FaceBook公司在2017年推出了以Python为主要编程语言的**PyTorch**。其优点是开源的代码和社区，本身其实也是经典机器学习库Torch框架的一个端口。



## （二）文档&源码

#### 官方文档

[Pytorch官方API文档](https://docs.pytorch.org/docs/stable/index.html)

[Pytorch官方教程文档](https://docs.pytorch.org/tutorials/index.html)

[Pytorch中文文档](https://pytorch-cn.readthedocs.io/zh/latest/) ~非官方~

学习任何一个框架或者库，最直接且高效的方法都应是直接参阅官方文档，对于晦涩的部分建议再查找相应博客或[Stack Overflow](https://stackoverflow.com/questions)。

当然，现在GPT可以作为很好的API查找工具，同时也能帮助你理解很多内涵。



#### Pytorch架构

[Pytorch源码](https://github.com/pytorch/pytorch)

常用组件如下

|                           主要组件                           | 描述                                                         |
| :----------------------------------------------------------: | ------------------------------------------------------------ |
|   [**torch**](https://pytorch.org/docs/stable/torch.html)    | 类似 NumPy 的张量库，不同于Numpy数组使用CPU内存，Torch支持GPU |
| [**torch.autograd**](https://pytorch.org/docs/stable/autograd.html) | 自动求导库，支持 torch 中所有可微分的张量操作                |
|  [**torch.jit**](https://pytorch.org/docs/stable/jit.html)   | 一个编译栈（TorchScript），用于从 PyTorch 代码创建可序列化和可优化的模型 |
|   [**torch.nn**](https://pytorch.org/docs/stable/nn.html)    | 一个与 autograd 深度集成的神经网络库，设计用于最大灵活性，nn即Neural network的缩写。 |
| [**torch.multiprocessing**](https://pytorch.org/docs/stable/multiprocessing.html) | 类似Python 的 multiprocessing 模块，但具有跨进程的神奇 torch 张量内存共享功能。适用于数据加载和 Hogwild 训练 |
| [**torch.utils**](https://pytorch.org/docs/stable/data.html) | 提供DataLoader、model_zoo和其他便利性工具函数                |

实际还包含torch.optim，torch.onnx，torch.functional，torch.random等等，可以在Pytorch的仓库源码中查看，torch/路径下。

**常用到的包我会在后续博文中讲解，需要更深入的话建议翻阅官方和并对照源码进行理解。**



## （三）常用依赖

#### 图像处理TorchVision

[TorchVision官方文档](https://docs.pytorch.org/vision/stable/index.html)

`torchvision` 包含流行的数据集、模型架构和计算机视觉中常用的图像变换。



#### 音频处理TorchAudio

[TorchAudio官方文档](https://docs.pytorch.org/audio/stable/)

`torchaudio`是一个使用PyTorch进行音频和信号处理的库。它提供I/O，信号和数据处理功能，数据集，模型实现和应用程序组件。





{% note info %}

多学习优秀的开源项目对个人编码能力尤其是架构理解提升显著，开始时看不懂或者看了前面忘了后面无碍，这也是需要积累的过程。

{% endnote %}

